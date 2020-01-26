
A Guide to CSS Animation — Part 2
==
![enter image description here](https://miro.medium.com/max/4752/1*8VI1jY60cMT8ij5lHr6Ydw.jpeg)
# animation-iteration-count

Let’s pick up from where we left off with by modifying our first animation. If you need a little refresher, this is what we had.



![](https://miro.medium.com/max/480/1*-Ip2pjgEccC_u8_jszRNSw.gif)

But the animation only ran once. What if we wanted the animation to run many times or not even stop? In the case of loading animations, we may want the animation to be infinite. This is where  `animation-iteration-count`  comes into play.

Let’s say we wanted the animation to run five times.



![](https://miro.medium.com/max/1448/1*jI6tr2c3WxzefQtv8gQs8w.png)

It’s as easy as that. Let’s turn our spinning square into a loading spinner. To do this,  `animation-iteration-count`  also accepts the keyword  `infinite`  👍


![](https://miro.medium.com/max/1448/1*Kjxi4yjkLLU_XYq-0HgsAg.png)

Which gives us the following 🎉

# animation-timing-function

Let’s take another look at that spinning square. The square does keep on spinning. But not without a little break after every spin. This is due to the  `animation-timing-function`.



![](https://miro.medium.com/max/480/1*ZLekwO4QthfAWlBgM-9vpA.gif)

The  `animation-timing-function`  property defines the speed characteristics of an animation. It accepts a few different values.

-   `cubic-bezier(x1, y1, x2, y2)`  - provides ability to define custom speed
-   `ease`  - start and end slowly but speedier in the middle(default)
-   `ease-in`- start slowly
-   `ease-in-out`  - start and end slowly but not the same as  `ease`
-   `ease-out`  - end slowly
-   `linear`  - maintain speed throughout
-   `steps(number, direction <optional>)`  - provides a way to split the animation into equal steps.  `direction`  values can either be  `start`  or  `end`.  `start`  means that the first step happens at the start of the animation.  `end`  means that the last step happens at the end of the animation.  `end`  is the default value.

So which one do you choose? Different scenarios will call for different easing. The following is a nice short resource about the basics of easing.

## [The Basics of Easing | Web Fundamentals | Google Developers](https://developers.google.com/web/fundamentals/design-and-ux/animations/the-basics-of-easing)


You can experiment with different easings to find what feels right in your applications. This pen shows how  `animation-timing-function`  can affect the same animation.

The only ease that might be trickier to grasp is  `cubic-bezier`.

## [Cubic Bézier curves - Wikipedia](https://en.wikipedia.org/wiki/B%C3%A9zier_curve#Cubic_B%C3%A9zier_curves)



In essence the  `cubic-bezier`  function defines a cubic bezier curve. There is a good explanation about the  `cubic-bezier`  function in this article

## [Single Transition Timing Function | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/single-transition-timing-function)



Or, you may prefer to play with the  `cubic-bezier`  function and compare it to the other easing values.  [cubic-bezier.com](http://cubic-bezier.com/)  has you covered 👍

----------

So returning to our spinning square. How do we remove that little break? We can apply a  `linear`  timing. This replaces the default  `ease`  timing.



![](https://miro.medium.com/max/1448/1*ITaERJZnx5Gix2wV1djZ8w.png)

This would give us



![](https://miro.medium.com/max/480/1*itA_VOJEAGwgdUSJFCVckQ.gif)

Sweet 🍭

# animation-play-state

Play state is pretty simple. You can pause animations or have them running. You do this with the  `animation-play-state`  property. For our spinning square we could introduce a checkbox that toggles the play state. Using the sibling selector, we can toggle the play state 👍



![](https://miro.medium.com/max/1448/1*WkJUXh31d-XxMKYiBKsv3Q.png)

When it’s  `:checked`  we set the play state to  `running`  👟

# animation-delay

Next up is delaying animations. Like  `animation-duration`,  `animation-delay`  takes a time value in milliseconds or seconds.

Let’s add some extra squares and have them all spin side by side  **once**. Note we’ve changed the  `animation-timing-function`  value to  `ease-out`.



![](https://miro.medium.com/max/480/1*r_w4OO-aSm4qeu-WxuDeyg.gif)

If we add a delay to each square could we create a staggered effect?



![](https://miro.medium.com/max/1448/1*7DTrcNdqSOcQT3yimOPSoQ.png)

The answer is yes! 👍

But, if we then wanted the squares to keep spinning we would lose the staggered effect. This is because  `animation-delay`  is only applied once before an animation begins 👎 It does not apply to every iteration of an animation. At this point we have two choices. We could experiment with different delays using the Animations Inspector. Or we could try stalling the first half of the animation by delaying the spin.



![](https://miro.medium.com/max/1448/1*eF33-X5vMbwtM8FlE6mlAg.png)

# animation-fill-mode

Next up is  `animation-fill-mode`. This one’s magic 🎩

By default, when we apply an animation to an element, it has no affect before or after it has ran.  `animation-fill-mode`  changes that.

The values for  `animation-fill-mode`  that will interest us are;

-   `forwards`  - element retains animation styling
-   `backwards`- element retains style from first keyframe during  `animation-delay`
-   `both`  - element retains styling in both directions

Let’s consider an animation where we shrink an element to half its size.



![](https://miro.medium.com/max/480/1*VUOlV2x_ttxTNnVCAPDAXg.gif)

Without using  `animation-fill-mode`  the element returns to normal size at the end of the animation. But using  `animation-fill-mode`  means we can keep the element at half size once the animation ends.



![](https://miro.medium.com/max/1448/1*5fYAMthgl7D0KGKYGRRx0Q.png)

Now a more common scenario for using  `animation-fill-mode`  is when showing and hiding elements. Consider a scenario where we have three elements that we want to fade in.



![](https://miro.medium.com/max/1448/1*RDzvBINfWRW-ayw9plJh0g.png)

We’d prefer a staggered effect so we give each element a different  `animation-delay`.



![](https://miro.medium.com/max/480/1*frFfGF2sru6RyHlyj3_uAw.gif)

But the outcome is not quite as desired because we didn’t use  `animation-fill-mode`  👎 Applying  `animation-fill-mode: backwards`  will fix it!

For another demo consider this walk sign using  `animation-fill-mode`  🚶

# animation-direction

Last but not least is animation-direction. No surprises that this property allows you to define the direction of your animation. There are four main keywords;

-   `alternate`- the direction of the animation alternates on each iteration
-   `alternate-reverse`- same as  `alternate`  but starts in  `reverse`
-   `normal`  - self explanatory
-   `reverse`  - the animation is played in reverse

For an example we could use  `alternate`  for something that opens and closes.

How about a clapper board?



![](https://miro.medium.com/max/480/1*YS2mQVJYJKKTdA5tKY3JzQ.gif)

Using an  `animation-iteration-count`  of  `2`  with  `animation-direction`  `alternate`  saves us writing separate animations.

# animation shorthand

If you’ve got this far, that’s all the animation properties 🎉 You know them all now 🤓 There’s now an opportunity to tidy up your animation code by using the shorthand property. That’s right, you don’t need to write out all the properties each time.

This



![](https://miro.medium.com/max/1448/1*M-li0KTmg0QpkwuzKdkoVg.png)

Is equivalent to this



![](https://miro.medium.com/max/1448/1*H358682oCimDg_z4N4mFPg.png)

Sweet 🍭



![](https://miro.medium.com/max/1448/1*08nwrxY4gHU2uT2iz-gHtg.png)

Those properties are also optional so you can use whichever combination you need 👍

But that’s not all. Using the  `animation`  property makes it a little easier to apply many animations to an element.

Consider an element that we make come in from below and then rotate by 45 degrees.



![](https://miro.medium.com/max/1448/1*oOPotWMrPIhx-WUCrj9z6A.png)

You can use comma separated values for your  `animation`  properties. But you could also do this



![](https://miro.medium.com/max/1448/1*v8v0Xpj91Yo08mIij91uZQ.png)

----------


> Written with [StackEdit](https://codeburst.io/a-guide-to-css-animation-part-2-2cd422f78567).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTU5NzM2MTQwLC03NjAwMzQ4MTNdfQ==
-->