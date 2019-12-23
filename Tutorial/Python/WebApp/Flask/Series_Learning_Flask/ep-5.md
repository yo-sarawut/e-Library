
# Jinja template inheritance | Learning Flask Ep. 5

Creating reusable base HTML templates and extending them throughout your Flask app

In this firth part of the Learning Flask series, you'll learn how to use the powerful Jinja templating engine to make working with our HTML files much more efficient.

Template inheritance works by creating a series of "base templates" and importing them into "child templates", minimising the amount of repetitive code we need to write and allowing us to reuse elements effectively and reliably.

Jinja templating can be a bit confusing at first but quickly becomes fun to work with and a joy to use!

We'll pick up where we left off from the last episode.

Let's get coding!

### Creating base templates

If you've been following along with this series, you'll be familiar enough with the concept of breaking up our Flask app into sub-directories and seperate files to maintain good readibility and create a clear separation of the different elements of our app.

Let's take a quick at our application structure:
```html
`app
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── static
│   │   ├── css
│   │   │   └── style.css
│   │   ├── img
│   │   │   └── flask.png
│   │   └── js
│   │       └── app.js
│   ├── templates
│   │   ├── admin
│   │   │   └── dashboard.html
│   │   └── public
│   │       └── index.html
│   └── views.py
├── requirements.txt
└── run.py` 
```
> Tip - I'm generating these directory maps using the  `tree`  command in my terminal

We're going to create 2 new  `templates`  directories.

-   One at  `templates/admin/templates`
-   One at  `templates/public/templates`

Let's create them now from the root  `app`  directory:

`mkdir /app/templates/admin/templates
mkdir app/templates/public/templates` 

Let's also create some HTML templates in those directories:

`touch app/templates/admin/templates/admin_template.html
touch app/templates/public/templates/admin_template.html` 

Now let's take a quick glance at our file structure:
```html
`app
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── static
│   │   ├── css
│   │   │   └── style.css
│   │   ├── img
│   │   │   └── flask.png
│   │   └── js
│   │       └── app.js
│   ├── templates
│   │   ├── admin
│   │   │   ├── dashboard.html
│   │   │   └── templates
│   │   │       └── admin_template.html
│   │   └── public
│   │       ├── index.html
│   │       └── templates
│   │           └── public_template.html
│   └── views.py
├── requirements.txt
└── run.py` 
```
We've added our 2 base HTML template files to the 2 directories.

> Note - To make things a little more interesting, we're going to use the Bootstrap CSS & JS library. Head over to the the Bootstrap webside to download the source files or feel free to use the Bootstrap CDN (Recommended).

If you're using the Bootstrap starter template found  [here](https://getbootstrap.com/docs/4.2/getting-started/introduction/#starter-template). You don't need to download any of the source files, otherwise, go ahead and download the Bootstrap library and jQuery library and do the following:

