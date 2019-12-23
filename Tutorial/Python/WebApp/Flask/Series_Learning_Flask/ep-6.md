
# Jinja template design | Learning Flask Ep. 6

An brief introduction to the power of the Jinja templating engine

In this part of the Learning Flask series, we're going to dive deeper into the Jinja templating engine and you'll learn more of the advanced features of this powerful library!

In the last part of this series, you learned how to create base templates, child templates and how to extend them. In this part you'll learn more about template design, working with Python objects in your HTML and a few more handy tips for writing efficient, reusable code.

There's a lot to cover, in fact, too much for this article. Check out the  [Jinja documentation](http://jinja.pocoo.org/docs/2.10/)  for a full list of the features available.

Let's get started!

### Creating a new view

For this example we'll create a new view called  `jinja`. Open up  `views.py`  and add the following route:

`@app.route("/jinja")
def jinja():
    return render_template("public/jinja.html")` 

We'll need to create a new child template for this view. Create a file called  `jinja.html`  in the  `templates/public`, open it in your editor and add the following:

**app/app/templates/public/jinja.html**

`{% extends "public/templates/public_template.html" %}

{% block title %}Jinja{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">
      <h1>Jinja</h1>
      <hr>

    </div>
  </div>
</div>

{% endblock %}` 

We should also add a link in our navbar so we access this view quickly! Go ahead and open up  `public_template.html`  in your editor.

Let's switch the  `About`  link to our new  `Jinja`  view.

Change this:

`<li class="nav-item">
  <a class="nav-link" href="/about">About</a>
</li>` 

To this:

`<li class="nav-item">
  <a class="nav-link" href="/jinja">Jinja</a>
</li>` 

Reload your browser and click on the Jinja link in the nav to see our new view in action.

### Passing objects to templates

We can pass any Python object to a template by passing it to the  `render_template`  function as a key/value pair. For example, let's create a simple variable called  `my_name`  and assign it a string value (Feel free to replace the value for your own!)

Open up  `views.py`  and create the new  `my_name`  variable inside the  `jinja`  view:

**app/app/views.py**

`@app.route("/jinja")
def jinja():
    my_name = "Julian"
    return render_template("public/jinja.html")` 

We pass objects to views in the  `render_template`  function as key/value pairs, like so:

`return render_template("public/jinja.html", my_name=my_name)` 

Go ahead and pass the  `my_name`  key/value pair into  `render_template`

Your view will now look like this:

**app/app/views.py**

`@app.route("/jinja")
def jinja():
    my_name = "Julian"
    return render_template("public/jinja.html", my_name=my_name)` 

Let's use this variable in our  `jinja.html`  template. We access objects in Jinja with the  `{{ object }}`  syntax.

Open up  `jinja.html`  and add the following just under the  `<hr>`  tag:

**app/app/templates/public/jinja.html**

`<h4>Accessing an objects value</h4>
<hr>
<p>Hello {{ my_name }}!</p>` 

Your  `jinja.html`  file should look like this:

**app/app/templates/public/jinja.html**

`{% extends "public/templates/public_template.html" %}

{% block title %}Jinja{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">
      <h1>Jinja</h1>
      <hr>

      <h4>Accessing an objects value</h4>
      <hr>
      <p>Hello {{ my_name }}!</p>

    </div>
  </div>
</div>

{% endblock %}` 

> Tip - Going forward, we're going to separate all of the sections in our  `jinja.html`  with a heading, description and example

Save the file and reload the page to see  `Hello`  and the value for  `my_name`!

We access an objects value in Jinja by passing it in between a pair of curly braces  `{{ like_so }}`

Let's create some more objects in our jinja view and pass them into our template. Replace the contents of the  `jinja`  function with the following:

**app/app/views.py**

