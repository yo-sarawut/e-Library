# Serving HTML files \| Learning Flask Ep. 3

How to render HTML files and structure template directories with Flask

In this part of the Learning Flask series, you'll learn how to work with and serve HTML files.

Flask provides a fast and easy way for us to serve static files! So building a simple website is a breeze.

We're going to pick up the same application we created in the last episode and build upon it. If you haven't read the last part of this series, I'd suggest doing so. If not, this is how our current application structure looks:

```text
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   └── views.py
├── requirements.txt
└── run.py`
```

Ready to code? Fire up a new terminal and browser windows and let's get started.

## Launch your app

From the root `app` directory, start Flask with the following command:

`flask run`

In your browser, head to [http://127.0.0.1:5000/](http://127.0.0.1:5000/) to see "Hello world!" at our app index route

Ok so the app is up and running. Now let's start rendering some HTML.

Before we start working with any HTML files, I want to show you how we can return HTML from a flask view.

Go ahead and open up `views.py` in your favourite editor. You should see the following:

**app/app/views.py**

```python
from app import app

@app.route("/")
def index():
    return "Hello world"

@app.route("/about")
def about():
    return "All about Flask"`
```

Let's modify the `about` route to return some HTML by simple passing an HTML string to `return`

```python
`from app import app

@app.route("/")
def index():
    return "Hello world"

@app.route("/about")
def about():
    return "<h1 style='color: red;'>I'm a red H1 heading!</h1>"`
```

> Tip - Flask will automatically reload when we make changes to any of the Python files assosiated with our app!

Go to `/about` in your browser to see the changes. You'll see a big red H1 heading at the top of the page!

We can also pass a multi line string of HTML to `return`, let's do that now:

```python
`from app import app

@app.route("/")
def index():
    return "Hello world"

@app.route("/about")
def about():
    return """
 <h1 style='color: red;'>I'm a red H1 heading!</h1>
 <p>This is a lovely little paragraph</p>
 <code>Flask is <em>awesome</em></code>
 """`
```

Cool right? But not very practical.

To make things a bit more fun, let's learn how to serve HTML files with Flask.

## Serving HTML files

Flask provides a very simple way for us to return HTML files to the client/browser, using the `render_template` function.

However, before we start using this function, we need to create some new files and directories.

Flask looks for a directory called `templates` in the root of the Flask application package. Let's go ahead and create it now.

Stop the app with `Ctrl + c`

Move into the `app` directory with:

`cd app`

Create the `templates` directory and move into it:

```text
mkdir templates
cd templates
```

Let's create a template called `index.html`:

`touch index.html`

Open up `index.html` in your editor and add the following:

```markup
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Index</title>
</head>

<body>
  <h1 style="color: blue">Index</h1>
  <p>This is an HTML file served up by Flask</p>
</body>

</html>
```

It's not going to win any design awards but will illustrate how to render HTML files!

Save and close the file.

Your project file structure should now look like the following:

```text
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── templates
│   │   └── index.html
│   └── views.py
├── requirements.txt
└── run.py
```

In your terminal, navigate back to the root `app` directory containing `run.py` and run the `flask run` command to restart the app.

Before we can start serving up any HTML files, we need to import `render_template` from Flask. Go ahead and add the following import to the top of `views.py`

**app/app/views.py**

`from flask import render_template`

> Tip - Flask provides many useful functions that you'll be learning about throughout this series

Next up, we need to tell our view to serve up the HTML file we just created. Let's serve `index.html` using the `index` route.

To return an HTML template, we use the following syntax:

`return render_template("index.html")`

Flask will look in the `templates` directory we've just created for `index.html` \(It's the default place Flask will go to look for HTML files when the `render_template` function is called\)

Your `views.py` file should now look like this:

```python
from app import app

from flask import render_template

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/about")
def about():
    return """
 <h1 style='color: red;'>I'm a red H1 heading!</h1>
 <p>This is a lovely little paragraph</p>
 <code>Flask is <em>awesome</em></code>
 """`