You can get the jQuery source code  [here](https://code.jquery.com/jquery-3.0.0.slim.min.js). Just copy and paste it into a file called  `jquery.slim.min.js`

-   Place  `bootstrap.min.css`  in the  `static/css`  directory
-   Place  `bootstrap.bundle.min.js`  in the  `static/js`  directory
-   place  `jquery.slim.min.js`  in the  `static/js`  directory

Go ahead and open up  `public_template.html`  in your editor and add the following:

**app/app/templates/public/templates/public_template.html**
```html
`<!doctype html>
<html lang="en">

<head>
  <!-- Required meta tags -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

  <!-- Import the Bootstrap stylesheet -->
  <link rel="stylesheet" href="{{ url_for('static', filename='css/bootstrap.min.css') }}">
  <!-- Import our custom stylesheet -->
  <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">

  <title>{% block title %}{% endblock %}</title>
</head>

<body>

  <main>
    {% block main %}{% endblock %}
  </main>

  <!-- Import jquery 3.3.1 slim min -->
  <script src="{{ url_for('static', filename='js/jquery.slim.min.js') }}"></script>
  <!-- Import Bootstrap bundle -->
  <script src="{{ url_for('static', filename='js/bootstrap.bundle.min.js') }}"></script>
  <!-- Import our custom JavaScript -->
  <script src="{{ url_for('static', filename='js/app.js') }}"></script>
  {% block script %}{% endblock %}
</body>

</html>` 
```
Ok so we've added quite a lot of new code to this HTML file. Let's step through what we've done:

> Tip - If you used the Bootstrap starter template, don't worry about importing any of the Bootstrap or jQuery CSS or JS files as they'll be delivered through the CDN

-   We import the  `bootstrap.min.css`  file in the  `<head>`
-   We then import our custom stylesheet as we did in the last episode
-   We added the  `{% block title %}`  and  `{% endblock %}`  tags between the  `<title> </title>`  tags
-   We added the  `{% block main %}`  and  `{% endblock %}`  tags between the  `<main> </main>`  tags
-   We imported the  `jquery.slim.min`  library
-   We imported the  `bootstrap.bundle.min.js`  library
-   We imported out custom JavaScript file down at the bottom just like in the last part of the series
-   Finally, we added the  `{% block script %}`  and  `{% endblock %}`  tags just before the closing  `</body>`  tag

You'll notice we use the syntax  `{% block something %} {% endblock %}`  to declare our blocks.

We'll later fill in these blocks when we import this template into our child templates.

You can name a block whatever you like, however you can only use a block name once.

We should add a navigation bar to our  `public_template.html`  template. Add the following just below the opening  `<body>`  tag:

**app/app/templates/public/templates/public_template.html**
```html
`<nav class="navbar navbar-expand-lg navbar-light bg-light mb-3">
  <a class="navbar-brand" href="#">Flask</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item">
        <a class="nav-link" href="/">Home</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="/about">About</a>
      </li>
    </ul>
  </div>

  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav ml-auto">
      <li class="nav-item">
        <a class="nav-link" href="/admin/dashboard">Admin</a>
      </li>
    </ul>
  </div>

</nav>` 
```
Ok great, now we've got a nice navbar! Let's create a child template and put our blocks to use.

### Child templates

A child template will inherit all of the HTML from the base template and fill in the areas where we declared our blocks.

Let's refactor  `index.html`  to be our first child template. Go ahead and open it up in an your editor and enter the following:

**app/app/templates/public/index.html**
```html
`{% extends "public/templates/public_template.html" %}

{% block title %}Home{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">
      <h1>Home</h1>
    </div>
  </div>
</div>

{% endblock %}` 
```
Let's look at what we've done.

-   We use the  `{% extends "path/to/our/template.html" %}`  syntax to import a base template
-   `{% block title %}Home{% endblock %}`  will set the page title
-   Then we fill in the blocks we declared in our base template by once again, using the  `{% block something %} {% endblock %}`  syntax

Anything inside our named blocks will be plugged into our base template!

Let's throw in some JavaScript into the  `{% block script %}`  tags and see what happens.

At the bottom of  `index.html`  add the following:
```html
`{% block script %}
<script>
  alert("Template inheritance is awesome");
</script>
{% endblock %}` 
```
Save the file and reload your browser window.

You should see the JavaScript alert dialogue pop up! Go ahead and close it and remove the  `{% block script %}`  and containing JavaScript we just added.

> Tip - Inspect the page HTML by hitting  `Ctrl + u`  to open up a new tab showing the source code to get a better understanding of what's happening

As you can see, our  `index.html`  file doesn't contain any of the boilerplate HTML we added in our base template. That's because  `index.html`  inherits all the contents of the base template, in our case it's inheriting everything from  `public_template.html`

So we've got our base template for our public views. Let's do the same with our admin views by creating a new base template and refactoring our  `dashboard.html`  file to become a new child template.

### Additional templates

Open up  `admin_template.html`  and add the following:

**app/app/templates/admin/templates/admin_template.html**
```html
<!doctype html>
<html lang="en">

<head>
  <!-- Required meta tags -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

  <!-- Import the Bootstrap stylesheet -->
  <link rel="stylesheet" href="{{ url_for('static', filename='css/bootstrap.min.css') }}">
  <!-- Import our custom stylesheet -->
  <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">

  <title>{% block title %}{% endblock title %}</title>
</head>

<body>

  <nav class="navbar navbar-expand-lg navbar-light bg-light mb-3">
    <a class="navbar-brand" href="#">Admin</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" href="/admin/dashboard">Dashboard</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="/admin/profile">Profile</a>
          </li>
      </ul>
    </div>

    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <a class="nav-link" href="/">Return to site</a>
        </li>
      </ul>
    </div>

  </nav>

  <main>
    {% block main %}{% endblock main %}
  </main>

  <!-- Import jquery 3.3.1 slim min -->
  <script src="{{ url_for('static', filename='js/jquery.slim.min.js') }}"></script>
  <!-- Import Bootstrap bundle -->
  <script src="{{ url_for('static', filename='js/bootstrap.bundle.min.js') }}"></script>
  <!-- Import our custom JavaScript -->
  <script src="{{ url_for('static', filename='js/app.js') }}"></script>
  {% block script %}{% endblock %}
</body>

</html>` 
```
We haven't changed much here, just a few tweaks to the navbar.

Now we need to refactor our  `dashboard.html`  file in the  `templates/admin`  directory to become a new child template.

Open up  `dashboard.html`  in your browser and change it to the following:

**app/app/templates/admin/templates/admin_template.html**
```html
`{% extends "admin/templates/admin_template.html" %}

{% block title %}Admin dashboard{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">
      <h1>Admin dashboard</h1>
    </div>
  </div>
</div>

{% endblock %}` 
```
Save the file and head back to your browser window.

If you now click on the  `Admin`  link in the top right of the navbar, you'll be taken to the admin dashboard page where you'll see our new base and child templates in action!

### Code challenge

If you're feeling comfortable, go ahead and create the 2 new child templates and inherit from their corresponding base templates for the 2 routes:

-   The  `about`  route in  `views.py`
-   The  `profile`  route in  `admin_views.py`

> Tip - You'll need to create 2 new HTML files and modify the routes!

### Key takeaways

Creating base templates and extending them in child templates is a great way to streamline your HTML files and create reusable code that's repeatable and reliable.

Keep the following procedure in mind:

-   Your base templates should contain your reusable code
-   Declare named block sections in your base templates using the  `{% block something %} {% endblock %}`  syntax
-   Create child templates that  `extends`  your base templates and plug the blocks with the corresponding block names

There's still lots more to cover on Jinja! You'll learn more about working with Python, Flask and Jinja in the next part of this series.

Last modified  ·  28 Feb 2019

> Written with [StackEdit](https://pythonise.com/series/learning-flask/jinja-template-inheritance).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDg4ODA0OTRdfQ==
-->