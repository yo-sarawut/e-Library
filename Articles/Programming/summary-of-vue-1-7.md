Summary of VueJS by Sarah Drasner (Part 1 of 7: Directives & Data Rendering)
===

_[JL’s Self-teaching Story] Series_

[_Net Ninja_] [JS Regular Expressions](http://bit.ly/M_JS_RE_NN)  
[_Net Ninja_] Vue JS2 ([Part1](http://bit.ly/M_VueJS2_NN_1_of_3), [Part2](http://bit.ly/M_VueJS2_NN_2_of_3), [Part3](http://bit.ly/M_VueJS2_NN_3_of_3))  
[_Net Ninja_] [Vuex](http://bit.ly/M_Vuex_NN)  
[_Net Ninja_] Python3 ([Part1](http://bit.ly/M_Python3_NN_1_of_3), [Part2](http://bit.ly/M_Python3_NN_2_of_3), [Part3](http://bit.ly/M_Python3_NN_3_of_3))  
[_Net Ninja_] Django ([Part1](http://bit.ly/M_Django_NN_1_of_3), [Part2](http://bit.ly/M_Django_NN_2_of_3), [Part3](http://bit.ly/M_Django_NN_3_of_3))  
[_Net Ninja_] Sass ([Part1](http://bit.ly/M_Sass_NN_1_of_2), [Part2](http://bit.ly/M_Sass_NN_2_of_2))  
[_Sean Larkin_] Webpack4 ([Part1](http://bit.ly/M_Webpack4_SL_1_of_4), [Part2](http://bit.ly/M_Webpack4_SL_2_of_4), [Part3](http://bit.ly/M_Webpack4_SL_3_of_4), [Part4](http://bit.ly/M_Webpack4_SL_4_of_4))[_Sarah Drasner_] VueJS (**Part1(_current_)**, [Part2](http://bit.ly/M_Vue_SD_2_of_7), [Part3](http://bit.ly/M_Vue_SD_3_of_7), [Part4](http://bit.ly/M_Vue_SD_4_of_7),   
                       [Part5](http://bit.ly/M_Vue_SD_5_of_7), [Part6](http://bit.ly/M_Vue_SD_6_of_7), [Part7](http://bit.ly/M_Vue_SD_7_of_7))

----------

🌲 This is the  **first**  part of my summary of Sarah Drasner’s “[Introduction to Vue.js](https://frontendmasters.com/courses/vue/)” on  [FrontendMasters](https://frontendmasters.com/). GitHub page can be accessed  [here](https://github.com/sdras/intro-to-vue). (_You can also check out her_ [_blog post_](https://css-tricks.com/intro-to-vue-1-rendering-directives-events/) _on CSS-Tricks “Intro to Vue.js: Rendering, Directives, & Events._)

----------

[1. Directives & Data Rendering]  
    1-1. Vue Instance  
    1-2. Comparing Vanilla JS  
    1-3. Directives  
    1-4. Challenge 1: Calculator

----------

I created a Vue dev environment by using  **Webpack**  and  `vue-loader`  through  `[Vue CLI 3](https://cli.vuejs.org/)`  and set up  **Vuex**,  **Routing**, and  **Sass**(_CSS Preprocessor_).

This part is not covered in this tutorial. If you’d like to know how I did that, please check  [this](http://bit.ly/M_Sass_NN_1_of_2)  out.

![](https://miro.medium.com/max/30/1*ATrLhNypWAhi9nWik-F2KA.png?q=20)

![](https://miro.medium.com/max/499/1*ATrLhNypWAhi9nWik-F2KA.png)

![](https://miro.medium.com/max/30/1*_x-ac519Up9de07oE9sgcQ.png?q=20)

![](https://miro.medium.com/max/497/1*_x-ac519Up9de07oE9sgcQ.png)

----------

# [ 1–1. Vue Instance ]

[src > components > examples > example1.vue]  
<template>  
  <div id="**_app_**">  
    **{{ text }}** Nice to meet Vue.  
  </div>  
</template><script>  
export default{   
  _data()_{  
    return{  
      **text: 'Hello Class!'**  
    }  
  }  
}  
</script><style scoped>  
**_#app_** {  
  text-align: center;  
  padding: 70px;  
  font-size: 22px;  
  max-width: 360px;  
  margin: 0 auto;  
  display: table;  
}  
</style>

> _Available to see the full code with_ **syntax highlighting** _on_ [_GitHubGist_](http://bit.ly/GHG_SD_Vue_0)_._

----------

# [ 1–2 Comparing Vanilla JS ]

## #1 Vanilla JS

[_JavaScript file_]  
const items = ['A', 'B', 'C', 'D'];function listOfStuff(){  
  let full_list='';  
  for(let i=0; i<items.length; i++){  
    full_list = full_list + '<li> **${items[i]}** </li>'  
  }  
  const contain = document.**_querySelector_**('#container');  
  contain.**_innerHTML_** = '<ul> **${full_list}** </ul>';  
}listOfStuff();  
-----------------------------------[_HTML file_]  
<div id='container'></div>

-   “A  **_template literal_**(`**${}**`) is a way to concatenate strings while allowing embedded expressions and improving readability” ([CodeBurst.io](https://codeburst.io/javascript-what-are-template-literals-5d08a50ef2e3); more examples on  [Medium](https://medium.com/front-end-hacking/es6-cool-stuffs-a-new-js-string-with-template-literals-c23a8af11b2)).
-   “The  `[Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)`  method  `**querySelector()**`  returns the first  `[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)`  within the document that matches the specified selector, or group of selectors” ([MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)).
-   “The  `[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)`  property  `**innerHTML**`  gets or sets the HTML or XML markup contained within the element” ([MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)).

## #2 Vue

[src > components > examples > example2.vue]  
<template>  
  <div id="**_app_**">  
    <ul>  
      <li v-for="_item_ in **items**" v-bind:key='_item_.id'>  
        **{{** _item_ **}}**  
      </li>  
    </ul>  
  </div>  
</template><script>  
export default{   
  _data()_{  
    return{  
      **items**: ['A', 'B', 'C', 'D']  
    }  
  }  
}  
</script>

> clean, semantic, declarative, legible, easy to maintain, reactive

----------

# [ 1–3. Directives ]

“A directive is some special token in the markup that tells the library to do something to a DOM element” ([Official Website](https://012.vuejs.org/guide/directives.html)).

## 1–3–1.  `[v-for](https://vuejs.org/v2/api/#v-for)`

> Loops through a set of values / can also do a static number

## 1–3–2.  `[v-model](https://vuejs.org/v2/api/#v-model)`

> Creates a relationship b/t the data in the instance/component and a form input, so, you can dynamically update values

**Example #1**

**Example #2**

`**v-model**` **Modifiers**:

-   `v-model._trim_`  will strip any leading or trailing whitespace from the bound string.
-   `v-model._number_`  changes strings to number inputs.
-   `v-model._lazy_`  won’t populate the content automatically, it will wait to bind until an event happens. (_It listens to change events instead of input_)

----------

## 1–3–3.  `[v-if](https://vuejs.org/v2/api/#v-if)`

> A conditional that will display information depending on meeting a requirement. (This can be anything: buttons, forms, divs, and components.)

Let’s look at the DOM. I ran my file on a development server.

> I created a Vue dev environment by using  **webpack**  and  `_vue-loader_`  through  `[_Vue CLI 3_](https://cli.vuejs.org/)`  and set up  **Vuex**,  **Routing**, and  **Sass**(_CSS Preprocessor_).
> 
> This part is not covered in this tutorial. If you’d like to know how I did that, please check  [this](http://bit.ly/M_Sass_NN_1_of_2)  out.

When we use  `v-if`, we have an empty comment:  `<!-- -->`

![](https://miro.medium.com/max/24/1*Z-fiIhFE4GzXTPXdA3hAnQ.png?q=20)

![](https://miro.medium.com/max/519/1*Z-fiIhFE4GzXTPXdA3hAnQ.png)

[v-if] When the text box is empty

When a text is entered, a red button shows up.

![](https://miro.medium.com/max/26/1*gKxNqOFkb4T2b8_j9Zfgzg.png?q=20)

![](https://miro.medium.com/max/545/1*gKxNqOFkb4T2b8_j9Zfgzg.png)

[v-if] When the text box is NOT empty

>  `v-if`  literally  _unmount_  the element from the DOM and  _remount_  it into the DOM. The code does NOT exist when a text is not entered in the text box.

----------

## 1–3–4.  `[v-show](https://vuejs.org/v2/api/#v-show)`

> `_v-show_`  has the same functionality with v-if. But,  `_v-show_`  does NOT  _unmount_the element from the DOM.  `_v-show_`  just toggles its visibility for us.

When we use  `v-show`,  `style=”display: none”`  is applied on a button.

![](https://miro.medium.com/max/29/1*wh1TCYpT0vudjFuoII-abQ.png?q=20)

![](https://miro.medium.com/max/606/1*wh1TCYpT0vudjFuoII-abQ.png)

[v-show] When the text box is empty

When a text is entered, a red button shows up.

![](https://miro.medium.com/max/29/1*Des05Qdu0aTgpCveqQZKLw.png?q=20)

![](https://miro.medium.com/max/591/1*Des05Qdu0aTgpCveqQZKLw.png)

[v-show] When the text box is NOT empty

If you have a user content where you know users will click it and make it appear or disappear a lot, you’d want to use  `v-show`  to minimize the work to show the element.

But, if you have a full template or component only shown in a specific circumstance, your load time will be much smaller initially. The reason is that you don’t have to load out that content, and then display “none”. So, that’s a good time to use  `v-if`.

----------

## 1–3–5.  `[v-if](https://vuejs.org/v2/api/#v-if)`  /  `[v-else](https://vuejs.org/v2/api/#v-else)`  /  `[v-else-if](https://vuejs.org/v2/api/#v-else-if)`

> Pretty straightforward: you can conditionally render one thing or another.

> We can toggle between the two conditions.

----------

## 1–3–6.  `[v-bind](https://vuejs.org/v2/api/#v-bind)`  or  `:(colon)`

> One of the most useful directives! (`_:_`  is a shortcut of  `_v-bind_`) We can use it for so many things including class & style binding, creating dynamic props, etc.

-   The button is in the DOM. It’s either in an active state or inactive state.
-   `[tacos ? activeClass : ‘’]`: ternary operators are really useful in directives (_You can’t write longer functions in directives, though. We’ll use methods for that_).

----------

## 1–3–7.  `[v-once](https://vuejs.org/v2/api/#v-pre)`  &  `[v-pre](https://vuejs.org/v2/api/#v-pre)`

> `_v-once_`  is not quite useful. It will not update once it’s been rendered.
> 
> `_v-pre_` is a little bit more useful. It will print out the inner text exactly how it is including code (good for documentation and debugging).

> If you’ve worked with React before, it’s similar to debugging with JSON stringify.

----------

## 1–3–8.  `[v-on](https://vuejs.org/v2/api/#v-on)`  or  `@`

> Extremely useful! (`_@_`  is a shortcut of  `_v-on_`) It’s great for binding to events like  [mouse-enter, mouse-over](https://bl.ocks.org/mbostock/5247027), and click. You’ll be able to pass in a parameter for the event like (e). We can also use ternaries directly.

We can also do  _multiple_  bindings like the following:

<div @="click: onClick, keyup: onKeyup, keydown: onKeydown"></div>

`**v-on**` **Modifiers**:

-   `@mousemove._stop_`  is comparable to  `[e.stopPropogation()](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation)`, which keeps the event from bubbling any further up into the DOM.
-   `@mousemove._prevent_`  is comparable  `[e.preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)`, which can keep a form from re-submitting.
-   `@submit._prevent_`  will no longer reload the page on submission.
-   `@click._once_`  will be triggered once. You can use it when you want to disable a click right after it fires. (_Don’t be confused with_ `_v-once_`_._)
-   `@click._native_`  allows you to listen to native events in the DOM.

> There are keycodes available to you, but you can also configure your own.

----------

## 1–3–9.  `[v-html](https://vuejs.org/v2/api/#v-html)`

> Great for strings that have html elements that need to be rendered

-   Not same as templates: inserted as plain HTML
-   Don’t use on user-rendered content, because it’s a security issue. Data can be hacked through cross(**X**)-**S**ite  **S**cripting (**XSS**) attacks.

----------

## 1–3–10.  `[v-text](https://vuejs.org/v2/api/#v-text)`

> Similar to using mustache templates

> If you’d like to dynamically update, it’s recommended to use mustache templates instead.

----------

![](https://miro.medium.com/max/30/1*KE4TcC7zLrHEs-DtnQymmQ.png?q=20)

![](https://miro.medium.com/max/751/1*KE4TcC7zLrHEs-DtnQymmQ.png)

Copyright ©️ Sarah Drasner at  [CSS-Tricks](https://css-tricks.com/intro-to-vue-1-rendering-directives-events/)

![](https://miro.medium.com/max/30/1*zVu2ErXrxMPkmRcJvA0kaw.png?q=20)

![](https://miro.medium.com/max/750/1*zVu2ErXrxMPkmRcJvA0kaw.png)

Copyright ©️ Sarah Drasner at  [CSS-Tricks](https://css-tricks.com/intro-to-vue-1-rendering-directives-events/)

> Detailed explanation can be found at CSS-tricks  [Vue Guide](https://css-tricks.com/guides/vue/).

----------

# [ 1–4. Challenge 1: Calculator ]

## Template:

## Solution:

> My GitHub Repository can be found at  [https://github.com/hlim18/JLbootcamp](https://github.com/hlim18/JLbootcamp). Click “**Branch**” — “**class-02-ch-01–04**” or  [this link](https://github.com/hlim18/JLbootcamp/tree/class-02-ch-01%E2%80%9304).

----------

Class instructor “Sarah Drasner” is an award-winning Speaker, Senior Developer Advocate at  [**Microsoft**](https://www.microsoft.com/), and Staff Writer at  [**CSS-Tricks**](https://css-tricks.com/). She’s a  [**Vue**](https://vuejs.org/)Core team member.

She can be found at  [her personal website](https://sarahdrasnerdesign.com/),  [GitHub](https://github.com/sdras),  [CSS-Tricks](https://css-tricks.com/author/sdrasner/),  [CodePen](https://codepen.io/sdras/),  [LinkedIn](https://www.linkedin.com/in/sarahdrasner/),  [Twitter](https://twitter.com/sarah_edo), and Medium([Sarah Drasner](https://medium.com/u/c2509fce86ff?source=post_page-----30103729ec9b----------------------)), and  [Frontend Masters](https://frontendmasters.com/teachers/sarah-drasner/).

----------

Thanks for reading! 💕  _If you like this blog post, please clap👏_
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNTQ2NTIwMTVdfQ==
-->