`# Strings
my_name = "Julian"

# Integers
my_age = 30

# Lists
langs = ["Python", "JavaScript", "Bash", "Ruby", "C", "Rust"]

# Dictionaries
friends = {
    "Tony": 43,
    "Cody": 28,
    "Amy": 26,
    "Clarissa": 23,
    "Wendell": 39
}

# Tuples
colors = ("Red", "Blue")

# Booleans
cool = True

# Classes
class GitRemote:
    def __init__(self, name, description, domain):
        self.name = name
        self.description = description 
        self.domain = domain

    def clone(self, repo):
        return f"Cloning into {repo}"

my_remote = GitRemote(
    name="Learning Flask",
    description="Learn the Flask web framework for Python",
    domain="https://github.com/Julian-Nash/learning-flask.git"
)

# Functions
def repeat(x, qty=1):
    return x * qty` 

Now we need to pass our objects into our template using the  `render_template`  function. Pass them in as key/value pairs like the following:

**app/app/views.py**

`return render_template(
    "public/jinja.html", my_name=my_name, my_age=my_age, langs=langs,
    friends=friends, colors=colors, cool=cool, GitRemote=GitRemote, 
    my_remote=my_remote, repeat=repeat
)` 

Your  `jinja`  view should now look like this:

**app/app/views.py**

`@app.route("/jinja")
def jinja():

    # Strings
    my_name = "Julian"

    # Integers
    my_age = 30

    # Lists
    langs = ["Python", "JavaScript", "Bash", "Ruby", "C", "Rust"]

    # Dictionaries
    friends = {
        "Tony": 43,
        "Cody": 28,
        "Amy": 26,
        "Clarissa": 23,
        "Wendell": 39
    }

    # Tuples
    colors = ("Red", "Blue")

    # Booleans
    cool = True

    # Classes
    class GitRemote:
        def __init__(self, name, description, domain):
            self.name = name
            self.description = description 
            self.domain = domain

        def pull(self):
            return f"Pulling repo '{self.name}'"

        def clone(self, repo):
            return f"Cloning into {repo}"

    my_remote = GitRemote(
        name="Learning Flask",
        description="Learn the Flask web framework for Python",
        domain="https://github.com/Julian-Nash/learning-flask.git"
    )

    # Functions
    def repeat(x, qty=1):
        return x * qty

    return render_template(
        "public/jinja.html", my_name=my_name, my_age=my_age, langs=langs,
        friends=friends, colors=colors, cool=cool, GitRemote=GitRemote, 
        my_remote=my_remote, repeat=repeat
    )` 

Ok so we've added quite a lot of code to our view function, just some standard Python objects that most of which you should be fairly familiar with.

We then passed them as key/value pairs into our template using the  `render_template`  function.

Let's put them to use in  `jinja.html`.

### Accessing objects in templates

Our template now contains all of the objects we've passed into it. Let's explore what we can do with them!

#### Looping

Looping in Jinja is done with the following syntax:

`{% for variable in iterable %}
<!-- Do something with the variable -->
{{ variable }}
{% endfor %}` 

Just like a Python  `for loop`, we use the  `for variable in iterable`  syntax, wrapped in a pair of  `{% %}`  braces.

We then access the variable using the double curly brace syntax  `{{ variable }}`

For loops must always be closed with  `{% endfor %}`

Let's put this into practice and loop through our  `langs`  list and create a HTML list with each of the values:

**app/app/templates/public/jinja.html**

`<h4>Looping through an iterable</h4>
<hr>

<strong class="d-block mb-3">Programming languages</strong>
<ul>
  {% for lang in langs %}
  <li>{{ lang }}</li>
  {% endfor %}
</ul>` 

Reload your browser tab to see the changes.

We can also enumarate an iterable using  `{{ loop.index }}`

**app/app/templates/public/jinja.html**

`<h4>Looping and enumerating an iterable</h4>
<hr>

<strong class="d-block mb-3">Programming languages</strong>
<ul>
  {% for lang in langs %}
  <li>{{ loop.index }} - {{ lang }}</li>
  {% endfor %}
</ul>` 

> Tip -  `loop.index`  starts at 1. To start enumerating at 0, use  `loop.index0`

