Vue.js — Forms, components and considerations
===

![enter image description here](https://miro.medium.com/max/1061/1*mP3ujHhKk-yFDsRntcapPw.png)

Forms are the key for an application to collect data from the user. Form handling is something that quickly gets out of hand if not contained properly. With the arrival of AJAX and then SPA (Single Page Applications), things have drastically changed. With SPA, you don’t even need HTML  `<form>`  element.

Making forms work is one thing and implementing them in a right way is altogether a different thing. Challenges are too many:

-   Accessibility
-   Aesthetics
-   Validations
-   Usability

Today, implementing Forms is not just about placing a few  `input`  or  `select`  tags. It is also about custom form components like Rich Text Editors, Date Pickers, etc. There are plenty of articles/tutorials about forms and custom input components, but we are yet to talk about best practices and challenges. This article is an attempt to highlight these considerations. Though we discuss with respect to Vue.js, many underlying principles are equally applicable to form handling in any SPA framework.

----------

# Accessibility and structure

## 1. Do not forget  `<form>`  element

With Vue.js, it is not necessary to use  `<form>`  element when you are dealing with Forms.  **But stop there!**  Wrapping your input components within  `<form>`  tag is the most sensible way to start caring for  **accessibility**. Assisted technologies, scrapping tools treat  `form`  differently. This is one of our Form which we pushed to production:

![](https://miro.medium.com/max/30/1*g4ERrBb634hDBaf5YYS1dg.png?q=20)

![](https://miro.medium.com/max/1136/1*g4ERrBb634hDBaf5YYS1dg.png)

No <form> tag

Another aspect is developer readability. By looking at the above code, a developer cannot easily infer what and where input controls are unless he reads the code line-by-line. It is not very helpful. Presence of  `<form>`  tag is a good indicator for a developer and allows better navigation in complex HTML structure.

> This is what Angular has got right. Angular needs  **Form element if you ever wish to do form handling. This is baked into the framework. However, it is not the case with Vue.js or React.**

## 2. Do not forget <label> element

HTML  `<label>`  element is the next thing you must do in order to have good accessibility. As in the previous code snippet, our form has no labels either. Without a label, screen-reader cannot speak to the user about form input element. It is the standard way to define a label for Form widget (Form input component). If there is only one thing you can do about accessibility, then it should be setting up proper labels.

> Another important thing about label is they are clickable. If properly set, a click on a label will activate given input element (custom or native).

As a side note, avoid putting multiple labels for the same input element. That can cause issues.

## 3. Nested forms

A common misconception happens when you try to split a bigger form into smaller components. Following the guideline 1, developers try to wrap input widgets into  `form`  element. And, when you finally compose these mini-forms into bigger form, you end up with  `<form>`  containing nested the  `<form>`  element.

> Nested form elements are forbidden in HTML.

Consider using alternatives like  `fieldset`  or custom form-component that framework provides. Or in case of Vue.js, if you have a form that can be used independently or within another larger form, consider creating three components as shown:

![](https://miro.medium.com/max/30/1*9I2zte42YYZff542rG_e9g.png?q=20)

![](https://miro.medium.com/max/741/1*9I2zte42YYZff542rG_e9g.png)

Sub-form represented as dummy component and used in other higher-order components

We have a base/dumb component that contains our input controls and common logic extracted into a separate file. These can then be imported into respective components.

> Again, Angular has nicely handled nested forms with the help of  **formArray**  and  **formGroup**  directives.With Vue.js, we have to take care of this at an application level. This doesn’t means Angular is superior at form handling. It has its own issues and quirks.

## 4. Clean form structure

Unless you have a neat HTML structure, your JavaScript code will never be optimal. If we apply the rule that 80% of the time is spent on reading the code and remaining 20% writing it, then it becomes very important that you have a neat HTML structure.

> Developers get a feel of component by looking at its structure/interface and not its JavaScript code.

Consider how twisted HTML structure can get even with two fields:

![](https://miro.medium.com/max/30/1*CyUH_QuTVq4cI987l8A4Sw.png?q=20)

![](https://miro.medium.com/max/1500/1*CyUH_QuTVq4cI987l8A4Sw.png)

How not to write HTML for Forms

Careful inspection tells us certain information:

-   Two input fields — one native and another custom field.
-   Difficult to identify fields as there is no label. Instead, a  `span`  is used.
-   Two error messages, each placed above input control.
-   One hint message after native input.
-   One  `blur`  event on native input to validate. No  `blur`  event for custom input control.
-   Unintuitive class manipulations

This is not very helpful. Constant back-n-forth between HTML, CSS and JavaScript would be required to understand exact behavior.  **Just by looking at HTML structure, we cannot feel the shape of our form.**  In worst case, developer would be forced to run the application and then see shape. Now consider the alternate representation of the same form:

![](https://miro.medium.com/max/30/1*UV17RREdFc_Cggqu2Ix_Xg.png?q=20)

![](https://miro.medium.com/max/1285/1*UV17RREdFc_Cggqu2Ix_Xg.png)

Cleaning up HTML structure

Same thing much cleaner!!!  **All we did was we promised to clean up our HTML. This cleaning up of HTML prompted us to rethink about how we are doing validations.**  This is a progressive enhancement. It is not just for users or web. It is for developers too. First create good DOM structure. Then polish it with styles. And then move on to JavaScript for all the business logic. There is no other way than this. Next time any developer trying to make modifications to this code, is set for quick pace. It helps us reiterate the fact that:

> Unless you have a neat HTML structure, your JavaScript code can never be optimal.

We have created three simple wrapper components:

1.  `input-container`  — Shows hint or error but not both at a same time
2.  `input-hint`  — Adds styling for hint text
3.  `input-error`  — Adds styling for error messages

_(Note: You will notice an absence of_ `_for_` _attribute for_ `_label_` _and_ `_name_` _attribute for_ `_input_` _element. They are just removed for the sake of brevity.)_

----------

# Presentation and Styling

Having talked about structure, it is time to consider styling aspects for forms and input controls; just don’t forget the principle —  _Have a neat HTML structure_.

## 5. Consistent aesthetics

A sufficiently large scale web application will have many custom input controls. They will be developed internally or imported from a third-party library. For example, our current Vue.js based project uses  [Google Material](https://github.com/material-components/material-components-web/),  [FlatPickr](https://flatpickr.js.org/),  [Trix editor](http://trix-editor.org/)  and others. At one point on the same form we had two distinct styles:

![](https://miro.medium.com/max/30/1*e2z5RqSsYhSmRgkYYba6ng.png?q=20)

![](https://miro.medium.com/max/620/1*e2z5RqSsYhSmRgkYYba6ng.png)

Mixed styling feels unpleasant

Needs for consistent aesthetics paves the way for next important consideration which is  **Ease of customization**.

## 6. Ease of Style Customization

Any custom form input component we develop or import from a third party should be easy to customize. When we say easy, it means it should be obvious to change commonly required CSS properties like font-size, color, border-style, width, height, etc. 100% style customization is not required. Good input components have following traits:

-   No hard-coded values for height and colors
-   Easy to change font-size
-   BEM like flat selectors for style overriding
-   Exposing CSS variables for common elements
-   No pre-specified margins

There are many popular components in Vue.js community. But if we need to customize styling, it is not that easy. Some of the examples are:

![](https://miro.medium.com/max/30/1*RXJwdLjdS6aCzko-RllRTg.png?q=20)

![](https://miro.medium.com/max/621/1*RXJwdLjdS6aCzko-RllRTg.png)

Components break or look ugly.

## 7. Minimum and Viable Styling for state

A Component should out-of-box provide minimal styling for different states. Every form input component has at least following state:

-   Default —input control is untouched
-   Error — when validation has failed for given input
-   Focus and blur state
-   Disabled state
-   Read-only state (different from disabled state)

----------

# JavaScript and Interactions

Finally, it is time to discuss interactions for the custom input controls. This is where we extensively start talking about Vue.js and Forms.

## 8. Focus and Blur event

This is the fundamental need of any input control. Many times, custom components are shipped without  `focus`  and  `blur`  event.  `blur`  event is used to trigger validations and other UI state changes whereas focus is often used to clear error state, bring overlay list, show/hide hints, etc.

> If the custom component is made-up of HTML elements that are not focus-able, then  `tagindex`  attribute can be used on any HTML element to trap the focus via mouse click or keyboard  `Tab`  key.

![](https://miro.medium.com/max/30/1*FD7caSiLaJyqG9s6RJlB4A.png?q=20)

![](https://miro.medium.com/max/433/1*FD7caSiLaJyqG9s6RJlB4A.png)

If the custom component has multiple focus-able elements, then have clear and unambiguous focus order for these elements.

## 9. Emit what you accept

> Rule is Simple. If a component accepts  **a string, then it should emit a string on change. If component accepts a date object, then it should emit a date object. However, if component accepts a date as as string, then do not emit value of date as a Date object on change.**

There are many components in the wild that does this. One example is  [vue-flatpickr-component](https://github.com/ankurk91/vue-flatpickr-component). If you are following immutable data practices, then it can land you in trouble. For example, you are listening for change event from a component, and trying to trigger an API request. A component is passed a date as  `string`  and it emits  `Date`  object on change which is essentially the same date you passed. Since immutability relies on simple equality check, the equality would fail and cause unwanted API request.

[](https://github.com/ankurk91/vue-flatpickr-component?source=post_page-----d81b3ffe9efb----------------------)


## 10. Stick to :value and @input binding

In Vue,  `v-model`  directive is used to create two-way binding on form input controls. This is also applicable to  **custom input controls**. So, the following two are equivalent:

<!-- Two-way binding syntax sugar using **v-model** -->  
<custom-input v-model="data"></custom-input><!-- Two-way binding under the hood -->  
<custom-input  
  v-bind:value="data"  
  v-on:input="data = $event"></custom-input>

This is the default behavior of  `v-model`  directive. It uses  `value`  as a prop and  `input`  as an event. But Vue.js allows you to customize this behavior by using  `model`  option:

// v-model here binds to **checked prop** and **change event**  
Vue.component('custom-input', {  
  // ... More options  
  model: {  
    prop: 'checked',  
    event: 'change'  
  }  
}

The suggestion here is to stick to what Vue.js provides out-of-box. I have seen  `model`  being changed just for the convenience of the component author. Vue.js is powerful but with it comes great responsibility.  `model`  customization is meant for scenarios where  `value`  prop  [serves a different purpose](https://vuejs.org/v2/guide/components-custom-events.html#Customizing-Component-v-model). Breaking this convention hampers code readability in general.

> Be idiomatic in handling  `:value`  and  `@input`  binding, you will get  `v-model`  for free. If  `v-model`  doesn’t work or you have to do something extra to support it, that means you are doing something wrong.

## 11. @input and @change events

HTML5 specification has defined two events — [input](https://developer.mozilla.org/en-US/docs/Web/Events/input)  and  [change](https://developer.mozilla.org/en-US/docs/Web/Events/change). These events are fired on native form inputs —  `input`,  `select`  and  `textarea`  element.

> To model native input elements as much as possible, custom Vue.js form input components should also emit input and change event.

What is the different between  **input**  and  **change**  event?  `input`  is fired whenever the value of the input control is changed.  `change`  is fired when a value of the input control is changed and  **that change is committed by the user.**  Change is committed when a user has made a selection or lost focus to the component. For example:

<input type="text" @input="onInput" @change="onChange" />

So when user type  **_abc_**  as a value,  `onInput`  will be called three times, one event for each keystroke; whereas  `onChange`  will not be called. It is when a user has changed his focus or pressed enter key (committing a change), the change event will fire.

> In a nutshell, ‘input’ event is fired repeatedly on each keystroke while ‘change’ event is fired less often than input event, on blur or selection.

It is important for your custom input component to support both types of events. For custom input controls like  `auto-complete`,  `input`  these events are critical as every keystroke may invoke an API request. For  `multi-select`,  `change`  event may matter more than  `input`  event as you may always be interested in the final result of a multi-select. Again, this depends on the UX demands of the application.

Well defined support for  `@input`  and  `@change`  event is vital and a key to building neat Forms.

## 12. Do not emit @input event from the value watcher

> Read this as: Do never fire @input event on changing the value programmatically.

Input event should be emitted by the component when a user has interacted with the component and changed the value. If a parent component has set the value of the custom input control and if you are watching for  `value`  prop, then no matter what,  **never emit** `**input**` **event from the watcher. This should be forbidden:**

**// POOR ABSTRACTION**  
Vue.component('custom-input', {  
    // ... More options  
    watch: {  
        value(newValue) {  
             const toEmit = someTransform(newValue);  
             const isProgrammatic = true; **// ABSOLUTELY FORBIDDEN**  
             this.$emit('input', toEmit, isProgrammatic);  
        }  
    }  
}

This happens when you do not have a proper parent-child relationship and attempting to do sibling component communication as shown in the following diagram:

![](https://miro.medium.com/max/30/1*4sGSomabAQDfjTnn06Q3Dg.png?q=20)

![](https://miro.medium.com/max/514/1*4sGSomabAQDfjTnn06Q3Dg.png)

This is reminiscent of many legacy practices that were relevant before the rise of Angular, React and alike. To further worsen the situation, you may be tempted to pass an additional boolean flag to signify if  **value change**  is caused by user interaction or not. Accordingly, you may decide to do a different action. Example, if a user changes the value, trigger an API call, otherwise, search within local data.

This becomes even more problematic when you use one-way data flow in your application. In fact, this is not just restricted to custom input components, it is applicable to any component built with any framework.

> When working with React, the only way is Prop and thus this problem doesn’t occur. Such implicit workflows are difficult in React which is mostly declarative. With Vue.js, one has to be careful with the freedom it provides.

## 13. Support for unidirectional/one-way data flow

Assuming that you have followed guidelines 9, 10, 11 and 12, the next step is to make your custom input components adhere to the one-way data flow. There are components that work seamlessly with  `v-model`  but fail when used with  `:value`  and  `@input`  bindings separately. When you are using unidirectional data architectural which happens naturally with Vuex or Redux, such components fail. In order for custom input controls to work well with unidirectional architecture, two things are a must:

1.  Support for  `:value`  and  `@input`  bindings.  `v-model`  is just a syntax sugar.
2.  Support for immutable data. Custom components typically deal with complex objects. Vue.js cannot detect mutations to the nested object values. Thus as a developer, you should ensure that whenever a value is changed, a new copy of the data is returned instead of mutating original  `:value`  passed to the input control.

Of course, failure to do so doesn’t mean that you cannot have unidirectional data architecture. But that leads to many issues and you will end up writing awkward code. For example, when you are using multi-select component and list of selected values are sliced from Vuex or Redux store and bound to the component  `prop`; if the multi-select component mutates the list upon user interaction, the mutation/change to the state happens outside of Vuex/Redux store/reducer which is forbidden and introduces many subtle bugs which are hard to track.

![](https://miro.medium.com/max/30/1*dlDr-g6vH7kKCxD5Fo_mug.png?q=20)

![](https://miro.medium.com/max/588/1*dlDr-g6vH7kKCxD5Fo_mug.png)

Good unidirectional architecture is possible only with immutability

> So far, I have seen only one custom input component explicitly mentioning keywords like  [immutability and equality](https://github.com/basecamp/trix#immutability-and-equality). It is the  [trix-editor](https://github.com/basecamp/trix)  by Basecamp Team. It is a Web Component not a Vue.js component. We have built our own Vue.js wrapper around it. I am still surprised to see lack of immutability in many components. Nobody seems to even mention such a vital aspect.

## 14. Consistent form validations

Finally, if everything goes right, the last topic of this discussion is  **Form Validation**. It is often an afterthought, thus ignored and yet very tricky aspect to handle. Angular is very particular about Forms and Form validations. That is not the case with Vue.js.

> Vue.js leaves  **Form Validation**  concerns outside of the core for good reasons. Form Validation is not just a development thing; lots of UX concerns are also involved. Every situation calls for a unique form validation technique and its error-state representation.

As said earlier, Angular has got Forms right in terms of accessibility but in terms of validations, it is too particular often causing more troubles than solving the problem. With Angular, you will find yourself dealing too much with touch/pristine state along with model validation. With Vue.js, the situation is better. You have a choice of doing it yourself or through many excellent external libraries like vee-validate and vuelidate.

Form validation is challenging because:

-   Validation could be sync or async
-   Validation state has many UX complications.

**To begin with, you can show validation state as soon as the Form is loaded.**

![](https://miro.medium.com/freeze/max/30/1*smLMMBhAFfo1lnYBFO434g.gif?q=20)

![](https://miro.medium.com/max/1016/1*smLMMBhAFfo1lnYBFO434g.gif)

Showing error as soon as form is loaded. Works but bad User Experience.

**Sometimes, you want to show errors/hints/warnings the moment a user interacts with an input control (here** `**input**` **event is critical).**

![](https://miro.medium.com/freeze/max/30/1*mw8cHyizV0la7JHfoxgBmA.gif?q=20)

![](https://miro.medium.com/max/1020/1*mw8cHyizV0la7JHfoxgBmA.gif)

Wait for user to interact at least once with a form.

**You may need to show error state after the user has interacted with the component (**`**blur**` **and** `**focus**` **events take center stage).**

![](https://miro.medium.com/freeze/max/30/1*xJQoqH02g4r0cdzQVQZFqw.gif?q=20)

![](https://miro.medium.com/max/1013/1*xJQoqH02g4r0cdzQVQZFqw.gif)

Trigger validation on focus and blur events

**Or, you wish to show errors only when the user has clicked submit/save button.**

![](https://miro.medium.com/freeze/max/30/1*3gYibgEFATrBQdNczK5fsQ.gif?q=20)

![](https://miro.medium.com/max/1021/1*3gYibgEFATrBQdNczK5fsQ.gif)

Wait for submit button interaction at least once

We are still just scratching the surface. There are many possibilities:

1.  In other cases, you wish to start showing an error after first submit button interaction. Then error should continue until the error is fixed.
2.  In few cases, you will want to clean entire error-state of the form as soon as user interacts with any input control.
3.  In rare cases, you will have a mixed form where some input controls should have immediate validation trigger (like creating new email account) and remaining fields should have validations on  `@blur`  event.

And on top of this, we have custom input controls. The list goes on …

Ideal form validation should support many design styles as no style fits all. I highly recommend the use of  [Vuelidate](https://monterail.github.io/vuelidate/) — Model based form validation.

[](https://monterail.github.io/vuelidate/?source=post_page-----d81b3ffe9efb----------------------)

## 

Vuelidate | A Vue.js library.

### 

Simple, lightweight model-based validation for Vue.js

#### 

monterail.github.io

## 15. Native form input events

There are cases where you need to have a common event handler on  `<form>`  element for events like  `focus`,  `blur`,  `input`, etc. This also applies to custom input elements as shown in the following snippets:

**<!-- Capture focus, blur from child input controls -->**  
<form @focus="resetError" @blur="validate" @input="doSomething"> <custom-input-1></custom-input-1> <custom-input-2></custom-input-2>  
</form>

Our events should bubble up so that  `form`  element can listen to them. But, the way event handling works in Vue.js, events do not bubble up for the custom elements. Also, just because we emit  `focus`  event, it doesn’t count as a native  `focus`  event. We need to trigger real native event using:

// Within Vue.js componentconst customEvent = new Event('input');// Vue.js only event  
this.$emit('input');// Native HTML event  
this.$el.dispatchEvent(customEvent);

Using  `dispatchEvent`, we can create real native event which will bubble up. But the question here is — **Should we do this? Well, I am not sure.**  I did not feel the need to do this yet. I asked this question on Stack Overflow and Twitter but haven’t got a convincing response yet:

[](https://stackoverflow.com/questions/50861726/should-we-use-native-input-event-for-custom-form-components-in-vue-js?source=post_page-----d81b3ffe9efb----------------------)

## 

Should we use native input event for custom form components in Vue.js?

### 

Consider the following Vue.js code: I have a form with three input elements. One is native input element whereas…

#### 

stackoverflow.com

Should you trigger native events for custom input controls?

There are few who seem to agree with this:

They meant ‘form.elements’ collection

Maybe we will have to wait for Web Components and see how frameworks incorporate them into the current ecosystem.

**16. Integration with Forms**

You can extend guideline 15 further by introducing hidden input field for custom component. By default, contents of a custom input control will not be sent over with a traditional form submission. To do this use, custom field.

> To make custom input behave like native input control, trick is to use hidden input field.

As shown in  [trix-editor](https://github.com/basecamp/trix)  documentation:

<form>  
    <input id="x" type="hidden" name="content">  
    <trix-editor input="x"></trix-editor>  
</form>

You can access your custom input control just like native input using  `HTMLFormControlsCollection`  returned by  [HTMLFormElement.elements](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/elements).

----------

# Other important aspects

-   **Immutable Forms**: As long as guideline 13 is followed, it becomes trivial to design immutable forms. For all the reasons why immutability is good, the same concept is applicable to Forms. Immutable forms are tremendously helpful in taming complexity and improving readability. Yes, there is a side effect that implementing immutability in JavaScript is not as easy as in any standard functional language; the readability benefits still far exceed this small nuisance.
-   **Support for read-only and disabled state for custom input**
-   **Use community libraries**: Consider using community component before building your own. You cannot address all of these concerns at once. It takes time to build robust, accessible and optimal components.
-   **Keep an eye on Web Components**: It is time to look for ways on how we can incorporate Web Components into our daily development to promote code reuse. This is even more applicable for leaf components.
-   **Taking accessibility further**: Consider going beyond simple  `<form>`  and  `<label>`  and adding full support for accessibility using  `aria`  [attributes](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA).

[**Source :**](https://blog.webf.zone/vue-js-forms-components-and-considerations-d81b3ffe9efb)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4OTc1OTA4MDJdfQ==
-->