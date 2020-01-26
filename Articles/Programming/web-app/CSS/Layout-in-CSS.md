# Layout in CSS

![enter image description here](https://miro.medium.com/max/2500/0*8O0Gk7m8pIJO35H2)

_This post (_[_Layout in CSS_](https://sargalias.com/blog/layout-in-css/)_) was originally published on_ [_Sargalias_](https://sargalias.com/)_._

----------

This article is about how to create a good layout in CSS. We’ll tackle layout in CSS from a few angles, specifically:

-   Things you must know to be able to handle layout in CSS effectively.
-   Positioning between a container and its components.
-   Positioning elements belonging to a component.
-   Positioning sibling components.

The goal is to show you how to do layout in CSS in a way that’s organised well for the lifetime of the project. Following these methods, you should encounter very few (if any) cascade issues in the future. The main way to manage this is by keeping components separate and decoupled from each other in terms of positioning.

So on we go.

----------

# Important considerations

Before we even start looking at the layout methods, there are some important things you need to know. We’ll mention them briefly here, but you really should know these concepts fairly well for the purposes of this article. Some good resources are listed to learn more about them if you need to.

# CSS components

A component is basically HTML and CSS that goes together and is counted as a standalone entity. For example a  _button_  would be a component. A  _widget_  with all the elements it contains and its functionality may be another component.

The benefit of components is that they are **reusable** and they can be placed anywhere on the website and still _look right_.

Also, if you structure your CSS well, you never have to worry about any unrelated CSS rules overriding anything in a component. You can be confident that your component will stay looking correct forever, unless you specifically make a change to it. This also goes for everything else you do in the project. A component will never be affected unless you deliberately intend to change it.

To learn more about how to code with components in mind, have a look at  [BEM](http://getbem.com/). Other ways of getting the same effect are things like using  [CSS Modules](https://github.com/css-modules/css-modules), among others.

# Margin-collapsing

If you’re going to think about layout, it is absolutely essential to know how margin-collapsing works. If you don’t know it off by heart, here are the articles to look at:

-   [Mastering margin-collapsing (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
-   [What you should know about collapsing margins (CSS-Tricks)](https://css-tricks.com/what-you-should-know-about-collapsing-margins/)

Keep it in mind any time you’re working on layout.

# Padding vs margin

_padding_  is part of the element. Things like the border and background depend on it.

_margin_  is the minimum empty space away from the element.

# Margin-top vs margin-bottom vs both

## Notes

`margin-top`  vs  `margin-bottom`  is only a discussion you need to worry about when you’re styling  _base styles_.  _Base styles_  are basically default styles with  _tag selectors_  and low  _specificity_.

The classic example is a  [WordPress](https://wordpress.org/)  blog post page. You probably don’t want to be styling that based on  _classes_. It would be better if you just styled the elements to have the correct styles by default.

On the other hand, if you’re positioning things within component, it really doesn’t matter whether you use  `margin-bottom`  or  `margin-top`. It’s all contained within that component and it won’t affect anything else, so you can use whatever works.

## Margin-top

`margin-top`  is best for when you need to style an element  **based on what element came before it**.

For example, imagine that you want every image in a blog post to be  `2rem`  below other elements by default, but in the case where an image is followed by another image, you want the space between them to only be  `1rem`.

In this case, you would have to use the selector  `img + img`. Since combinator selectors match the last element, you would be forced to use  `margin-top`.

**Example**

img { margin-top: 2rem; }  
img + img { margin-top: 1rem; }

## Margin-bottom

`margin-bottom`  is better when something requires a specific  `margin-bottom`, regardless of what element follows it.

For example, if you want every  `h2`  to have a minimum space underneath it of  `2rem`, you would use the  `margin-bottom`property.

**Example**
```
h2 { margin-bottom: 2rem; }
```
## Both

Using both is also acceptable. That way you can set minimum spacing both above and below each particular element.

As long as you understand how  _margin-collapsing_  works, there won’t be any problem.

h2 {  
  margin-top: 1rem;  
  margin-bottom: 2rem;  
}img {  
  margin-top: 2rem; // must have at least 2rem space above it  
  margin-bottom: 1rem;  
}img + img {  
  /*  
    Has only 1rem above it when it's after another image.  
    Margin collapsing results in just 1rem space between the two images,  
    even though there is a margin-bottom of 1rem and margin-top of 1 rem.  
   */  
  margin-top: 1rem;  
}

# Variables and standardization

One very important principle to mention about layout in general, is that things should be as standardized as possible and you should have variables for common things.

For example, ideally you shouldn’t be coming up with  `margin`  values based on what you think looks right at that moment. Generally, it would be much better to have your standard  `margin`  or  _general space_  value in a variable. Then you can just use that every time you need a  `margin`.

Of course you can have multiple values, that’s fine as well. Overall your website will feel much more consistent than having random values everywhere.

## Refactoring into variables

You should try to refactor everything you can into global variables. My general rule of thumb is if it’s used 3 times or more anywhere on the site, then I make a variable for it.

The disclaimer is that they also have to be  _related_  and it has to make sense for those things to be refactored into a single variable. It’s not enough that they have the same value. Those values need to have the same  _meaning_.

For example, imagine that you have multiple declarations of  `margin: 3rem;`, as well as multiple declarations of  `padding: 3rem;`in different places. These two values don’t necessarily  _mean_  the same thing. One might be your common value for  _section margin_, whereas the other one might be the  `padding`  within some  _hero_  components. Those two values shouldn’t be under the same variable, because tomorrow you might want to change your  _section margin_  without changing the other value. It’s important that you refactor things into variables which  **semantically mean the same thing**. Don’t refactor things because they happen to have the same value by coincidence. Refactor things that  _are_  the same value, both in value and meaning.

## Where to place variables

I put every single variable in a specific file at the top of the project. That way they are all in one place and it’s easy to change the look of the entire website just by changing the values of variables.

## Things to refactor

The variables include almost everything, such as:

-   Spacings
-   Borders
-   Font-sizes
-   Colors
-   Shadows
-   Etc.

Refactoring things into variables is a no-brainer for CSS today. It allows you to make changes very quickly and helps keep things consistent. Particularly for layout, this consistency can really help out. It’s much easier to space things if you can use a pre-set value, than to have to calculate correct spacing for elements every time.

----------

# Layout

Understanding the concepts above, we can now move onto layout. So how do you go about creating the best layout in CSS?

As mentioned above, broadly speaking, there are 3 scenarios to consider:

-   Positioning between a container and its components.
-   Positioning elements belonging to a component.
-   Positioning sibling components.

The first one is probably the trickiest one, so let’s start with that.

# Positioning components within containers

Here are what (in my experience) are the best methods for positioning components within containers.

## The best layout method — Decoupled containers and components

## What we want

-   Components within a container shouldn’t care about their positioning at all.
-   The container should position the components it contains.This also means that containers are in charge of spacing their components away from each other properly. E.g. by using CSS grid.
-   Optionally, the components can fill up the entire area that the container provides. This isn’t necessary, but it does mean that things are even more decoupled (and more fluid in terms of responsive design). However it doesn’t make sense for all components to be able to stretch more than a certain size.

## Why it’s important

In short, if a component never cares about where it’s positioned,  **it is completely decoupled from its container**. All a component has to do is care about itself.

This means that:  **Any component or container can be swapped out at any time and everything will still look perfect. No need to change any CSS whatsoever.**

In comparison, if a component needs to change its  `margin`  and such depending on where it is and what’s around it, then it will never be completely  **reusable**. It will always need to CSS changes before it’s placed anywhere.

# Ways of achieving decoupled containers and components

## Using grid

`grid`  provides  _gutters_  and allows for exact positioning of child elements. So if  `grid`  is a reasonable  `display`  mode to use, it’s very easy to achieve decoupled containers and components with it.

**Pros**

-   Very good for positioning child components in a pattern.
-   Has  _gutters_  (the  `gap`  property), so can position child components without them needing a  `margin`.

**Cons**

-   If it’s not positioning things in a pattern, it will require some specific targeting, probably resulting in messy CSS. E.g. quite complicated`grid-template-columns`  and / or  `grid-template-rows`.
-   To use the  `grid-template-areas`  property, child components will need to have a complimentary property set on them.

**Implementation**

Implementation of this method is extremely simple.
```css
.container {  
  display: grid;  
  gap: 2rem;  
}
```
Consider the pen below. Note how:

-   The parent sets the positioning of the components.
-   Each component takes up the full amount of space given to it and the components are right up against the  _content-box_  of the container.

## Display modes other than grid

For  `display`  modes  `flex`  and  `block`, things are not as simple:

-   If there are multiple components inside a container, they currently need a  `margin`  to space themselves out from their siblings, because an equivalent to the  `gap`  property doesn’t exist for these  `display`  modes.
-   For the components to fill up the entire container, without any margins in-between, there will need to be an additional  _inner container_. This  _inner container_  will provide a  _negative_  `margin`  to counteract the  `margin`  of the components, so that the components fill up the entire space provided by the initial container.

**Pros**

-   Will potentially be very good when the  `gap`  property (or equivalent) is implemented on them.
-   `Flexbox`  is often required to achieve a particular kind of positioning, and generally doesn’t require its child elements to have  `margin`.

**Cons**

-   Requires an additional inner container for the components to fill up the entire container (which is optional).
-   Components need to set their own margin for now (until box alignment level 3 is implemented).
-   Initially an unexpected way to structure your CSS. New developers in the team or less experienced developers may not understand it.

**Implementation**

Note: These would be far easier to do in REMs. Then you wouldn’t have any weird maths with percentages.

## Using BEM mix

A  _mix_  in BEM is when an element has both a class for a  _BEM block_  as well as a  _BEM element_.

(This concept is hardly ever mentioned in BEM, so I’m not sure whether its use is acceptable or frowned upon.)

The BEM element is due to the parent container.

The BEM block is because it’s a self contained block.

With this method, as long as the BEM block never sets its own margins, the parent container can have very good control over the block’s positioning.

**Pros**

-   Can target child components individually.
-   Child components don’t need to have any margin.

**Cons**

-   Requires the child component to never have any margin.

**Implementation**

<div class="parent-block">  
    <div class="parent-block__element child-block">Both an element and a block</div>  
</div>

## Specific containers for components

With this method, the parent block has elements specifically for positioning child components.

**Pros**

-   Perfect positioning of child components.

**Cons**

-   It’s a lot of extra HTML and CSS.

**Implementation**

<div class="parent-block">  
    <div class="parent-block__element-for-specific-child">  
        <div class="child-block">Child block</div>  
    </div>  
</div>

# Alternative layouts for for containers and components

## Alternative layout 1 — Container sets padding left and top, components set margin right and bottom

With this method, the container sets its  `padding-left`  and  `padding-top`.

Components space themselves away from their siblings by setting  `margin-right`  and  `margin-bottom`.

Container sets  `padding-right`  and  `padding-bottom`, accounting for the  `margin`  of the components, so that the end result is symmetrical to the  `padding-left`  and  `padding-top`.

**Pros**

-   A simpler layout than some of the layouts for decoupling containers and components.

**Cons**

-   Correct spacing strongly couples the spacing of the components and the container.
-   Components can’t be switched without adjusting their positioning.
-   There may be cases where the components’  `margin-bottom`  is too large, so that there is far more space at the bottom of the container than the  `padding-top`  covers. In that case, you’ll either have to use an  _inner container_(just like with the  _decoupled containers and parent_  workaround), or you’ll have to rely on  _margin-collapsing_  to make the components fill up the entire container.

**Implementation**

**Note: These would be far easier to do in REMs. Then you wouldn’t have any weird maths with percentages.**

## Alternative layout 2 — Container weakly selects immediate components

With this method, the container selects their immediate components without increasing the  _specificity_  of the selector. (Low  _specificity_  is paramount if you want to have CSS that won’t spiral out of control and destroys your project. There isn’t a single CSS methodology out there that advocates high  _specificity_.)

**Pros**

-   The container sets the spacing of components. This means that at least the component doesn’t need to care about its positioning, so it doesn’t need to alter its CSS to account for whatever spacing it might need. It’s all done by the parent.
-   Selector specificity is not increased.

**Cons**

-   The components must not have  _margins_  themselves, otherwise you’ll have  _cascade_  issues.
-   This method sets the  _margins_  of all components to be exactly the same. You can’t pick and choose different  _margins_  for different components. This means that you can’t space different components different if that’s what’s needed.
-   If the container has multiple siblings and it needs them spaced out, it will need to put a margin on them. This means that the components won’t take up the entire space of the container unless an  _inner container_  is used.

**Implementation**

.container > * { margin: 1rem; }

## Alternative layout 3 — Container strongly selects components

With this method the container directly selects its components and sets their spacing.

The container can use any number of  _selectors_  and  _pseudo-classes_  it needs.

**Pros**

-   Can target any of the components and set different margins on them.

**Cons**

-   Everything from alternative layout 2, except that you can space individual components differently.
-   Specificity is increased  **(which is probably the worst thing possible in CSS)**.

**Implementation**

.container {  
  .component { margin: 1rem }  
  .component:last-child { margin: 2rem }  
}

## Suggestions

In the end, we don’t currently have a method which is perfect.

The  `grid`  and  `flexbox`  display modes are not always usable.

The  _BEM mix_  method is pretty good, but it’s not BEM best practice.

The  _specific containers_  method has extra HTML and CSS.

So pick your poison, the method which you think is the least bad.

Other than those methods, there are also the alternative layout methods to consider.

# Positioning siblings within a single component

This is much simpler than positioning between containers and components because:

-   Components are self-contained. They do not affect anything else outside of the component.
-   Elements belonging to a component are not decoupled from each other. They expect those other elements to be there and may depend upon them.

Overall, this means that you can use any method you want to style a component correctly. Nothing needs to be decoupled.

So if you can use the methods mentioned above for keeping containers and components separate, feel free to do so, but any other method should be absolutely fine.

# Positioning sibling components

This can be an interesting case.

Technically, this situation is exactly the same as the container and components scenario, because everything has a parent container. At the very highest level it’s the  `body`  element.

This means that the ideal solutions are already discussed in the container and components section.

However, for very high level components (like things nested immediately under the  `body`  element, such as the website header or footer), it may be fine to just give them a  `margin-bottom`  or  `margin-top`  and be done with it.

After all, making the  `body`  element decide the  `margin`  for the header and footer doesn’t provide any benefit here. It’s not like those components will be moved and used elsewhere like normal components.

# Final note

A final note to keep in mind is that, above all else, you write CSS to make things look the way you want them to look. You also need to write your CSS in a way that it’s easy to maintain in the future.

In the end the layouts mentioned here are just  **suggestions**, not hard rules. There will definitely be cases where they’re not optimal and where it makes more sense to use something else or break some of the concepts mentioned here. Be pragmatic and think about what makes the most sense to use at any time in your project.

However, I hope that knowing of these layout methods expands your “layout vocabulary” and that the explanations behind why they’re useful hopefully show you some concepts that are good to be aware of.

Also if you have any other layout methods you like,  **please share in the comments**.

> Written with [StackEdit](https://medium.com/@sargalias/layout-in-css-634c3ca3dcff).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MTMyMTg5NzFdfQ==
-->