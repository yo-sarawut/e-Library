

# How to Use Pure CSS to Create a Beautiful Loading Animation for your App

![](https://gblobscdn.gitbook.com/assets%2F-M16IoaANYRvc0I-U9uw%2F-M6k8kptFV8QwhuYRNWJ%2F-M6k9-BXarb6RyvdYSqa%2Fimage.png?alt=media&token=5751672b-9b65-41b3-bb84-a87e96396aea)



‌

Some of the social giants like Facebook even use this approach to give page loading a better experience. How can we do that with just some simple CSS?

-   [What are we going to build?](https://www.freecodecamp.org/news/how-to-use-css-to-create-a-beautiful-loading-animation-for-your-app/#what-are-we-going-to-build)
-   [Just want the snippet?](https://www.freecodecamp.org/news/how-to-use-css-to-create-a-beautiful-loading-animation-for-your-app/#just-want-the-snippet)
-   [Part 1: Creating our loading animation](https://www.freecodecamp.org/news/how-to-use-css-to-create-a-beautiful-loading-animation-for-your-app/#part-1-creating-our-loading-animation)
-   [Part 2: Using our loading animation in a dynamic app](https://www.freecodecamp.org/news/how-to-use-css-to-create-a-beautiful-loading-animation-for-your-app/#part-2-using-our-loading-animation-in-a-dynamic-app)

## What are we going to build?

We're going to create a loading animation using a CSS class that you can apply to pretty much any element you want (within reason).

![](https://www.freecodecamp.org/news/content/images/2020/05/loading-animation.gif)

Loading animation preview

This gives you great flexibility to use it and makes the solution nice and simple with only CSS.

While the snippet is pretty small and you could just copy and paste it, I'll walk you through what's happening and an example of using it dynamically when loading data.

## Just want the snippet?

You can grab it here!

[](https://gist.github.com/colbyfayock/d155418975d1e0e04b2805e285296033)

CSS Loading Animation

CSS Loading Animation. GitHub Gist: instantly share code, notes, and snippets.

![](https://github.githubassets.com/favicons/favicon.svg)262588213843476Gist

![](https://github.githubassets.com/images/modules/gists/gist-og-image.png)

## Do I need to know how to animate before this tutorial?

No! We'll walk through in detail exactly what you need to do. In fact, the animation in this tutorial is relatively simple, so let's dig in!

## Part 1: Creating our loading animation

This first part is going to focus on getting the loading animation together and seeing it on a static HTML website. The goal is to walk through actually creating the snippet. We'll only use HTML and CSS for this part.

### Step 1: Creating some sample content

To get started, we'll want a little sample content. There's really no restrictions here, you can create this with basic HTML and CSS or you can add this to your Create React App!

For the walk through, I'm going to use HTML and CSS with a few examples of content that will allow us to see this in effect.

To get started, create a new HTML file. Inside that HTML file, fill it with some content that will give us the ability to play with our animation. I'm going to use  [fillerama](http://fillerama.io/)  which uses lines from my favorite TV show  [Futurama](https://en.wikipedia.org/wiki/Futurama)!

![](https://www.freecodecamp.org/news/content/images/2020/05/static-html-css-website-fillerama.jpg)

Static HTML & CSS webpage with content from fillerama.io

If you're going to follow along with me, here's what my project looks like:

```
my-css-loading-animation-static
- index.html
- main.css

```

[Follow along with the commit!](https://github.com/colbyfayock/my-css-loading-animation-static/commit/9aa7925f7048fa1b73fef74d0d56380c29fc5d73)

### Step 2: Starting with a foundation loading class

For our foundation, let's create a new CSS class. Inside our CSS file, let's add:

```css
.loading {
  background: #eceff1;
}

```

With that class, let's add it to a few or all of our elements. I added it to a few paragraphs, headings, and lists.

```html
<p class="loading">For example...

```

![](https://www.freecodecamp.org/news/content/images/2020/05/static-html-css-gray-background.jpg)

Static HTML & CSS webpage with a gray background for the content

That gives us a basic background, but we'd probably want to hide that text. When it's loading, we won't have that text yet, so most likely we would want to use filler text or a fixed height. Either way, we can set the color to transparent:

```css
.loading {
  color: transparent;
  background: #eceff1;
}

```

![](https://www.freecodecamp.org/news/content/images/2020/05/static-html-css-gray-background-hidden-text.jpg)

Static HTML & CSS webpage with a gray background and transparent color for the content

If you notice with list elements, whether you apply the class to the top level list element (`<ol>`  or  `<ul>`) vs the list item itself (`<li>`), it looks like one big block. If we add a little margin to the bottom of all list elements, we can see a different in how they display:

```css
li {
  margin-bottom: .5em;
}

```

![](https://www.freecodecamp.org/news/content/images/2020/05/static-html-css-gray-background-different-lists.jpg)

Style difference between applying to the top level list or the list items

And now it's starting to come together, but it kind of just looks like placeholders. So let's animate this to look like it's actually loading.

[Follow along with the commit!](https://github.com/colbyfayock/my-css-loading-animation-static/commit/f68cdef36be11311a5cc11a1d39e52ea7e7bb48d)

### Step 3: Styling and animating our loading class

Before actually animating our class, we need something to animate, so let's add a gradient to our  `.loading`  class:

```css
.loading {
  color: transparent;
  background: linear-gradient(100deg, #eceff1 30%, #f6f7f8 50%, #eceff1 70%);
}

```

This is saying that we want a  [linear gradient](https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient)  that's tilted at 100 degrees, where we start with  `#eceff1`  and fade to  `#f6f7f8`  at 30% and back to  `#eceff1`  at 70%;

![](https://www.freecodecamp.org/news/content/images/2020/05/static-html-css-gray-background-subtle-gradient.jpg)

Subtle gradient background that might look like a glare

It's hard to see initially when it's still, it might just look like a glare on your computer! If you'd like to see it before moving on, feel free to play with the colors above to see the gradient.

Now that we have something to animate, we'll first need to create a  [keyframes](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes)  rule:

```css
@keyframes loading {
  0% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0 50%;
  }
}

```

This rule when applied will change the background position from starting at 100% of the x-axis to 0% of the x-axis.

With the rule, we can add our  [animation](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)  property to our  `.loading`  class:

```css
.loading {
  color: transparent;
  background: linear-gradient(100deg, #eceff1 30%, #f6f7f8 50%, #eceff1 70%);
  animation: loading 1.2s ease-in-out infinite;
}

```

Our animation line is setting the keyframe to  `loading`, telling it to last for 1.2 seconds, setting the  [timing function](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function)  to  `ease-in-out`  to make it smooth, and tell it to loop forever with  `infinite`.

![](https://www.freecodecamp.org/news/content/images/2020/05/static-html-css-gray-background-subtle-gradient.jpg)

No change – it's not animating

If you notice though after saving that, it's still not doing anything. The reason for this is we're setting our gradient from one end of the DOM element to the other, so there's nowhere to move!

So let's try also setting a  `background-size`  on our  `.loading`  class.

```css
.loading {
  color: transparent;
  background: linear-gradient(100deg, #eceff1 30%, #f6f7f8 50%, #eceff1 70%);
  background-size: 400%;
  animation: loading 1.2s ease-in-out infinite;
}

```

Now, since our background expands beyond our DOM element (you can't see that part), it has some space to animate with and we get our animation!

![](https://www.freecodecamp.org/news/content/images/2020/05/static-html-css-loading-animation.gif)

Our loading animation!

[Follow along with the commit!](https://github.com/colbyfayock/my-css-loading-animation-static/commit/bc4b5ec955a0906fea032edbbaf90f037f76c91b)

## Part 2: Using our loading animation in a dynamic app

Now that we have our loading animation, let's put it into action with a basic example where we fake a loading state.

The trick with actually using this is typically we don't have the actual content available, so in most cases, we have to fake it.

To show you how we can do this, we're going to build a simple  [React](https://reactjs.org/)  app with  [Next.js](https://nextjs.org/).

### Step 1: Creating an example React app with Next.js

Navigate to the directory you want to create your new project in and run:

```shell
yarn create next-app
# or
npm init next-app

```

It will prompt you with some options, particularly a name which will determine the directory the project is created in and the type of project. I'm using  `my-css-loading-animation-dynamic`  and the "Default Starter App".

![](https://www.freecodecamp.org/news/content/images/2020/05/nextjs-new-project.jpg)

Creating a new project with Next.js

Once installed, navigate into your new directory and start up your development server:

```
cd [directory]
yarn dev
# or 
npm run dev

```

![](https://www.freecodecamp.org/news/content/images/2020/05/nextjs-starting-dev-server.jpg)

Starting development server with Next.js

Next, let's replace the content in our  `pages/index.js`  file. I'm going to derive the content from the previous example, but we'll create it similar to how we might expect it to come from an API. First, let's add our content as an object above our return statement:

```javascript
const content = {
  header: `So, how 'bout them Knicks?`,
  intro: `What are their names? I'm Santa Claus! This opera's as lousy as it is brilliant! Your lyrics lack subtlety. You can't just have your characters announce how they feel. That makes me feel angry! Good news, everyone! I've taught the toaster to feel love!`,
  list: [
    `Yes! In your face, Gandhi!`,
    `So I really am important? How I feel when I'm drunk is correct?`,
    `Who are those horrible orange men?`
  ]
}
```

To display that content, inside  `<main>`, let's replace the content with:

```jsx
<main>
  <h1>{ content.header }</h1>
  <p>{ content.intro }</p>
  <ul>
    { content.list.map((item, i) => {
      return (
        <li key={i}>{ item }</li>
      )
    })}
  </ul>
</main>

```

And for the styles, you can copy and paste everything from our Part 1  `main.css`  file into the  `<style>`  tags at the bottom of our index page. That will leave us with:

![](https://www.freecodecamp.org/news/content/images/2020/05/basic-content-with-nextjs.jpg)

Basic content with Next.js

With that, we should be back to a similar point we finished at in Part 1 except we're not actively using any of the loading animations yet.

[Follow along with the commit!](https://github.com/colbyfayock/my-css-loading-animation-dynamic/commit/365e081522ec07b1754bf360a95b0bc373476c95)

### Step 2: Faking loading data from an API

The example we're working with is pretty simple. You'd probably see this coming pre-generated statically, but this helps us create a realistic demo that we can test our loading animation with.

To fake our loading state, we're going to use React's  `useState`,  `useEffect`, and an old fashioned  `setTimeout`  to preload some "loading" content, and after the  `setTimeout`  finishes, update that content with our actual data. In the meantime, we'll know that we're in a loading state with a separate instance of  `useState`.

First, we need to import our dependencies. At the top of our  `pages/index.js`  file, add:

```jsx
import { useState, useEffect } from 'react';

```

Above our  `content`  object, let's add some state:

```jsx
const [loadingState, updateLoadingState] = useState(true);
const [contentState, updateContentState] = useState({})

```

And in our content, we can update the instances to use that state:

```jsx
<h1>{ contentState.header }</h1>
<p>{ contentState.intro }</p>
<ul>
  { contentState.list.map((item, i) => {
    return (
      <li key={i}>{ item }</li>
    )
  })}
</ul>

```

Once you save and load that, you'll first notice we get an error because our  `list`  property doesn't exist on our  `contentState`, so we can first fix that:

```jsx
{ Array.isArray(contentState.list) && contentState.list.map((item, i) => {
  return (
    <li key={i}>{ item }</li>
  )
})}

```

And after that's ready, let's add our  `setTimeout`  inside of a  `useEffect`  hook to simulate our data loading. Add this under our  `content`  object:

```jsx
useEffect(() => {
  setTimeout(() => {
    updateContentState(content);
    updateLoadingState(false)
  }, 2000);
}, [])

```

Once you save and open up your browser, you'll notice that for 2 seconds you don't have any content and then it loads in, basically simulating loading that data asynchronously.

[Follow along with the commit!](https://github.com/colbyfayock/my-css-loading-animation-dynamic/commit/f0cada8d696ffe3e983f5efc03dc9d75a2245fe1)

### Step 3: Adding our loading animation

Now we can finally add our loading animation. So to do this, we're going to use our loading state we set up using  `useState`  and if the content is loading, add our  `.loading`  class to our elements.

Before we do that, instead of individually adding this class to each item in the DOM, it might make more sense to do so using CSS and adding the class to the parent, so let's do that first.

First, update the  `.loading`  class to target our elements:

```css
.loading h1,
.loading p,
.loading li {
  color: transparent;
  background: linear-gradient(100deg, #eceff1 30%, #f6f7f8 50%, #eceff1 70%);
  background-size: 400%;
  animation: loading 1.2s ease-in-out infinite;
}

```

Then we can dynamically add our class to our  `<main>`  tag:

```jsx
<main className={loadingState ? 'loading' : ''}>

```

_Note: if you use  [Sass](https://sass-lang.com/), you can manage your loading styles by  [extending](https://sass-lang.com/documentation/at-rules/extend)  the  `.loading`  class in the instances you want to use it or create a  [placeholder](https://sass-lang.com/documentation/style-rules/placeholder-selectors)  and extend that!_

And if you refresh the page, you'll notice it's still just a blank page for 2 seconds!

The issue, is when we load our content, nothing exists inside of our tags that can that would allow the line-height of the elements to give it a height.

![](https://www.freecodecamp.org/news/content/images/2020/05/html-css-collapsed-content.jpg)

No height when there's no content

But we can fix that! Because our  `.loading`  class sets our text to transparent, we can simply add the word  `Loading`  for each piece of content:

```jsx
const [contentState, updateContentState] = useState({
  header: 'Loading',
  intro: 'Loading',
  list: [
    'Loading',
    'Loading',
    'Loading'
  ]
})

```

_Note: We can't use an empty space here because that alone won't provide us with a height when rendered in the DOM._

And once you save and reload the page, our first 2 seconds will have a loading state that reflects our content!

![](https://www.freecodecamp.org/news/content/images/2020/05/html-css-loading-animation-1.gif)

HTML & CSS loading animation

[Follow along with the commit!](https://github.com/colbyfayock/my-css-loading-animation-dynamic/commit/5b7b1c40d1eebf97f65c966bb771a5f6787073ea)

## Some additional thoughts

This technique can be used pretty broadly. Being a CSS class makes it nice and easy to add where every you want.

If you're not a fan of setting the  `Loading`  text for the loading state, another option is to set a fixed height. The only issue with that is it requires more maintenance for tweaking the CSS to match what the content loading in will look like.

Additionally, this won't be perfect. More often than not, you won't know exactly how much copy you have on a page. The goal is to simulate and hint that there will be content and that it's currently loading.

Reference : [https://www.freecodecamp.org/news/how-to-use-css-to-create-a-beautiful-loading-animation-for-your-app/](https://www.freecodecamp.org/news/how-to-use-css-to-create-a-beautiful-loading-animation-for-your-app/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY4MjI2NDA4XX0=
-->