Let's loop though the key/value pairs of our  `friends`  dictionary:

**app/app/templates/public/jinja.html**

`<h4>Looping key/value pairs in a dict</h4>
<hr>

<strong class="d-block mb-3">Friends & ages</strong>
<ul>
  {% for name, age in friends.items() %}
  <li>{{ name }}: {{ age }}</li>
  {% endfor %}
</ul>` 

Just like in Python, we can access the dictionary methods such as  `.keys()`,  `.values()`  and  `.items()`.

Using the  `{% for variable in iterable %}`  and closing it with the  `{% endfor %}`  syntax, you can loop through any iterable, including lists, tuples, dictionaries, sets etc.. and access the variable value using  `{{ variable }}`

### Calling functions

We can call any functions we pass into our template simply by doing just that!

Let's call our  `repeat`  function and pass it some arguments:

**app/app/templates/public/jinja.html**

`<h4>Calling functions</h4>
<hr>
<p>{{ repeat("Jinja is great! ", 10) }}</p>` 

Save and refresh the page to see  `Jinja is great!`  printed 10 times.

Passing and calling functions from templates is useful, but an even better way is to create custom filters which you'll learn about shortly!

### Accessing object indexes, keys and attributes

Just like in Python, we can access the indexes, keys and attributes of an object.

Accessing a list index:

**app/app/templates/public/jinja.html**

`<h4>List index</h4>
<hr>
<p>{{ langs[0] }}</p>` 

Accessing a dictionary value:

**app/app/templates/public/jinja.html**

`<h4>Dictionary value</h4>
<hr>
<p>{{ friends["Tony"] }}</p>` 

Accessing a class attribute:

**app/app/templates/public/jinja.html**

`<h4>Class attributes</h4>
<hr>
<p>{{ my_remote.description }}</p>` 

As you can see, we just use the familiar Python syntax for accessing these values.

### Classes

You've seen how to access class attributes using the  `class.attribute`  syntax. We can also call class methods from our Jinja template, just like in Python:

**app/app/templates/public/jinja.html**

`<h4>Class methods</h4>
<hr>
<p>{{ my_remote.pull() }}</p>` 

### Assignments

Assigning new variables in Jinja is done using the  `{% set x = y %}`  syntax.

Let's create a new instance of our  `GitRemote`  class from within our template using the  `set`  tag:

**app/app/templates/public/jinja.html**

`<h4>Create a class</h4>
<hr>
{% set new_repo = GitRemote(
    name="Learning Flask",
    description="Learn the Flask web framework for Python",
    domain="https://github.com/Julian-Nash/learning-flask.git") 
%}
<p>{{ new_repo.description }}</p>` 

We can also unpack and set variables directly in our template, for example:

`<h4>Unpack variables</h4>
<hr>
{% set foo, bar = colors %}
<p>{{ foo }}</p>
<p>{{ bar }}</p>` 

### Conditionals & comparison operators

Just like in Python, Jinja gives us acccess to many of the familiar conditional operators.

`if`  statement:

**app/app/templates/public/jinja.html**

`<h4>Conditional if</h4>
<hr>
{% if cool %}
  <p>Cool = {{ cool }}</p>
{% endif %}` 

We have to close any  `if`  conditionals with the  `{% endif %}`  syntax

`if`,  `elif`  &  `else`:

**app/app/templates/public/jinja.html**

`<h4>Conditional if/elif</h4>
<hr>
{% if my_age < 18 %}
<p>No entry</p>
{% elif my_age <= 25 %}
<p>You may enter</p>
{% else %}
<p>Entry denied. You're not cool enough</p>
{% endif %}` 

As you'll see we threw in some Python comparison operators. You have access to all of the standard operators including:

-   `==`  Equality
-   `!=`  Inequality
-   `>`  Greater than
-   `>=`  Greater than or equal to
-   `<`  Less than
-   `<=`  Less than or equal to

> Tip - You must always close an  `{% if x %}`  statement with  `{% endif %}`

