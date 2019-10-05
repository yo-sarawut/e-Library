
Simple Vue.js Form Validation with Vuelidate
==

![enter image description here](https://miro.medium.com/max/1200/1*bVjduU244kDytiGwuoFrmg.png)

Thanks to Vue’s reactivity model, it’s really easy to roll your own form validations. This can be done with a simple method call on the form submit, or a computed property evaluating input data on each change.

Using your form validation can quickly become cumbersome and annoying, however, especially when the number of inputs in the form increase, or the form structure gets more complicated e.g. multi-step forms.

Thankfully, there are great validation plugins for Vue like  [Vuelidate](https://github.com/monterail/vuelidate). In this article, we’ll be looking at how Vuelidate can be used to simplify:

-   Validation
-   Multi-step form validation
-   Child component validation
-   Error messages

We’ll also see how the  [Vuelidate-error-extractor](https://github.com/dobromir-hristov/vuelidate-error-extractor)  plugin can be used to simplify error message display per input, or as an error summary above or below the form.

> Note: this article was originally posted  [here on the Vue.js Developers blog](https://vuejsdevelopers.com/2018/08/27/vue-js-form-handling-vuelidate/?utm_source=medium-vjd&utm_medium=article&utm_campaign=fhv)  on 2018/08/27

# Basic validation with Vuelidate

**Vuelidate**  is data-model oriented, meaning validation rules are added to a  `validations`  object in the component definition, rather than being added directly to input elements in the DOM.

The structure must resemble that of the form object, but the number of validation rules can be dynamic and change depending on which fields need validation.

Here’s a live example:

# Defining custom validators

Out of the box validation rules in Vuetify will work for most cases, but every so often you’ll need a custom validator.

With  **Vuelidate**, each validation rule is a function that returns a  `Boolean`  or  `Promise`  resolving to a  `Boolean`. This means you can predefine your own validators in a  `validators.js`  file and just import each validator when needed.

Custom validators receive the currently validated data as a first param, and the whole data context as a second. For example, if you have a form data object and you are validating the email property, the first param will be the email itself and the second will be the whole data object.

You can also create custom validators with the help of a few special helpers that come packed with  **Vuelidate**. Check out the  [Custom Validators](https://monterail.github.io/vuelidate/#custom-validators)  section in the Vuelidate docs for examples.

# Dynamically changing rules

Being able to change the validation rules on the fly can be a godsend with multi-step forms. Each step has its own rules that validate certain parts of the form data.

**Vuelidate**  can use computed properties as validation rules. That means that you can return different rules for each step of a multi-step form.

In the example below,  `validations`  is now a function returning an object, rather just an object. This means it will be called after the component is initialized and computed properties are run.

# Breaking down large forms into child components

Once a form gets bigger, you might want split up your form into several smaller components to avoid having a mega component handling all the form validation.

However, storing form data in separate components rather than in a single place makes collecting the data harder. You could loop each child component via a  `ref`  binding and get the data, either implementing a data fetcher method or naming the form data in a specific way.

Another way is to store form data in Vuex, where you define all the rules on the parent and create a computed property referencing the store’s form state. Pass down the validator to each component if needed.

> _Tip: if using Vuex for form data, try the_ [_vuex-map-fields_](https://github.com/maoberlehner/vuex-map-fields) _plugin to reduce boilerplate by setting each field as a computed property._

For most cases, I keep all the data and validation rules on a parent wrapping component that passes down the relevant validator to each child as a prop and handles sending the data to the server.

Each smaller component then uses the  `$touch()`  method on its validator prop to note that data is being changed and emits changed data via  `$emit('input', value)`  for easy  `v-model`  binding.

To make the validator available to all children, you have a few options:

-   Pass it down as a prop to each component
-   Use the  [Provide/Inject API](https://medium.com/@znck/provide-inject-in-vue-2-2-b6473a7f7816)
-   Create a new Vue instance in the store itself. Check  [this gist](https://gist.github.com/autumnwoodberry/d56d4f28d987b846c5216b2142586f7c)  on how that might work

Here’s a live example of the first method i.e. passing the down as a prop to each component. This is the simplest to comprehend and in most situations will be the one you will want to use.

Once we’ve covered error message display, I’ll show you an example using the Provide/Inject API.

# Validation error display

So the form is in place, its validated on each key press, but what about displaying error messages to the users?

We can just check each validator for errors and color our inputs, but what if we wanted to show a message? What if there is a need to display more than one error at a time? If/else checks start flying around everywhere.

As you can see there is a lot of repetition there, a lot of checking, you need to know what validators each field has. Adding a new rule means you have to go and edit the template too.

# Error display with Vuelidate-error-extractor

There is a better way!  **Vuelidate-error-extractor**, which I wrote, does the heavy lifting for you by extracting all the errors for each field, finding the appropriate error message for each rule and displaying it. It gives the user a flexible way of displaying errors with minimal boilerplate and repetitiveness.

You can use one of the built-in templates for Bootstrap and Foundation or just as easily build our own to suit your needs. All you need to do is register the plugin, define an object containing common error messages and register the template you want to use. We will refer to the single input error display as  `singleErrorExtractor`

# Creating custom error display components

**Vuelidate-error-extractor**  loops the validations for each form data and checks each rule if it’s valid or not. The invalid ones are then extracted and a validation error message is assigned to them.

The bundled  `singleErrorExtractorMixin`  provides a set of helper methods and computed properties to assist the developer with building their own input error display.

Now just wrap your input with the new component:

Check out  [custom templates docs](https://dobromir-hristov.github.io/vuelidate-error-extractor/custom_templates.html)  for a detailed explanation on how to make your own error display.

Being so flexible means that you can adapt it to any Vue UI framework you wish. Here is a list of popular UI frameworks and examples how to implement it for each one:  [https://dobromir-hristov.github.io/vuelidate-error-extractor/other_frameworks.html](https://dobromir-hristov.github.io/vuelidate-error-extractor/other_frameworks.html)

# Form error summary

Sometimes you need to have a summary of all the errors in a form, be it on top or at the bottom.

You can use the prebuilt components for Foundation or Bootstrap, use the  `baseMultiErrorExtractor`  component or the  `multiErrorExtractor`  mixin. For 90% of use cases, the  `baseMultiErrorExtractor`  will suffice.

It will reuse the same error messages that you defined up front for the  `singleErrorExtractor`  to use. The  `$validator`  must be passed as a prop.

To be able to assign a proper field label to each error, it requires an object called  `attributes`  to be defined where the error messages were defined. This object represents a map annotating how each field should be called, i.e.  `{ name: "Name", email: "Email" }`.

# Reducing boilerplate by injecting the validator

Passing the  `validator`  and  `attribute`  prop to each form input and the  `multiErrorExtractor`  can get annoying quite fast, not to mention the boilerplate.

To overcome this, you can use the provided  `form-wrapper`  component to inject the validator down to all inputs.

This method uses the Provide/Inject API to pass down the  `$validator`  to all the components that need it. Each  `form-group`  can then drop its  `validator`  and  `attribute`  props, to be replaced by a single  `name`  prop, annotating which field in the form it represents.

It will also try to figure out the input’s  `attribute`  property by checking the  `attributes`  object we defined earlier.

# Summary

Handling and validating forms on the front end as you saw, can often become a pain in the bum, especially when forms become big and need to be split up.

Using  **Vuelidate**  makes the whole ordeal a lot more bearable. In tandem with  **Vuelidate-error-extractor**, displaying error messages under each input can go from a tedious repetitive chore, to simply adding a wrapping component or two, that do it all for you.

# Code examples

-   [Basic validation with Vuelidate](https://codesandbox.io/embed/6y93q20wyr)
-   [Defining custom validators](https://codesandbox.io/embed/wwv80myowl)
-   [Dynamically changing rules](https://codesandbox.io/embed/o979o4myjq)
-   [Breaking down large forms into child components](https://codesandbox.io/embed/nnxy0wjpwm)
-   [Validation error display](https://codesandbox.io/embed/4w8x04l2k0)
-   [Error display with Vuelidate-error-extractor](https://codesandbox.io/embed/mjxzpvpw6j)
-   [Creating custom error display components](https://codesandbox.io/embed/l240kmxwl)
-   [Form error summary](https://codesandbox.io/embed/6v1lyz831r)
-   [Reducing boilerplate by injecting the validator](https://codesandbox.io/embed/0p986z74p0)

> **Take A Free Vue.js Introduction Course!**  Learn what Vue is, what kind of apps you can build with it, how it compares to React & Angular, and more in this 30-minute video introduction.  [Enroll for free](https://courses.vuejsdevelopers.com/p/vue-js-crash-course?utm_source=medium-vjd&utm_medium=article)!

[**Source :**]()
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzQ5MzE3NDZdfQ==
-->