
Vue.js App Performance Optimization: part 1 — Introduction to performance optimization and lazy loading.
===

**While mobile-first approach becomes a standard and uncertain network conditions are something we should always take into consideration it’s harder and harder to keep your application loading fast. In this series I’ll dig deep into Vue performance optimization techniques that we are using in** [**Vue Storefront**](https://github.com/DivanteLtd/vue-storefront) **and that you can use in your Vue.js applications to make them loading instantly and perform smooth. My goal is to make this series a full and complete guide on Vue apps performance.**

[Part 1 — Introduction to performance optimization and lazy loading.](https://vueschool.io/articles/vuejs-tutorials/lazy-loading-and-code-splitting-in-vue-js/)

[Part 2 — Lazy loading routes and vendor bundle anti-pattern.](https://itnext.io/vue-js-app-performance-optimization-part-2-lazy-loading-routes-and-vendor-bundle-anti-pattern-4a62236e09f9)

[Part 3 — Lazy loading Vuex modules](https://itnext.io/vue-js-app-performance-optimization-part-3-lazy-loading-vuex-modules-ed67cf555976)

Part 4 — Delivering good waiting experience and lazy loading individual components — soon

Part 5 — Lazy loading libs and finding smaller equivalents — soon

Part 6 — Performance-friendly usage of UI libraries

Part 7 — Making use of Service Worker cache — soon

Part 8 — Prefetching

-----

Part 1 — Introduction to performance optimization and lazy loading.
==

While mobile-first approach becomes a standard and uncertain network conditions are something we should always take into consideration it’s harder and harder to keep your application loading fast. In this series, I’ll dig deep into Vue performance optimization techniques that we are using in  [Vue Storefront](https://www.vuestorefront.io/?utm_source=vueschool.io&utm_medium=external-blog&utm_campaign=vuestorefront)  and that you can use in your Vue.js applications to make them loading instantly and perform smooth. My goal is to make this series a full and complete guide on Vue apps performance.

## How Webpack bundling works?

Most of the tips in this series will focus on making our JS bundle smaller. To understand while it’s crucial first we need to understand how Webpack is bundling all of our files.

While bundling our assets Webpack is creating something called  
dependency graph (click  [here](https://cloud.githubusercontent.com/assets/1365881/5745055/40da9236-9c26-11e4-9e2b-6611cd743423.png)  to see how it looks like). It’s a graph that links all of our files based on imports. Assuming we have a file called  `main.js`  specified as an entry point in our webpack config it will be a root of our dependency graph. Now every js module that we will import in this file will become its node in the graph and every module imported in these nodes will become their nodes.

Webpack is using this dependency graph to detect which files it should include in the output bundle. Output bundle is just a single (or multiple as we will see in the later parts) javascript file containing all modules from the dependency graph.

The bundle is essentially our entire application’s JavaScript.

We can illustrate this process with below image:

![](https://paper-attachments.dropbox.com/s_2E24013928DC2D1846E0F307F3A147533515D197E2854B22120C80C9A603E380_1556811094745_01.png)

Now that we know how bundling works, it becomes obvious that the bigger our project gets, the bigger the initial JavaScript bundle becomes.

The bigger bundle, the longer it takes to download and parse for our users. The longer a user has to wait, the more likely he is to leave our site. In fact,  [according to Google](https://www.thinkwithgoogle.com/marketing-resources/data-measurement/mobile-page-speed-new-industry-benchmarks/), 53% of mobile users leave a page that takes longer than three seconds to load.

As a summary,  **bigger bundle = fewer users**, which can be directly translated to a loss of potential revenue. Bing is a good example -  **2 seconds of delay resulted in a 4.3% loss in revenue per visitor**  **for them.**

## Lazy loading

So how we can cut off bundle size when we still need to add new features and improve our application? The answer is easy — **lazy loading and code splitting.**

As the name suggests  **lazy loading is a process of loading parts (chunks) of your application lazily**. In other words — loading them only when we really need them. Code splitting is just a process of splitting the app into this lazily loaded chunks.

![](https://paper-attachments.dropbox.com/s_2E24013928DC2D1846E0F307F3A147533515D197E2854B22120C80C9A603E380_1556811200558_02.png)

In most cases, you don’t need all the code from your Javascript bundle immediately when a user visits your website.

For example, we don’t need to spend valuable resources on loading the “My Page” area for guests that visits our website for the first time. Or there might be modals, tooltips and other parts and components that are not needed on every page.

It is wasteful at best, to download, parse and execute the entire bundle everything on every page load when only a few parts are needed.

Lazy loading allows us to split the bundle and serve only the needed parts so users are not wasting time to download and parse code that’ll not be used.

To see how much of the JavaScript code is actually used in our website we can go to the devtools -> cmd+shift+p -> type coverage -> hit ‘record’. Now we should be able to see how much of the downloaded code was actually used.

![](https://paper-attachments.dropbox.com/s_2E24013928DC2D1846E0F307F3A147533515D197E2854B22120C80C9A603E380_1556811287345_03.png)

**Everything marked as red is something that is not needed on current route and can be lazily loaded.**  If you are using source maps you can click on any file in this list and see which of it’s parts were not invoked. As we can see even  [vuejs.org](https://vuejs.org/)  has a huge room for improvement ;).

By lazy loading proper components and libraries we managed to cut off the bundle size of Vue Storefront by 60%! That’s probably the easiest way to gain some performance boost.

Ok, we know what lazy loading is and that it’s pretty useful. It’s time to see how we can use lazy loading in our own Vue.js applications.

## Dynamic imports

We can easily load some parts of our application lazily with  [webpack dynamic imports](https://webpack.js.org/guides/code-splitting/). Let’s see how they work and how they differ from regular imports.

If we import a JavaScript module in a standard way like this:

```js
// cat.js
const Cat = {
  meow: function () {
    console.log("Meowwwww!")
  }
}
export default Cat

// main.js
import Cat from './cat.js'
Cat.meow()
```

It will be added as a node of a  `main.js`  in the dependency graph and bundled with it.

But what if we need our  `Cat`  module only under certain circumstances like a response to a user interaction? Bundling this module with our initial bundle is a bad idea since it is not needed at all times. We need a way to tell our application when it should download this chunk of code.

This is where dynamic imports can help us! Now take a look at this example:

```js
// main.js
const getCat = () => import('./cat.js')
// later in the code as a response to some user interaction like click or route change
getCat()
  .then({ meow } => meow())
```

Let’s take a quick look at what happened here:

Instead of directly importing  `Cat`  module we created a function that returns the  `import()`  function.  **Now webpack will bundle the content of the dynamically imported module into a separate file**. The function representing dynamically imported module returns a Promise that will give us access to the exported members of the module while resolved.

We can then download this optional chunk later, when needed. For instance as a response to a certain user interaction(like route change or click).

By making a dynamic import we are basically isolating the given node (in that case  `Cat`) that will be added to the dependency graph and downloading this part when we decide it’s needed (**which implies that we are also cutting off modules that are imported inside  `Cat.js`**).

Let’s see another example that will better illustrate this mechanism.

Let’s assume we have a very small web shop with 4 files:

-   `main.js`  as our main bundle
-   `product.js`  for scripts in product page
-   `productGallery.js`  for product gallery in product page
-   `category.js`  for scripts in category page

Without digging too much into details let’s see how those files are distributed across the application:

```js
// category.js
const category = {
  init () { ... }
}
export default category

// product.js
import gallery from ('./productGallery.js')

const product = {
  init () { ... }
}
export default product

// main.js
const getProduct = () => import('./product.js')
const getCategory = () => import('./category.js')

if (route === "/product") {
  getProduct()
    .then({init} => init()) // run scripts for product page
}
if (route === "/category") {
  getCategory()
    .then({init} => init()) // run scripts for category page
}
```

In above code, depending on the current route we are dynamically importing either  `product`  or  `category`  modules and then running  `init`  function that is exported by both of them.

Knowing how dynamic imports are working we know that  `product`  and  `category`  will end up in a separate bundles but what will happen with  `productGallery`  module that wasn’t dynamically imported? As we know by making module dynamically imported  **we are cutting part of the dependency graph.**  Everything that was imported inside this part will be bundled together so  `productGallery`  will end up in the same bundle as  `product`  module.

In other words we are just creating some kind of a new entry point for the dependency graph.

![Each color is representing separate JS bundle](https://paper-attachments.dropbox.com/s_2E24013928DC2D1846E0F307F3A147533515D197E2854B22120C80C9A603E380_1558377879646_image.png)

## Lazy loading Vue components

Now that we know what lazy loading is and why we need it. It’s time to see how we can make use of it in our Vue applications.

The good news is that it’s extremely easy and we can lazily load the entire Single File Component, with it’s CSS and HTML with the same syntax as previously!

```js
const lazyComponent = () => import('Component.vue')
```

…that’s all you need! Now the component will be downloaded only when it’s requested. Here are the most common ways to invoke dynamic loading of Vue component:

-   function with import is invoked

```js
const lazyComponent = () => import('Component.vue')
lazyComponent()
```

-   component is requested to render

```html
<template>
  <div> 
    <lazy-component />
  </div>
</template>

<script>
const lazyComponent = () => import('Component.vue')
export default {
  components: { lazyComponent }
}

// Another syntax
export default {
  components: {
    lazyComponent: () => import('Component.vue')
  }
}
</script>
```

Please note that the invocation of lazyComponent function will happen only when component is requested to render in a template. For example this code:

```html
<lazy-component v-if="false" /> 
```

The component will not be loaded until it is required in the DOM, which is as soon as the v-if value changes to true.

## Summary and what’s next

Lazy loading is one of the best ways to make your web app more performant and reduce the bundle size. We learned how to use lazy loading with Vue components.

In the next part of this series I’ll show you the most useful (and also the fastest) way to gain some significant performance boost on any Vue.js application.

You will learn how to split your Vue code with async routes along with recommended best practices for this process.

-----

Part 2 — Lazy loading routes and vendor bundle anti-pattern.
===

In the previous article, we learned about the concept of lazy loading and briefly understood how webpack bundling works under the hood. With a good understanding of basics, we can see how to apply this knowledge in a real-world Vue application. The trick you will earn today could dramatically decrease your bundle size in just a few minutes. Feel excited? Let’s see what it is!

## Problem with growing applications

Let’s assume we are building a very simple portfolio website with Vue. Even such a simple website will need some kind of routing so we need to use  `vue-router`  to split it into 2 individual pages - Home and About.

Our file structure and routing could look more or less like below:

```js
// router.js
import Home from './Home.vue'
import About from './About.vue'

const routes = [
  { path: '/', component: Home }
  { path: '/about', component: About }
]
```

![](https://cdn-images-1.medium.com/max/1200/1*35NnFOrorhQThxQX7Oml3w.png)

When we want to publish our application to the internet we need to build it first and get rid of everything that can slow it down. It means that all files need to be concatenated, transpiled to pure JavaScript and minified to ensure the smallest possible size of the production bundle (a single js file that will be downloaded by the end-user). The bigger the production bundle is the longer it takes for the user to download it and for the browser to parse it.

It’s important to mention that webpack will do all of this for us with a default configuration!

**It turns out that 1 second is enough for the user to do a mental context switch and potentially leave our website**  so it’s great that webpack is doing all those optimizations for us. Otherwise, we might be losing some of our visitors!

![Slide from amazing talk about performance and human perception by Ilya Grigorik https://www.youtube.com/watch?v=7ubJzEi3HuA](https://paper-attachments.dropbox.com/s_3E2B6D676393E308921DFCC4F358F8BC4A52C080E465D3F2D31F0A4B09CFFE85_1562593516588_image.png)

Despite all those build-time magic we are still delivering code that isn’t optimized. Do you know why? Let’s see

As you probably noticed depending on which route we are visiting we might not need either  `Home.vue`  or  `About.vue`  (with it’s  `lodash`  dependency) yet both of them are in the same  `app.js`  bundle and will be downloaded no matter what route user visits. What a waste of downloading and parsing time!

It’s not a big deal if we are downloading one extra route but you can imagine this app growing bigger and bigger and any new addition will mean that the user will be downloading a bigger bundle on the initial visit. The more time the user has to stare at the white screen the bigger chance is that he/she will open Instagram feed with funny cat images and (maybe) never come back!

![This should be you when your bundle is too big.](https://pet-happy.com/files/up/2014/09/scared-cat.jpg)

## Route-based code splitting with vue-router

To avoid making our application worse by actually making it better and adding new features  **we just need to make separate bundles for each route**  using dynamic import syntax that we learned in the previous article. Only the code from route that is currently visited by the user will be downloaded.

Like everything else in Vue.js — it’s extremely easy. Instead of importing components directly into route objects you need to pass a dynamic import function there. The route component will be downloaded ONLY when the given route will be resolved.

So instead of importing route component statically like this:

```js
// router.js
import Home from './Home.vue'
import About from './About.vue'

const routes = [
  { path: '/', component: Home }
  { path: '/about', component: About }
]
```

We should import it dynamically. Dynamic import will generate a new bundle with this route as an entry point:

```js
// router.js 
const routes = [
  { path: '/', component: () => import('./Home.vue') }
  { path: '/about', component: () => import('./About.vue') }
]
```

Knowing this let’s see how our bundles will look like with dynamic imports in comparison to single  `app.js`  file:

![](https://cdn-images-1.medium.com/max/800/1*O4ec5EhhM_ULzY4LH6xk-g.png)

With above setup webpack will create three bundles:

-   `app.js` — our main bundle with app entry point (main.js) and libs/components needed in every route (in this case it’s  `vue`  and  `vue-router`)
-   `home.js` — bundle with Home page that will be downloaded only when route with  `/`  path is entered
-   `about.js` — bundle with About page (and it’s dependency — `lodash`) that will be downloaded only when route with  `/about`  path will be entered.

**Side note:**  _Bundle names here are not the real ones generated by webpack for the sake of simplicity. Webppack is actually generating something like_  `0.js`  `1.js`  _etc depending on your configuration_

This simple technique is sufficient for almost every application and can give extremely good results in a very short time. Assuming we have similar number of code in every route we reduced the initial bundle size by 50% in just 2 lines of code! The improvements are even bigger for a for an application with more routes. In fact this technique is so effective that in many cases it’s enough to solve most of the performance issues your application could have.

## Code splitting in Nuxt

If you’re using Nuxt I’m happy to inform you that above technique is applied there out of the box. Nuxt’s default directory-based routing system is code-splitting every route by default!

## Common vendor bundle anti-pattern

Now let’s take a look at the very popular and commonly used anti-pattern that can make your route-based code splitting impact less powerful.

Sometimes it’s tempting to put all of our third-party dependencies from  `node_modules`  in one file (usually called  `vendor.js.`) It seems performance-wise to download all of them only once and reuse in the whole application. Let me explain why it’s not.

While it may sound beneficial, this approach is introducing the same problem that we had with bundling all routes together. Have a look at the below diagram:

![](https://cdn-images-1.medium.com/max/1600/1*sPuEIhcm1NqDjVRCKCXVhA.png)

Do you see the problem? Even though we need lodash only in a single route it’s downloaded together with other dependencies no matter on which route the user is. It means that he/she will need to wait for lodash to be downloaded and parsed before seeing the website.

Bundling all dependencies in one file will make your app load slower. This is certainly not what you want to achieve!

By not bundling all dependencies in one file and instead of importing them in the needed routes we ensure that it’s only downloaded when needed. Though, without further optimization, it does come with an overhead and code duplication.

Let’s assume  `Home.vue`  also needs lodash.

![](https://cdn-images-1.medium.com/max/1600/1*VPV1rLABkruxSoGhKDbjJg.png)

In that case navigating from  `/about`  (`About.vue`) to  `/`  (`Home.vue`) (or in reversed order) will end up with downloading the library twice.

It’s still much better to download a few small dependencies again instead of forcing your user to wait for all of them to be downloaded on the initial visit but we have room for improvement. If we already have this dependency it’s just stupid not to reuse it, right?

This is where webpack  [splitChunksPlugin](https://webpack.js.org/plugins/split-chunks-plugin/)  can help us. Just by adding these few lines of code in the webpack config, webpack will automatically group all dependencies shared in various bundles into a separate one. This bundle will only be downloaded once and then reused.

```js
// webpack.config.js
optimization: {
  splitChunks: {
    chunks: 'all'
  }
}
```

In  `chunks`  property we are telling webpack which chunks (output bundles) of code should be optimized for code duplication. Setting this property to  `all`  as you probably have guessed means that it should optimize all of them.

You can read more about this process in the  [webpack docs](https://webpack.js.org/guides/code-splitting/#prevent-duplication).

## Summary

Splitting your code by routes is without a doubt the best way to achieve significantly better performance results in your application and you should implement it as soon as possible.

**Introducing this technique in Vue Storefront took us 20 minutes and reduced the size of the initial bundle by almost a half!**

While applying many of the optimization techniques from day zero is considered unnecessary premature optimization, routes code-splitting is certainly not something you should postpone.

By code-splitting your routes from the beginning, you get a performance app right away!

## What’s next?

You already know a lot about lazy loading Vue components. In the next part, you’ll master this technique by understanding which components should be loaded lazily and how to deliver a smooth waiting experience to your users when those components are being downloaded.

-


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2NTA2NDA2MF19
-->