How to Build BookSearch App using Vue.js and ElasticSearch
===
- [https://medium.appbase.io/building-booksearch-application-using-vue-and-elasticsearch-a39615f4d6b3](https://medium.appbase.io/building-booksearch-application-using-vue-and-elasticsearch-a39615f4d6b3)
![enter image description here](https://miro.medium.com/max/2880/1*xX5Q917ujpQsdZp-gy72zw.png)

In this post, we are going to build a Booksearch Application using Vue.js and ElasticSearch. You might have already heard of Vue.js, one of the fastest growing JavaScript frameworks. You might also have heard about ElasticSearch — it is the #1 search engine. In any case, I will do a walkthrough explaining the basics of Search and build the app in a step-by-step manner.

> Before diving in, you can try out the Live demo of the final app  [here](https://y2rvj53koz.codesandbox.io/).
> 
> .
> 
> .
> 
> .
> 
> .

# What is ElasticSearch

ElasticSearch is a  _blazing fast, open-source, full-text search engine_. It allows you to  **store**,  **search**, and  **analyze**  both small and large volumes of data quickly (we are talking milliseconds here). It is generally used as the underlying engine/technology to power applications that have complex search features and requirements. You can read more about it  [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started.html).

# Why ElasticSearch

With ElasticSearch, you can build a fast search which utilizes its powerful Query DSL. However, setting up ElasticSearch correctly requires a lot of work. For instance, the mappings, analyzers, and tokenizers need to be set correctly or you may not receive accurate search results back. Besides, the more filters that get applied along with the search query, the more complex the resulting search query becomes.

# Setting Up ElasticSearch

Setting up and maintaining our own search engine cluster can be time-consuming and costly. So we will be using  **Appbase.io** to save our time and cost of maintaining Cluster.

At appbase.io, we have built some open-source tools to help you do all these things within a matter of clicks.

-   Tool to  **add data**  into ElasticSearch —  [Importer](http://importer.appbase.io/)
-   Tool to  **view ElasticSearch data**  like an excel sheet —  [Data Browser](https://opensource.appbase.io/dejavu/)
-   Tool to  **generate relevant ElasticSearch queries**  easily —  [Query Builder](https://opensource.appbase.io/mirage/)

In this blog post, we will be using these tools to utilize the strength of ElasticSearch with Vue to build powerful apps.

# Building our Search Backend

As mentioned above, we will be using  [appbase.io](https://appbase.io/)  for our search backend. It offers a real-time search API service based on ElasticSearch. This saves us time and cost of setting up and maintaining our own search engine cluster.

_This means that we wouldn’t require writing any server code. 💥_

In order to make Booksearch application, we will need a dataset of some really good books. I have already created an  [appbase.io](https://appbase.io/)  app with the books dataset indexed over  [here](https://dejavu.appbase.io/?&appname=good-books-yj&url=https://gBgUqs2tV:3456f3bf-ea9e-4ebc-9c93-08eb13e5c87c@scalr.api.appbase.io&mode=view). You can either clone this dataset to use your own credentials or copy the below credentials:

app="good-books-yj"  
credentials="gBgUqs2tV:3456f3bf-ea9e-4ebc-9c93-08eb13e5c87c"

![](https://miro.medium.com/max/30/1*OHJ1oyLeuV30NAahXFrFOw.png?q=20)

![](https://miro.medium.com/max/2880/1*OHJ1oyLeuV30NAahXFrFOw.png)

Good Books Dataset in  [Dejavu](https://dejavu.appbase.io/)

## How to use ElasticSearch with Vue.js?

We will be using the  [**ReactiveSearch-vue**](https://opensource.appbase.io/reactivesearch/vue)  open-source library to build the Booksearch application in this post. This library offers a range of highly customizable rich UI components that can connect with an ElasticSearch index hosted anywhere. It provides scaffolding to build UIs such as Airbnb, Yelp, you name it. We will show how simple it is to build one by creating our Booksearch app.

ReactiveSearch for Vue is a port of ReactiveSearch (written for React) that has been downloaded over 125,000 times in the past year and currently powering hundreds of production search UIs. You can read more about the Vue.js announcement here:

[](https://medium.appbase.io/vue-js-components-for-building-search-uis-7b2a1b6fe159?source=post_page-----a39615f4d6b3----------------------)

## 

Vue.JS Components for building Search UIs

### 

We’re super excited to announce the first release of Reactive Search for Vue, a UI components library for…

#### 

medium.appbase.io

# Setting Up Frontend

# Step 1: Base setup of Vue.js with ReactiveSearch

We will use  [Codesandbox.io](https://codesandbox.io/)  to help us build our application in a step by step fashion. Open the above link and click on the  `Open Vue`  button.

![](https://miro.medium.com/max/30/1*_89jAC47icWAmGlR8cbADQ.png?q=20)

![](https://miro.medium.com/max/2696/1*_89jAC47icWAmGlR8cbADQ.png)

CodeSandbox for Vue

If you instead want to develop this locally, you can also use  `vue-cli`. You can read more about it  [here](https://opensource.appbase.io/reactive-manual/vue/getting-started/reactivesearch.html#step-0-create-boilerplate-with-vue-cli).

**Install ReactiveSearch for Vue**

Now we can add our dependency by clicking the  `Add Dependency`  button on CodeSandbox and searching for  `reactivesearch-vue`, or if you are working locally you can install the package:

yarn add @appbaseio/reactivesearch-vue

# Step 2: Adding components from ReactiveSearch library

Now that we have the dataset to play around with and we are also done with our setup, it’s time for adding components to our app.

We need to first register the library so that we can use the components in the  `main.js`. We can do this via the  `use`  method of  `Vue`:

import ReactiveSearch from "@appbaseio/reactivesearch-vue";Vue.use(ReactiveSearch);

## Connecting our Search Backend via ReactiveBase Component

All the ReactiveSearch components are wrapped inside a container component —  `ReactiveBase`  which connects the components to an Elasticsearch index. We’ll apply this in the  `/src/App.vue`  file. You can read more about  `Reactivebase`  [here](https://opensource.appbase.io/reactive-manual/vue/getting-started/reactivebase.html).

The  `app`  and  `credentials`  are taken from my appbase.io app. In case you are using  [your own app](https://dashboard.appbase.io/), you can swap the values in L2 and L3.

Screen after adding ReactiveBase 👋

## Use DataSearch Component for the main search

`DataSearch`  creates a search box UI component that is connected to one or more database fields.

`dataField`  prop values are the name of the field on which we want to apply our search.

`iconPosition`  is used to align the search icon to right or left.

You can learn more about this component props over  [here](https://opensource.appbase.io/reactive-manual/vue/search-components/datasearch.html#props).

Screen showing DataSearch Component 🎇

## Use MultiList Component for Authors filter

We always want to read the book from our favorite authors so why not we built an option to select our favorite authors and search through the list of authors.

In this component,  `dataField`  attribute defines the data field to be connected to the component’s UI view.  `title`  attribute gives the heading to the component, while  `class`  attribute is used to provide the class name to the MultiList container. We can use  `react`  prop which allows components to watch each other and update their data reactively. For example, an Authors Filter component can update its data based on the selected fields in the Rating Filter component and DataSearch component.

You can learn more about the attributes of this component  [here](https://opensource.appbase.io/reactive-manual/vue/list-components/multilist.html#props).

Screen After adding MultiList ✨

## Use RatingsFilter Component for Rating filter

We want only the best books for us, so why not create an option to filter the best-rated books on our dataset.

`SingleRange`  component displays a curated list of items where only one item can be selected at a time. Each item represents a range of values, specified in the  **data**  prop of the component.

In this component,  `dataField`  attribute defines the data field to be connected to the component’s UI view.  `title`  attribute gives the heading to the component, while  `:data`  attribute is a collection of UI  `labels`  with associated  `start`  and  `end`  range values. You can read more about the attributes of component  [here](https://opensource.appbase.io/reactive-manual/vue/range-components/singlerange.html).

`:data`  is the shorthand for  `v-bind:data`  which is used to pass data to the components.

Screen after adding SingleRange 🚀

# Step 3: Use ReactiveList Component for displaying Book Results

`ReactiveList`  creates a data-driven result list UI component. This list can reactively update itself based on changes in other components or changes in the database itself.

ReactiveList Component

In this component,  `pagination`  is used to show the pagination at bottom of the list.  `react`  is used to watch changes through different component like SingleRange and MultiList in our case. You can read more about this component properties  [here](https://opensource.appbase.io/reactive-manual/vue/result-components/reactivelist.html#props).

Notice  `slot`  and  `slot-scope`  it is used to get data from the child component to parent component. If you have used  `React`  it is like a  `render-prop`  . You can read more about it  [here](https://vuejs.org/v2/guide/components-slots.html).

Screen after adding the ReactiveList component ✨

# Step 4: Styling the Application

We will now make use of some styles to make the application look elegant and professional. We can add styles to an element using  `class`  and adding their respective CSS in  `styles.css`.

You can get all the styles  [here](https://gist.github.com/jyash97/0a1e03aea7118e974e03902425e2d069)  & add them to  `App.vue`  .

We will also make this app mobile responsive. To do this, we will use a  `variable`  to hide/show filters using a button when we are on a mobile viewport.

Adding styles and Methods & structuring to handle small screen 📱

Button to switch views

`@click`  is shorthand for  `v-on:click`. It is used to track whenever a click event is fired on the button.

Final Application 📚

# Summary

Here comes the end of our journey, and we have got our awesome Booksearch app built with ReactiveSearch-Vue. To summarize everything so far:

This post introduces ReactiveSearch-Vue — A Vue.js UI components library for ElasticSearch that provide scaffolding for building great search experiences. Next, we went step-by-step to add different UI components and style our app.

-   **Step 1**: Base setup for Vue with ReactiveSearch —  [CodeSandbox here](https://codesandbox.io/s/8x0lll36o9).
-   **Step 2**: Adding components from ReactiveSearch library —  [CodeSandbox here](https://codesandbox.io/s/pwmo3x210x).
-   **Step 3**:  Displaying data using ReactiveList —  [CodeSandbox here](https://codesandbox.io/s/ovoxo4q00q).
-   **Step 4**: Adding styles to make responsive and professional —  [CodeSandbox](https://codesandbox.io/s/9167mmkqlo).

> Check out the live demo  [here](https://y2rvj53koz.codesandbox.io/).

Alternatively, if you want to build this app locally using vue-cli, you can check out the Github repo  [here](https://github.com/jyash97/good-books).

# Useful References

All ReactiveSearch components can be interactively tried using the playground at  [https://reactivesearch-vue-playground.netlify.com/](https://reactivesearch-vue-playground.netlify.com/).

The documentation for all the components is available at  [https://opensource.appbase.io/reactive-manual/vue.](https://opensource.appbase.io/reactive-manual/vue/)

Finally,  [go ★ ReactiveSearch](https://github.com/appbaseio/reactivesearch)  on Github so you can find it when you need to build that awesome search!
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzMDE5MTcxM119
-->