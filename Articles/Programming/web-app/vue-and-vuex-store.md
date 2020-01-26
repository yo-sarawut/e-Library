
Vue & Vuex Store — Short Tutorial for Beginners
==

Recently I’ve started to play around with Vue, something which I didn’t really want to even start to code with for a long time, just because I was in love with React (before React it was Angular 1) — which from the very beginning was impressing me with how it was done comparing at that time to Angular, it was new experience.

Going back to Vue — if you haven’t tired it yet, I think it is time to reconsider that and give some time for learning Vue. Surprisingly (is a positive way) I found this framework very friendly — easy start, with good  [documentation](https://vuejs.org/v2/guide/), great community and tons of open-source libraries which can be used.

I would assume that it could be easier for me to start coding right away in it because of my previous experience with React and Angular, tho  _vue-cli_  is very handy in bootstraping a new project.

Before we start, am assuming that you have at least installed Vue and you are ready to code, if you haven’t done that yet — please go to Vue  [Installation](https://vuejs.org/v2/guide/installation.html)  page first.

Source code with examples can be found on my github profile:  [@maclisowski](https://github.com/maclisowski)



# Create new project

At first lets create a new project — in order to do that you can simply type in console:
```
 vue create example
```
When we are asked, which preset we should use — please choose default, which means that we want to use  _babel_  and  _eslit_.

Once installation is done, you should be able to see output similar to one as on screenshot below.



![](https://miro.medium.com/max/2298/1*fp7u3AHbrfSWM9DIgLzNjQ.png)

During installation, will be created directory with having same name as your project — in our case it is  **example**. Now it is time to go to newly created directory and see if everything got installed properly and if we can run default example application. To do that type in console:

```vue
 npm run serve
```
The output in console should be similar to one below, with the difference that port might be different (in time of writing this article am running different project in Vue on which am working on):



![](https://miro.medium.com/max/1036/1*xztKFZ5vIzIyR581ZXlJpw.png)

Copy Local address and open it in your browser, now you can see very first example of web app written in Vue



![](https://miro.medium.com/max/2552/1*SDseVdGdMAeoByihWIygkA.png)

Okay but what now? Most of all, we are missing one npm package, with out store, called  [Vuex](https://vuex.vuejs.org/)  which is state management library. Store management is very important part of every modern web application — you can save there data needed for your application to work, react on state updates and do some action, in majority of cases those are triggering re-rendering DOM.

To instal Vuex use this commad:
```javascript
npm install vuex — save
```
Once it is installed, lets open our project in IDE — in my case it is  [Visual Studio Code](https://code.visualstudio.com/)  — lets take a look at  **main.js**  file:



![](https://miro.medium.com/max/3334/1*jH58JPRKS-uxU-vwGYhsow.png)

All of that is just simple to run boilerplate, which uses one component  **HelloWorld.vue**  to display a page with content.



![](https://miro.medium.com/max/3348/1*gphwDKOIZK3lV5Ok6jvjtA.png)

Now, lets create a simple store and integrate it with Vue. Take a look at screenshot below — lines: 2 and 7. In line number 2 we have imported Vuex library into our project, then in look at line number 7, where we told Vue that we would want to use Vuex and that’s it in terms of integration Vue + Vuex — pretty simple right?

![](https://miro.medium.com/max/30/1*eZDlwh--_iE-y5Gt4GMCEw.png?q=20)

![](https://miro.medium.com/max/3354/1*eZDlwh--_iE-y5Gt4GMCEw.png)

Right now we have to create our store with initial state, prepare methods to update state as well as getters to retrieve data and make our store to be available in our Vue app instance.

We will have to restructure a little bit our tiny app in order to keep it clean. For those purposes we are going to create directory store in which we will have all files related with our Vuex store. Then in  **store/index.js**  file we will will create new  **Vuex.Store**  instance.



![](https://miro.medium.com/max/3350/1*Yb0DxT2B8UitPfD7YFydxQ.png)

As you can see here, right now  **Vue.use(Vuex)**  has been  **moved to store/index.js**  — it is required, otherwise there will be thrown an error:  _Error: [vuex] must call Vue.use(Vuex) before creating a store instance._

Guess I don’t have to explain — error message is pretty straightforward here :)

As you probably have noticed, in line number 3 we are importing file from store directory app.store.js — there is heart of our app store, there we are storing state, actions, mutations and getters. Lets take a look at it:



![](https://miro.medium.com/max/3350/1*Iolni40TgdWlvnhmCt9ysw.png)

Line 1 to 7 — those are name definitions for our actions and mutations.

Line 10 — initial app state

Line 14 — getters, are used to retrieve data from store state

Line 21 — actions, those we are dispatching later to store in components, in order to perform some actions related with updating state

Line 31 — mutations, are responsible for updating state values — those are called by actions

Since this example is just an counter which allows to increase/decrease value by 1 — everything should be pretty simple and straightforward in screenshot above. If anything is unclear, keep reading and at the end checkout repository with  [source code on github](https://github.com/maclisowski/vue-vuex-example).

Almost everything is set, now we need few updates in our  **HelloWorld.vue**  file — can be found in  **components**  directory — as well as in  **main.js**  file where we have to pass to Vue our store. Lets see:



![](https://miro.medium.com/max/3348/1*dqaHq81BVljYQcR7hQlfuw.png)

As mentioned earlier, we moved  _Vue.use.(Vuex)_  to  _store/index.js_  file, instead of that we are importing this fine here (line 3) and then we are passing our store to Vue instance — line 9.

Lets see what has happen in  **HelloWorld.vue** — I have removed everything what was between <template></template> tags and created simple placeholder to display counter value from our store and two buttons to increase/decrease value.


![](https://miro.medium.com/max/3354/1*NOMitmfFVILdUilpl594VQ.png)

Let`s discuss what is actually going on here in this file. In <template> you can see  _{{ appCounter }} —_ this is actual value from store app state. To get a value from store state we have to define computed method which will use method defined in store getters (line 18–20).

Now, on line 6 and 7 we have two buttons with defined on click events, to call methods responsible for dispatching action to the store to increase or decrease value of our counter. Those are defined in lines 22–29. As you have already noticed, to call an action from our store we can use  **this.$store.dispatch()**  method and as a parameter we have to pass name of our action defined before in  **store/app.store.js**  file and imported here in line 13.

Final result of our example application you can watch on this video:

Hope it can help anyone with starting journey with Vue :)

If you have any questions feel free to reach me out! Thanks for your time!

ref : [https://medium.com/@maciej.lisowski.elk/vue-vuex-store-short-tutorial-for-beginners-1befd8697654](https://medium.com/@maciej.lisowski.elk/vue-vuex-store-short-tutorial-for-beginners-1befd8697654)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDM3NzMyMzksLTIwNzI3MzczNjZdfQ
==
-->