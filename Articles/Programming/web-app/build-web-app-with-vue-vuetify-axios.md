How to build a web app with Vue, Vuetify and Axios
===
[Source:](https://medium.com/javascript-in-plain-english/implement-movie-app-with-vue-vuetify-axios-open-movie-database-api-d12290318cf9)

![enter image description here](https://miro.medium.com/max/1600/1*dA0K8ZQ4yQn1Ld4JQBG4ug.png)

# Introduction

In this article, we will be building a Vue.js Application supported by Vuetify and Axios. The aim of this article is to implement a movie application which will be calling on an API. The user will be able to search for movies. The API will retrieve movies with all the search details. When a user clicks on a movie, it will give more details of each movie. It’s a fairly simple App, but it will explain the use case of calling the API from the Vue.js App.

# Contents

1.  Why Axios?
2.  Why Vuetify?
3.  A brief about the movie API
4.  Calling and testing API and Test.
5.  Create an App
6.  Requirement and structure of the App
7.  Add Vuetify to the Project
8.  Add vue-router to the project
9.  Add axios to the project
10.  Remove the currently scaffolded component
11.  Create LatestMovies component
12.  Implement Movie Component
13.  Display the ratings
14.  Add Search Movie component
15.  An issue with search movie and how we can rectify it
16.  Add a warning message if there is no search data in the API
17.  Creating a central file for axios/refactoring
18.  Wrapping Up and source code

# 1. Why Axios?

In Vue.js App, we can display the data from an external API. This can be done by vue-resource and axios. Axios is a 3rd part library and it is a popular one.  [Here is the official link for using Axios with Vue.js](https://vuejs.org/v2/cookbook/using-axios-to-consume-apis.html).

The important point to be noted here is that in the official docs there are no details about installing axios to the Vue.js app. We will cover this in Section 9:  _Add axios to the project_.

# 2. Why Vuetify?

Vuetify is a material design framework built on top of Vue.js. It has nice UI components and which can be readily available to use on Vue.js.

# 3. A brief about the movie API

[http://www.omdbapi.com/](http://www.omdbapi.com/)

The  [omdbapi](http://www.omdbapi.com/)  is an open and free movie database API which will provide the movie details and images too. The main drawback is that most images are not very clear, but it will do the trick. Also API support is there.

In order to use this API, first of all, need to signup and they will provide an API key sent to you via mail. This can be used for each query result.

Passing key and also the special string is needed. s stands for search when passing **_s=”Indiana”_**, API will retrieve all data contains Indiana. Also, **_i_** stands for a movie with imbd id will be returned, so only one is returned since it is unique. We are using “**_s”_**  and **_“i”_** here for the demo.

# 4. Calling and testing API and Test

In order to check what we will receive when calling the omdbapi is by testing with postman tool or any API test mechanism. Here I am using the postman for this.



![](https://miro.medium.com/max/968/1*Qz8IqTSZQG3z45WeI6yGhg.png)

As you see in the image, need to pass the apikey=XXXX and the s=”movie-name”

So the URL becomes

> [http://www.omdbapi.com/?s=movie-name&apikey=XXXX&page=1&type=movie&Content-Type=application/json](http://www.omdbapi.com/?s=indiana&apikey=b76b385c&page=1&type=movie&Content-Type=application/json)

Awesome, we are good, now we can proceed to create an app and work on the axios as well.

# 5. Create an App

Create a Vue js application is done by a simple command
``` js
vue create movie-app
``` 
movie-app is our app name.

![](https://miro.medium.com/max/30/1*_GRlYMIq2PIy9lt-dzKlyQ.png?q=20)

![](https://miro.medium.com/max/1245/1*_GRlYMIq2PIy9lt-dzKlyQ.png)

# 6. Requirement and structure of the App

The structure of the app have 3 components.

1.  LatestMovie component.
2.  Movie Component.
3.  SearchMovie component.

LatestMovie component will have the current home page and I will display the movies related to my favorite movie “indiana”

On clicking on each movie, will display details of every single movie, Which can be done by using the Movie component.

Provided an option to search and display those movies, which can be handled by SearchMovie component.

# 7. Add Vuetify to the Project

As already discussed, we are using the Vuetify for the desgin of the App. Need to do some groundwork for that. on the terminal, type
``` 
vue add vuetify
``` 
![](https://miro.medium.com/max/30/1*Rs1pFRTIeysNQhdE5_UUNA.png?q=20)

![](https://miro.medium.com/max/1205/1*Rs1pFRTIeysNQhdE5_UUNA.png)

After installation, our front end will look like this:

![](https://miro.medium.com/max/30/1*93-wXWbEjhE_91NU_7cyMg.png?q=20)

![](https://miro.medium.com/max/1277/1*93-wXWbEjhE_91NU_7cyMg.png)

Awesome right, they provide a nav bar also. Then will proceed.

# 8. Add vue-router to the project

Will explain why we needed the vue-router, it will do the routing functionalities and component switching without hassle. Installing the vue-router is by
``` 
npm install vue-router
``` 
![](https://miro.medium.com/max/30/1*E9nzhzWCiJ2IuX9gghviRQ.png?q=20)

![](https://miro.medium.com/max/316/1*E9nzhzWCiJ2IuX9gghviRQ.png)

now, need to link the router to the application and create a routes file.

1.  Create a router file
2.  Add content to the router file
3.  Link the router to the app

**_1.Create a router file_**

I am following a pattern by which create a folder called  **_router_**  in the src path and in that, will create an  **_index.js_** file

![](https://miro.medium.com/max/30/1*2hVB5zeLxC01sqkgkjXiqg.png?q=20)

![](https://miro.medium.com/max/230/1*2hVB5zeLxC01sqkgkjXiqg.png)

**_2. Add content to the router file_**

So far, we created a router/index.js file now need to import the Vue instance and vue-router to that file also, need to export the default router file.

Each router path will have 3 components:  **_path, name, component._**
``` javascript
import Vue from 'vue'  
import VueRouter from 'vue-router'Vue.use(VueRouter)export default new VueRouter({  
  routes: [  
    {  
    }  
  ]  
})
``` 
**_3. Link the router to the app_**

First, need to import the router from the path, and use that in the Vue instance. All these are done in the src/main.js file
``` 
import router from ‘./router’
``` 
Current main.js file will look like this:
``` js
import Vue from 'vue'  
import './plugins/vuetify'  
import App from './App.vue'  
import router from './router'Vue.config.productionTip = false  
new Vue({  
  render: h => h(App),  
  router  
}).$mount('#app')
``` 
# 9. Add axios to the project

Axios is our point of contact to call the API services in this app. Now we need to install axios to our project.
``` js
npm install axios --save
``` 
![](https://miro.medium.com/max/30/1*peus5peqmkliaK4Tw1MEEw.png?q=20)

![](https://miro.medium.com/max/668/1*peus5peqmkliaK4Tw1MEEw.png)

# 10. Remove the currently scaffolded component

By default, we are having a component in place, will remove that and will create the components we needed.

HelloWorld.vue is the default component, will remove that from our app.

# 11. Create LatestMovie component

Need to do some steps here

1.  Create the LatestMovie.vue.
2.  Add the axios to the LatestMovie component.
3.  Link the router to LatestMovie.
4.  Add a progress bar for LatestMovie.
5.  **_Create the LatestMovie.vue._**

Create a file called  **_LatestMovie.vue_** in components folder.

**_2. Add the axios to the LatestMovie component._**

Here, we are using the mounted() life cycle for this, added the code to get the result from the omdbapi with the indiana movie data.
``` js
mounted () {  
  axios  
    .get('[http://www.omdbapi.com/?s=mummy&apikey=XXXXX&page=1&type=movie&Content-Type=application/json'](http://www.omdbapi.com/?s=mummy&apikey=b76b385c&page=1&type=movie&Content-Type=application/json%27))  
    .then(response => {  
      this.wholeResponse = response.data.Search  
    })  
    .catch(error => {  
      console.log(error)  
    })  
}
``` 
**_3. Link the router to LatestMovie._**

Now, we need to link the  **_LatestMovie_**  to the router file.

in the src/router/index.js:

import LatestMovie from '@/components/LatestMovie'

add the links to the **router/index.js:**
``` js
export default new VueRouter({  
  routes: [  
   {  
      path: '/',  
      name: 'LatestMovie',  
      component: LatestMovie  
    }  
  ]  
})
``` 
**_4. Add a progress bar for LatestMovie_**

If the API will take time to retrieve, we will need to display a progress bar. This can be achieved by using the  _“ <v-progress-circular”_ from vuetify.

Created a data property which will be set to true initially, then after the API response will be set to false.

Also another data property called wholeResponse will take care of the data.

So totally our  **_LatestMovie.vue_** becomes:
``` js
<template><v-container v-if="loading">  
    <div class="text-xs-center">  
      <v-progress-circular  
        indeterminate  
        :size="150"  
        :width="8"  
        color="green">  
      </v-progress-circular>  
    </div>  
  </v-container><v-container v-else grid-list-xl>  
    <v-layout wrap>  
      <v-flex xs4  
        v-for="(item, index) in wholeResponse"  
        :key="index"  
        mb-2>  
        <v-card>  
          <v-img  
            :src="item.Poster"  
            aspect-ratio="1"  
          ></v-img><v-card-title primary-title>  
            <div>  
              <h2>{{item.Title}}</h2>  
              <div>Year: {{item.Year}}</div>  
              <div>Type: {{item.Type}}</div>  
              <div>IMDB-id: {{item.imdbID}}</div>  
            </div>  
          </v-card-title><v-card-actions class="justify-center">  
            <v-btn flat  
              color="green"  
              [@click](http://twitter.com/click)="singleMovie(item.imdbID)"  
              >View</v-btn>  
          </v-card-actions></v-card>  
      </v-flex>  
  </v-layout>  
  </v-container>  
</template><script>  
import axios from 'axios'  
export default {  
  data () {  
    return {  
      wholeResponse: [],  
      loading: true  
    }  
  },  
  mounted () {  
  axios  
    .get('[http://www.omdbapi.com/?s=indiana&apikey=XXXX&page=1&type=movie&Content-Type=application/json'](http://www.omdbapi.com/?s=indiana&apikey=XXXX&page=1&type=movie&Content-Type=application/json%27))  
    .then(response => {  
      this.wholeResponse = response.data.Search  
      this.loading = false  
    })  
    .catch(error => {  
      console.log(error)  
    })  
  }  
}  
</script><style lang="stylus" scoped>  
  .v-progress-circular  
    margin: 1rem  
</style>

Now, add the router-view to the App.vue to display the component:

<router-view></router-view>
``` 
# 12. Implement Movie Component

Now, it is the time for the single movie part. This can be achieved by using the Movie.vue file.

1.  Add the Movie.vue file
2.  Add the router
3.  Add the mode
4.  Pass the props in a router.
5.  Pass the props in latest component.
6.  Work on the props data in the movie component.

**_Add the Movie.vue file_**

Add the file in components/Movie.vue

**_Add the router_**

Register the Movie.vue to the router/index.js file

import Movie from '@/components/Movie'

**_Add the mode_**

There is “#” is there in the URL, we can remove those using the

mode: history

In the router/index.js file.

**_Pass the props in a router._**

Create a path for the Movie.vue component, using the below code in the **router/index.js**
``` js
{  
      path: '/movie/:id',  
      name: 'Movie',  
      props: true,  
      component: Movie  
    },
``` 
We are giving props: true because we are passing the imdb_id to the Movie.vue component then that value is used to call the API for that single movie.

**_Pass the props in latest component_**

Now up on clicking on the view in the LatestMovie, will call the method which will, in turn, pass the imdb_id as a props to the Movie.vue.
``` js
<v-btn round  
              color="green"  
              [@click](http://twitter.com/click)="singleMovie(item.imdbID)"  
              >View</v-btn>
``` 
and the singleMovie method is
``` js
methods: {  
    singleMovie (id) {  
      this.$router.push('/movie/' + id)  
    }  
  }
``` 
**_Work on the props data in the movie component_**

Now, the data is passed from the LatestMovie. That value is received as prop in the Movie.vue component. This value can be used by _this.id_

Also, added a data property called singleMovie to handle the response.

The code in the Movie.vue becomes,
``` js
<template>  
  <v-container>  
    <v-layout row wrap>  
      <v-flex xs12>  
        <h2>welcome to single movie component</h2>  
          <div>{{singleMovie}}</div>  
      </v-flex>  
    </v-layout>  
  </v-container>  
</template><script>  
import axios from 'axios'  
export default {  
  props: ['id'],  
  data () {  
    return {  
      singleMovie: ''  
    }  
  },  
  mounted () {  
    axios  
      .get('[http://www.omdbapi.com/?apikey=b76b385c&i=XXXXX&Content-Type=application/json'](http://www.omdbapi.com/?apikey=b76b385c&i=tt0209163&Content-Type=application/json%27))  
      .then(response => {  
        this.singleMovie = response.data  
      })  
      .catch(error => {  
        console.log(error)  
      })  
  }  
}  
</script><style>  
</style>
``` 
# 13. Display the ratings

The omdbapi will provide us the current ratings for the movie. We will display that value in the table,

![](https://miro.medium.com/max/30/1*okaLcvRTXsW2znGn-t7Ugg.png?q=20)

![](https://miro.medium.com/max/667/1*okaLcvRTXsW2znGn-t7Ugg.png)

For that, will display using a modal, which will be invoked on clicking the view rating button.
``` js
<template>  
<v-layout row wrap>  
      <v-flex xs12>  
        <div class="text-xs-center">  
        <v-dialog  
          v-model="dialog"  
          width="500">  
          <v-btn  
            slot="activator"  
            color="green"  
            dark>  
            View Ratings  
          </v-btn>  
          <v-card>  
            <v-card-title  
              class="headline grey lighten-2"  
              primary-title  
            >  
              Ratings  
            </v-card-title>  
            <v-card-text>  
              <table style="width:100%" border="1" >  
                <tr>  
                  <th>Source</th>  
                  <th>Ratings</th>  
                </tr>  
                <tr v-for="(rating,index) in this.ratings" :key="index">  
                  <td align="center">{{ratings[index].Source}}</td>  
                  <td align="center">{{ratings[index].Value}}</td>  
                </tr>  
              </table>  
            </v-card-text>  
            <v-divider></v-divider>  
            <v-card-actions>  
              <v-spacer></v-spacer>  
              <v-btn  
                color="primary"  
                flat  
                [@click](http://twitter.com/click)="dialog = false"  
              >  
                OK  
              </v-btn>  
            </v-card-actions>  
          </v-card>  
        </v-dialog>  
      </div>  
      </v-flex>  
    </v-layout>  
  </template>
``` 
We are iterating a data value called ratings. This data property is from a response from API ie r_esponse.data.Ratings._

# 14. Add Search Movie component

For this, we need to create the following:

1.  Create a SearchMovie.vue file
2.  Create a text field in the App.vue.
3.  On clicking the search button, will pass the data from the text field to the SearchMovie.vue file as prop.
4.  In SearchMovie.vue file, we will receive the value and call the API to get the data.

[commit link for this](https://github.com/anoobbava/movie-app/commit/1212477d5c4fdb25b0a3ba999f1ca6429e646fec)

# 15. An issue with search movie and how we can rectify it

Currently mounted lifecycle hook is called only one time, when we search for one time, it displays the data, ie when searched with iron man, it shows the data. but After searching with “titan”, It shows the same data. This can be fixed by using the watch property on the props of the data called name(from the App.vue) and updated the mounted property as a method. As a result, the system will call 2 times, ie when the first loaded by the mounted lifecycle hook and again search will be handled by the watcher action for the props(name) value.

![](https://miro.medium.com/max/30/1*zCH_0IVgw8MntbHXnusw9Q.png?q=20)

![](https://miro.medium.com/max/1241/1*zCH_0IVgw8MntbHXnusw9Q.png)

![](https://miro.medium.com/max/30/1*WnkGWlNwwevk9kAeFFQX7A.png?q=20)

![](https://miro.medium.com/max/1254/1*WnkGWlNwwevk9kAeFFQX7A.png)

t**he issue, we are searching for Titan, but we got iron man**

[commit link for the fix](https://github.com/anoobbava/movie-app/commit/706d81167bf948db62ff63afdb5ff5f2ee197734)

# 16. Add a warning message if there is no search data in the API

Suppose, when we are calling for the API with invalid movie or movie that is not available in our omdbapi . In that case, need to display a message.

We are creating a data property by default which is false, when searched data is not returning anything, will set as true and it will display the message.

![](https://miro.medium.com/max/30/1*_B2SmVA0_LbpNqQFlbQ7xg.png?q=20)

![](https://miro.medium.com/max/1266/1*_B2SmVA0_LbpNqQFlbQ7xg.png)

[commit link for the code change](https://github.com/anoobbava/movie-app/commit/20625f2b3b9d6283fe6b43bca6f652f085673af4)

# 17. Creating a central file for axios/refactoring

Still, our axios and API calling codes are scattered everywhere in the component. It will good if we place those all in a single place like services in angular.

For that

1.  Create a folder named services in src/ and create a file MovieApi.js
2.  Import the axios in the main.js
3.  Create a default URL in the main.js
4.  Export the MovieApi.js file
5.  Import the MovieApi.js in the components.
6.  Remove the axios code from the components and place in the MovieApi.js file.
7.  Call the appropriate methods from components.

[commit link for the code change](https://github.com/anoobbava/movie-app/commit/4f1638136ebdf9d7d5b98190d678936bb185ddc0)

# 18. Wrapping Up and source code

Our final output will be this:

![](https://miro.medium.com/max/30/1*hii3QStv4XyzXlL2fFpU-w.png?q=20)

![](https://miro.medium.com/max/1273/1*hii3QStv4XyzXlL2fFpU-w.png)

LatestMovie component.

![](https://miro.medium.com/max/30/1*oxTNq1V6B3t-OGhiD0lN8Q.png?q=20)

![](https://miro.medium.com/max/1272/1*oxTNq1V6B3t-OGhiD0lN8Q.png)

searchMovie.vue

![](https://miro.medium.com/max/30/1*6eUr_CW1OxES0OAXDBe7SA.png?q=20)

![](https://miro.medium.com/max/1256/1*6eUr_CW1OxES0OAXDBe7SA.png)

Movie.vue

[**GitHub URL**](https://github.com/anoobbava/movie-app)

# And there we have it!

I hope you have enjoyed following along. Please leave claps and comments if you liked the content and would like to discuss further!
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1OTI2NjUwLDE4OTE1MzkyMTddfQ==
-->