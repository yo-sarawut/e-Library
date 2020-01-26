Vue.js (and Vuex) bug squasher cheatsheet
===
[Source:](https://blog.usejournal.com/vue-js-and-vuex-bug-squasher-cheatsheet-50d4cccd8f79)

![enter image description here](https://miro.medium.com/max/1920/1*QzA0HAalTxc7SFbVRiHAyQ.png)

_Recently I have been writing a lot of Vue, and it happens every so often that i make the same mistakes, then it takes me 10–15 minutes to find out why it isn’t working, so I made this cheatsheet for_ **_us_**_. I hope this helps you in some way. If you have any suggestions for more common bugs, please leave a comment so I can make this article better._

## 1. v-show on template

When you are using  **v-show**, Vue is changing the CSS  **display**  property. the template tag in Vue does not actually create an element, so if you try to use v-show, nothing will happen since Vue does not have an element to target.

**solution**  
use  **v-if** on the template tag or change the template tag into an element (div, section, etc).

## example


![](https://miro.medium.com/max/1620/1*j_WSnO7Bx0fWfX83JPphSg.png)

----------

## 2. Why is the ref element undefined?

Most likely you are trying to access an element that is not being rendered due to being nested somewhere within an ancestor element that has v-if directive that evaluates to false.

**solution**

1.  Change the  **v-if**  to  **v-show**
2.  Wait until the  **v-if evaluates to true,** then access and start using the ref element.

## example

![](https://miro.medium.com/max/30/1*9-_-bxs10ekd1cncP5fT7g.png?q=20)

![](https://miro.medium.com/max/1620/1*9-_-bxs10ekd1cncP5fT7g.png)

----------

## 3. Are you targeting the correct property: Updating a property in Vuex state

When your Vue application starts to become more complex, and you have things that are named similarly, and perhaps more nesting than is healthy in your data structures, it can be easy to target the incorrect property when you are mutating the state.

**solution**

1.  Better naming
2.  Try to avoid nesting unless it is necessary or suits the situation and double
3.  check if the path to the property is correct.

## example

In my app the Vuex store module was named  **user**, then there were properties like  **loggedIn**,  **token**  and so on. and then also a property called  **user**  containing the actual data. When I was importing the module into other modules and i wanted to access the name, it would be  **user.state.user.name**, many times i simply just ended up typing  **user.name**. The two property names were essentially fighting for the same mental ram in my head.

----------

## Join the Vue Community

I am creating a community of Vue fans, it will be free for the first 20 people. But after that it will have a fee of about $20. Why? To ensure that only people that are serious about Vue join. There are still some spots available,  [join now!](https://vue-community.com/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAwMDQzMzYxLDI1Nzc0MzcwMF19
-->