```

Go to `/index` in your browser at [http://127.0.0.1:5000/](http://127.0.0.1:5000/) to see your HTML masterpiece.

Nice work. You've rendered your first HTML page with Flask!

Just like how we split our views into multiple files, we can do something similar to our HTML template directories to make our life easier and working with our files more manegable.

In the last episode, we created an `admin_views.py` file to contain all of our admin routes.

Let's refactor our template directories and files to reflect that change.

## Template directories

Our new file structure is going to look like the following:

```text
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── templates
│   │   ├── admin
│   │   │   └── dashboard.html
│   │   └── public
│   │       └── index.html
│   └── views.py
├── requirements.txt
└── run.py`
```

We're going to create 2 new directories within our `templates` directory:

* public - Will contain all of the HTML files we want to serve from  `views.py`
* admin - Will contain any HTML files we'll serve from our admin routes in  `admin_views.py`

This keeps things separated and easy for us to navigate and work with.

In the terminal, stop the app with `Ctrl + c` and move into the templated directory with:

`cd app/templates/`

Now we'll create our 2 new directories:

`mkdir public admin`

We then need to move our `index.html` file into the `public` directory. Do so with:

`mv index.html /public`

Whilst we're here, let's create a new file in `admin` called `dashboard.html`

`cd admin touch dashboard.html`

Once again, your app structure should now look like this:

```text
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── templates
│   │   ├── admin
│   │   │   └── dashboard.html
│   │   └── public
│   │       └── index.html
│   └── views.py
├── requirements.txt
└── run.py`
```

Before we add any HTML to `dashboard.html`. Let's refactor our view in `views.py` to serve `index.html` from the newly created directory.

Open up `views.py`. We're going to change the path to the file we want to serve in `render_template`.

Change this:

**app/app/views.py**

```python
`@app.route("/")
def index():
    return render_template("index.html")`
```

To this:

**app/app/views.py**

```python
`@app.route("/")
def index():
    return render_template("public/index.html")`
```

We've changed `"index.html"` to `"public/index.html"` to reflect our new directory structure.

Start up your app and reload your browser to test everything works.

Awesome! We've separated our HTML templates into something more logical and easy to manage.

Let's add some HTML to `dashboard.html` and refactor our `admin_views.py` file. Just like we just did with `views.py`

Open up `dashboard.html` and add the following:

**app/app/templates/admin/dashboard.html**

```markup
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Dashboard</title>
</head>

<body>
  <h1 style="color: green">Admin dashboard</h1>
  <p>This HTML file is served from the admin templates directory</p>
</body>

</html>
```

Save and close the file.

We now need to refactor the route in `admin_views.py`. Open the file and make the following changes.

First up, we need to import `render_template`. Add the following to the top of `admin_views.py`

**app/app/admin\_views.py**

`from flask import render_template`

We then need to change our file path in the `render_template` function.

From this:

```python
@app.route("/admin/dashboard")
def admin_dashboard():
    return render_template("dashboard.html")
```

To this:

```python
@app.route("/admin/dashboard")
def admin_dashboard():
    return render_template("admin/dashboard.html")
```

Save the file and go to `admin/dashboard` in your browser to see the changes.

And we're done! We've split up our app and created a logical file structure within our app.

If you're feeling adventurous, I want you to try the following:

* Create a new Python file containing a new view
* Import that file into the  `__init__.py`  file
* Create a new template directory for those views
* Add an HTML template to it
* Render that template

If you're not feeling ready for that just yet, it's no worries! Contunie working your way through the series and you'll soon be building Flask apps of your own.

## Wrapping up

A Flask application can be as simple or as complex as you want it to be.

You can put all of your views into a single file or break them up into separate logical files, likewise with templates, you can keep them all together of split them up into corresponding directories.

The beauty of Flask is that it's all up to you.

In the next part of this series, you'll be learning how to serve static files including images, CSS and Javascript.

Last modified · 28 Feb 2019

> Written with [StackEdit](https://pythonise.com/series/learning-flask/rendering-html-files-with-flask).