### Logic & other operators

Just like in Python, you have full access to the logic operators:

-   `and`  Return true if the left and the right operand are true
-   `or`  Return true if the left or the right operand are true.
-   `not`  Negate a statement (See tip below)
-   `(exp)`  Group an expression

> Tip - Read more about the  `not`  operator  [here](http://jinja.pocoo.org/docs/2.10/templates/#logic)  at the official Jinja docs

You'll also have access to many other operators you'll be familiar with including:

-   `in`  Containment test. For example  `{{ "a" in ["a", "b", "c"] }}`  will return  `true`
-   `is`  Performs a test.  `{% foo is bar %}`  /  `{{ foo is not bar }}`

### Special Jinja operators

Jinja features some special operators you may not be familiar with and we'll be using later in this guide:

-   `|`  Applies a filter (Continue reading) For example  `{{ langs|length }}`  will return  `6`
-   `~`  Converts all operands to strings and concatenates them, for example  `{{ "cool" ~ "==" ~ cool }}`  returns "cool==True"
-   `(**args, **kwargs)`  Callable. You've seen this used when we called class method

### Math

You'll have full access to all of the Python math operators in Jinja. Not particularly useful but there if you need them.

### Template filters

Jinja comes with a bunch of useful template filters which can be compared to funtions that take an argument or aguments and return a value or set of values.

We're only going to show a few in this example, but a full list of built in filters can be found  [here](http://jinja.pocoo.org/docs/2.10/templates/#logic)

The syntax for using filters is  `{{ object|filter }}`

We'll use the  `length`  filter to return the length of a list:

**app/app/templates/public/jinja.html**

`<h4>Built in filters (length)</h4>
<hr>
<p>{{ langs|length }}</p>` 

We can also use filters in conjunction with conditionals, for example:

**app/app/templates/public/jinja.html**

`<h4>Filters & conditionals</h4>
<hr>
{% if langs|length > 2 %}
  {% for lang in langs %}
    {% if lang == "Python" %}
      <p>{{ lang|upper }}</p>
    {% else %}
      <p>{{ lang|reverse }}</p>
    {% endif %}
  {% endfor %}
{% endif %}` 

> Tip - You can nest loops and conditionals just like in Python. Be sure to close the conditional or loop with an  `{% endif %}`  or  `{% endfor %}`  respectively

The  `upper`  filter will capitalize the string we pass to it whilst the  `reverse`  filter will return a reversed string.

Be sure to read the Jinja  [docs](http://jinja.pocoo.org/docs/2.10/templates/#list-of-builtin-filters)  for a full list of built in filters, they're incredibly useful

One of the filters I find myself using a lot is the  `join`  filter. Let's join our  `langs`  list into a single string:

**app/app/templates/public/jinja.html**

`<h4>Join filter</h4>
<hr>
<p>Unjoined: {{ langs }}</p>
<p>Joined: {{ langs|join(", ") }}</p>` 

### Custom filters

Flask provides us a convenient way to build our own custom template filters.

Let's create a filter that takes a datetime object and returns a nicely formatted string.

Open up  `views.py`  and add follow along.

First, we need to import the  `datetime`  library

**app/app/views.py**

`from datetime import datetime` 

Let's create a datetime variable in our  `jinja`  view and pass it to  `render_template`:

**app/app/views.py**

`date = datetime.utcnow()

return render_template(
    "public/jinja.html", my_name=my_name, my_age=my_age, langs=langs,
    friends=friends, colors=colors, cool=cool, GitRemote=GitRemote, 
    my_remote=my_remote, repeat=repeat, date=date
)` 

Let's drop our  `date`  variable into our  `jinja.html`  file and see how it looks without formatting:

**app/app/templates/public/jinja.html**

`<h4>Custom filters</h4>
<hr>
<p>{{ date }}</p>` 

Save and refresh your browser to see the raw datetime object:

`2019-02-06 17:40:58.374084` 

Let's create a custom filter and pass our  `date`  variable to it. Back in  `views.py`, add the following:

**app/app/views.py**

`@app.template_filter("clean_date")
def clean_date(dt):
    return dt.strftime("%d %b %Y")` 

We create custom filters by registering them on our app using the  `@app.template_filter`  syntax and passing it the name of the filter we want to create.

We then pass our object into the function defined below it. It's here we can modify the object and return it back to the template.

The great thing about custom template filters is that once defined, we can access them from any template in our app! In this case, we're just formatting the datetime object and returning it as a nicely formatted string.

Go ahead and save the file and reload the browser to see the changes take effect.

### Escaping

Escaping strings is vital in any web application as we simply cannot rely on our users (or ourselves!) to ensure we're not passing in any malicious strings that may get executed by the browser.

In Flask, auto escaping IS enabled by default for all templates ending in  `.html`,  `.htm`,  `.xml`  and  `.xhtml`  when using the  `render_template`  function.

Let's start by looking at when we want to insert some HTML or JavaScript into our template to be executed by the browser. This is not uncommon, in fact, you're looking at it right now!

Let's create a variable in our  `jinja`  route and assign it an HTML string:

**app/app/views.py**

`my_html = "<h1>This is some HTML</h1>"` 

Be sure to pass it to  `render_template`  as  `my_html=my_html`

Let's dump  `my_html`  into our  `jinja.html`  template:

**app/app/templates/public/jinja.html**

`<h4>Escaped</h4>
<hr>
{{ my_html }}` 

Save and reload the page.

Instinct tell us that the browser is going to parse the HTML and render it as part of our page. However, as Flask enables Jinja escaping by default, we just see a string containing the HTML, rather than the H1 heading we defined.

Let's escape our  `my_html`  variable and make it part of the page with the  `safe`  filter:

**app/app/templates/public/jinja.html**

`<h4>Marked as safe</h4>
<hr>
{{ my_html|safe }}` 

You'll see a big H1 heading which is now part of our pages actual HTML.

> Tip - Use with caution. Never pipe any values through the  `safe`  filter from untrusted sources. Especially from users!

To illustrate this, let's create a suspicious variables in our  `jinja`  view:

**app/app/views.py**

`suspicious = "<script>alert('NEVER TRUST USER INPUT!')</script>"` 

Pass the  `suspicious`  variable to  `render_template`  and add the following to  `jinja.html`:

**app/app/templates/public/jinja.html**

`<h4>Suspicious script</h4>
<hr>
{{ suspicious|safe }}` 

Save and refresh your browser to see why cautious use of the  `safe`  filter is required! (Don't worry it's safe... Get it?)

Go ahead and comment out the last part otherwise you'll have an annoying  `alert`  dialogue every time you reload your browser!

Let's move on to macros.

### macros

Jinja macros are an extremely convenient and useful way to create reusable code within your templates. They're a bit like functions as in we can reuse them over and over again and supply arguments.

We define a  `macro`  with the following syntax:

``{% macro macro_name(**args, **kwargs) -%}
  <!-- We then define the code we want as part of our macro -->
  <!-- We have access to any args & kwargs passed into the macro -->
  <!-- We access the args and kwargs with the familiar `{{ variable }}` syntax -->
{%- endmacro %}`` 

> Tip - Pay attention to the dashes in the opening and closing {% macro -%} & {%- endmacro %} tags

A demonstration is in order!

Say you've got a page with lots of input fields, we can create an  `input`  macro and pass it arguments which then get rendered within the macro.

Open up  `jinja.html`  and add the following:

**app/app/templates/public/jinja.html**

`{% macro input(label="", type="text", id="", name="", placeholder="") -%}
  <div class="form-group">
    <label>{{ label }}</label>
    <input type="{{ type }}" class="form-control" id="{{ id }}" name="{{ name }}" placeholder="{{ placeholder }}">
  </div>
{%- endmacro %}` 

We've created an HTML  `input`  elemt inside our macro which we can pass arguments to and reuse throughout our template.

> Tip - Notice the default arguments? You can do that with macros!

Here's the syntax to use a macro in your templates:

`{{ macro_name(**args, **kwargs) }}` 

Let's go ahead and use our macro a few times in  `jinja.html`. We'll wrap our macros in a  `<form>`  tag:

**app/app/templates/public/jinja.html**

`<h4>Macros</h4>
<hr>

{% macro input(label="", type="text", id="", name="", placeholder="") -%}
  <div class="form-group">
    <label>{{ label }}</label>
    <input type="{{ type }}" class="form-control" id="{{ id }}" name="{{ name }}" placeholder="{{ placeholder }}">
  </div>
{%- endmacro %}

<form action="#" method="POST">

    {{ input(label="Name", id="name", name="name", placeholder="Enter your name") }}

    {{ input(label="Email", type="email", id="email", name="email", placeholder="Enter your email") }}

    {{ input(label="Password", id="password", name="password", placeholder="Enter your password") }}

</form>` 

Save and refresh your browser.

Awesome, we've got 3  `<input>`  fields all with different labels, types, names, ids and placeholders. Notice how little code we had to white to produce these 3 input fields? That's the power of macros!

Another key feature of macros, is being able to import them from other templates, similarly to how you import a Python library.

Let's create a  `macros`  directory at the root of our  `templates`  directory and create a new file in there called  `input_macros.html`.

Open up  `input_macros.html`  and copy and paste the macro we just created:

**app/app/templates/macros/input_macros.html**

`{% macro input(label="", type="text", id="", name="", placeholder="") -%}
  <div class="form-group">
    <label>{{ label }}</label>
    <input type="{{ type }}" class="form-control" id="{{ id }}" name="{{ name }}" placeholder="{{ placeholder }}">
  </div>
{%- endmacro %}` 

Save and close the file.

Now back in  `jinja.html`, we're going to refactor our code to import and use the macro from  `input_macros.html`.

First up, we need to import the template. At the top of  `jinja.html`, just under the  `{% extends %}`  tag, add the following:

`{% import "macros/input_macros.html" as im %}` 

We now have full access to any of the macros defined in  `input_macros.html`! Pretty cool right.

We just need to refactor our existing macros and get rid of the macro we created in  `jinja.html`  just now. Go ahead and delete the macro and change the following:

from this:

**app/app/templates/public/jinja.html**

`<form action="#" method="POST">

  {{ input(label="Name", id="name", name="name", placeholder="Enter your name") }}

  {{ input(label="Email", type="email", id="email", name="email", placeholder="Enter your email") }}

  {{ input(label="Password", id="password", name="password", placeholder="Enter your password") }}

</form>` 

To this:

**app/app/templates/public/jinja.html**

`<form action="#" method="POST">

  {{ im.input(label="Name", id="name", name="name", placeholder="Enter your name") }}

  {{ im.input(label="Email", type="email", id="email", name="email", placeholder="Enter your email") }}

  {{ im.input(label="Password", id="password", name="password", placeholder="Enter your password") }}

</form>` 

We've just prepend our macro calls with  `im`  after adding  `{% import "macros/input_macros.html" as im %}`  at the top of the file.

### Wrapping up

As you can see, Jinja provides us with some pretty useful tools for creating smart templates in our Flask application (And I can't help but feel I've only touched the surface!)

I highly suggest you have a look through the  [Jinja documentation](http://jinja.pocoo.org/docs/2.10/)  to grasp even more knowledge of this awesome templating language.

Getting to grips with Jinja early on can really make a difference. You'll be way more efficient and reduce the amount of boilerplate code you're writing.

Drop a comment below if you found this guide useful or if you think I missed anything critical. This wasn't designed to be an exhaustive or in depth guide (That's what the docs are for!) But it should give you enough ammo to start designing smarter templates of your own!

Last modified  ·  28 Feb 2019






> Written with [StackEdit](https://pythonise.com/series/learning-flask/jinja-template-design).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5ODU1ODM3NF19
-->