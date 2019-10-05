Vue.js Advanced Reactivity API and Caching Method-style Getters
===

![enter image description here](https://miro.medium.com/max/1280/1*41oEHeq_kwMWNX9KQGMtIQ.jpeg)

We’re going to talk about a common request when working with relational data in Vuex. Why and how to cache method-style getter invocations, though the principles would also apply to method-style computed properties.

If you have been following recent Vue v3 RFCs, you might have come across the  [Advanced Reactivity API](https://github.com/vuejs/rfcs/pull/42), which comes as a very welcome direction for Vue to take. This article is written using Vue v2, but ultimately the code will be simplified if this RFC is implemented.

Firstly, although both property-style and method-style getters offer caching as part of core Vuex functionality, method-style getter invocations do not cache results. If that doesn’t make much sense, keep reading, it should become clear.

# What is a Method-style Getter?

Below is the example from the Vuex documentation of a method-style getter, sometimes referred to as a parameterized getter.
```vue
getTodoById: (state) => (id) => {  
  return state.todos.find(todo => todo.id === id)  
}
```
Normally a getter works by processing state into a given result.

todoCount: (state) => state.todos.length,

This will mean that  `store.getters.todoCount`  might provide the value 12, which will be cached in the event that the value is accessed again without any underlying reactive data changing.

isTodoOpen: (state) => (id) =>  
  !!state.todos[id].assignee &&   
  state.todos[id].status !== 'complete’,

The above example can be accessed by  `store.getters.isTodoOpen(123)` which will return a boolean. This value is not cached, calling it repeatedly will result in multiple executions.

> So what is cached here?

Nothing from a reactive standpoint. When the getter property is accessed on the store,  `store.getters.isTodoOpen`, just prior to invocation, this will run the outer function which will not access any reactive data, but create a function, an arrow which accepts id. This created function is now cached.

# Why aren’t the results of these getters cached?

There are lots of good reasons not to cache the results of these functions. How many times would you expect them to be called? Will the cache grow very big? How should the cache key be calculated? When should the cache be invalidated?

There are a lot of broad questions with no concrete answers, and there is a danger the functionality would be used without proper knowledge of the impact that poor caching could have on performance.

Ultimately, for anyone who thinks they would benefit from caching these results, it is important you measure the performance of the cache.

Maybe there isn’t a one-size-fits-all solution, which is why the mechanics are explained below and if you need something different, you should be able to put it together yourself.

# Our Use Case

At Teamwork, we have a suite of products that are based on frequently changing, highly relational data. Our flagship product is a project management tool, and we have a system with a lot of entities, with a lot of data and a lot of relationships.

You might be querying your backend for a denormalized view on your data closely coupled with the current view in the browser.

There are however benefits to treating your Vuex store as an extension of your database, where normalized data is kept. Where each module might match a database table and use of keys is widespread just like in a database, see this article on  [module structure](https://medium.com/js-dojo/structuring-vuex-modules-for-relationships-speed-and-durability-de25f7403643)  for an introduction to the concept. In this case, getters can take on the role of the  [**database view**](https://www.essentialsql.com/what-is-a-relational-database-view/). The denormalized, use case specific, query which relies on underlying normalized data.

> Getters might be used to filter, merge, enrich or map data.

Worth calling out at this point, that this means creating new arrays or new objects as getters don’t, and shouldn’t, mutate state.

Now that we have clarified that and hopefully not gone off on too much of a tangent, let’s look at some code.

# Mapped Collection render

Below is a render of 3 tasks, each task is a record in the store which has a getter to 'map' it, the example is contrived but the principal is the same. Each mapped record is passed to a component responsible for rendering it ([JSFiddle link](https://jsfiddle.net/mikeapr4/0kszxL64/)).

Each component render includes a timestamp and a short time after render, a field on one record is changed.

Before the explanation, keep in mind this example is for illustration and although it could be refactored to remove the flaw, there are real world scenarios that cannot.

The important thing to notice is that when the field on a single record is changed,  **all**  3 record components update! But why?

Is it due to some kind of over-reactivity? No, though the behaviour does look that way. What is happening is that …

1.  The record change triggers the parent component to re-render …
2.  … which means that  **all**  the getters are called again.
3.  Because they are not cached they will re-run and therefore created new objects …
4.  … which will not be strictly equal to the previous objects …
5.  … therefore trigger each record component to re-render.

Obviously the cost is negligible in the example, but in the real world, these kinds of inefficiencies don’t go unnoticed.

# With some rudimentary caching

Let’s take the above example and add in some simplistic caching.

Above is a new method-style getter which maintains a cache (above the invocation scope), each invocation of the getter will check the cache based on a key and either return the cached value or re-run the original getter. This caching wouldn’t be recommended as it doesn’t leverage reactivity at all, but it will prove the benefit caching can give.

Below is the first snippet with the getter added (link to  [JSFiddle](https://jsfiddle.net/mikeapr4/5yLd9zvc/)).

Note that the re-render does not trigger all the record components to re-render, just the one that was changed.

# The right caching solution

The above code is far too simplistic, it isn’t reactive and it is missing cleanup code. Here is another solution:

Before explaining how it works, how should it be used? As follows:

const { plugin, cache } = methodGetterCacher();  
...  
plugins: [plugin],  
...  
getters: {  
  mappedTask: cache((state) => (id) => ({  
    name: state.tasks[id].name.toUpperCase(),  
  })),  
},

Without the proposed API, using this code requires access to the store, hence the need for a plugin. An ugly nuisance, but it will only be necessary once.

The outer getter function is then passed to the utility and a new  **cached**  function is returned, this is a clean interface.

Let’s look at the just the wrapping code for a second…

**[A]** const methodStyleCache = (getVM, getter) => {  
  ...  
  **[B]** return (...args) => {  
    ...  
    **[C]** const innerMethod = getter.call(null, ...args);  
  
    **[D]** return (id) => {      ...  
      watcher = computed(getVM(), () => innerMethod(id));  
      ...  
      return watcher.lazyValue();  
    };  
  };  
};

What is happening here is that we take the input getter function  **[A]**  which has an outer and inner function, we create a new outer function  **[B]**, we then run the outer function  **[A]**  to get the inner function  **[C]**, and then create a new inner function  **[D]**, which will execute the input function  **[C]**. In a nutshell, we are wrapping both the outer and inner functions.

# Advanced API Polyfill

This solution has a  `computed`  function which aims to replicate computed functionality within Vue, which is the foundation for the way getters work within the store. This function in theory would be deprecated by the new API.

Essentially this is creating a getter for each inner function ID. We need to do this because accessing the getter value from “cache” should still pass dependencies from the inner getter to the calling code. If this doesn’t make sense, this  [article](https://medium.com/dailyjs/tracing-or-debugging-vue-js-reactivity-the-computed-tree-9da0ba1df5f9)  on debugging reactivity should shed some light on it, but feel free to continue without deep diving.

A downside to this solution is that it relies on  _unpublished_  access to Vue. As always, this interface cannot be guaranteed in future Vue versions. However, even if the new v3 API is abandoned, and furthermore this interface no longer available (a very unlikely scenario). This feature is for performance gain, if it were lost, the functionality of the application would not be broken. It has already been confirmed that v3 comes with significant performance improvements, so it may even be the case this functionality is no longer needed.

Regardless, the option is there to copy the Watcher unit tests from Vue into your own codebase ([observer/watcher.spec.js](https://github.com/vuejs/vue/blob/dev/test/unit/modules/observer/watcher.spec.js)), therefore ensuring that if a newer version comes along which breaks this interface, tests will fail and identify the problem in development rather than production.

# Measure it

Here is a  [JSFiddle](https://jsfiddle.net/mikeapr4/j1Ldha5s/)  with the above code in action, but I have also added simple counters for cache hits and misses which get logged to the console. This way the cache performance can be evaluated.

# Further possibilities

As mentioned at the start, this functionality can be applied to computed properties with some tweaking also, and if you want to delve deeper and are interested in applying the cache with a limited size, take a look at this  [gist](https://gist.github.com/mikeapr4/8436ce26952bae0e20072eb6d10ff43a).

Even if you aren’t ready to use this functionality now, I hope it has been an interesting read, and like me, you are keen to see the Advanced Reactivity API arrive in Vue.

[**Source :**](https://engineroom.teamwork.com/vue-js-advanced-reactivity-api-and-caching-method-style-getters-a80979b6660)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MzQ2ODE5OTNdfQ==
-->