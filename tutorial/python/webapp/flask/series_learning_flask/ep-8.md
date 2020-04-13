# Generating dynamic URLs in Flask \| Learning Flask Ep. 8

Learn how to create and work with dynamic URLs and dynamic data in Flask

Dynamic URL's in Flask play an important role in the ability to create unique URL's that aren't hard-coded into our application.

For example, let's say our application allows users to create an account and log into their profile, we'll need a way to dynamically generate a route for that specific user.

Can you imagine hard coding a unique URL for each and every user of your application?!

Let's dive in and learn how we can generate dynamic URL's in Flask.

## creating a dynamic route

First up, let's create a new route in out app. We're going to give it the URL `/profile`:

**app/app/views.py**

```python
@app.route("/profile")
def profile():
    return render_template("public/profile.html")`
```

We'll also create a new template for this route. Go ahead and create a file named `profile.html` in the `templates/public` directory \(Or whatever directory contains your HTML files\)

Let's just create a simple page for now:

**app/app/templates/public/dynamic.html**

```python
{% extends "public/templates/public_template.html" %}

{% block title %}Profile{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">

      <h1>Profile</h1>
      <hr>

    </div>
  </div>
</div>

{% endblock %}
```

> Tip - We're using the Bootstrap CSS library but feel free to use your own or leave it out completely

As it is, our new route isn't dynamic. We need to make some tweaks to the URL we've provided in out `@app.route` decorator.

Go ahead and make the following changes to the `@app.route` URL:

**app/app/views.py**

```python
@app.route("/profile/<username>")
```

* We've added trailing slash to  `/profile/`
* We've provided a variable in the URL path and wrapped in with two opposing arrows  `<>`  as shown.

Essentially, we're expecting some sort of value to be passed into the URL after `/profile/`. We're then capturing that data as a variable called `username`.

Just remember, to catch a a value in the URL and store it as a variable it must look `<like_this>` and follow a trailing slash.

Before we can work with the `username` data, we need to pass it into the routes function as an argument:

**app/app/views.py**

`def profile(username):`

We now have access to the `username` variable and its data.

For clarity, our route now looks like this:

**app/app/views.py**

```python
@app.route("/profile/<username>")
def profile(username):
    return render_template("public/profile.html")
```

At this point, if you try to access the `/profile` route in your browser, Flask will throw an error because the `profile` function is expecting an value!

> Tip - Trailing slashes matter in Flask. If you try to access a route that's not defined with a trailing slash in the URL, you'll get an error.

## Capturing URL variables

Go to `/profile/x` in your browser. You'll see Flask returns our new `profile.html` page and displays `/profile/x` in the browser URL address bar.

We can now work with data that comes into our app from the URL! Let's create a dictionary containing a few usernames and some information about our users.

We'll search the dictonary for the `username` variable and return some basic information about that user. Let's create our `users` dictionary:

**app/app/views.py**

```python
users = {
    "mitsuhiko": {
        "name": "Armin Ronacher",
        "bio": "Creatof of the Flask framework",
        "twitter_handle": "@mitsuhiko"
    },
    "gvanrossum": {
        "name": "Guido Van Rossum",
        "bio": "Creator of the Python programming language",
        "twitter_handle": "@gvanrossum"
    },
    "elonmusk": {
        "name": "Elon Musk",
        "bio": "technology entrepreneur, investor, and engineer",
        "twitter_handle": "@elonmusk"
    }
}
```

We'll add some logic to our `profile` route to look up the user and return their information:

**app/app/views.py**

```python
@app.route("/profile/<username>")
def profile(username):

    user = None

    if username in users:
        user = users[username]

    return render_template("public/profile.html", username=username, user=user)
```

Lastly, let's refactor our `profile.html` to display our user information:

**app/app/templates/public/dynamic.html**

```python
{% extends "public/templates/public_template.html" %}

{% block title %}Profile{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">

      <h1>Profile</h1>
      <hr>

      <div class="card">
        <div class="card-body">
          {% if user %}
          <h5 class="card-title">{{ username }}</h5>
          <hr>
          <p><strong>{{ user["name"] }}</strong></p>
          <p style="color: blue">{{ user["twitter_handle"] }}</p>
          <p class="text-muted">{{ user["bio"] }}</p>
          {% else %}
          <p>User {{ username }} not found</p>
          {% endif %}
        </div>
      </div>

    </div>
  </div>
</div>

{% endblock %}
```

## Requesting a dynamic route

Save the files and head to `/profile/mitsuhiko` or any of the other usernames in your browser to see their profile!

![Dynamic URLs in Flask](https://pythonise.com/static/img/uploads/dynamic-url-example.PNG)

Also, try a name that's not in our dictionary to see how we've handled that with a simple \`

\` statement in our template.

Dynamic URL's aren't just limited to one variable. Let's stack some more veriables to capture in our URL string.

## Multiple URL variables

In our first example, we created the `profile` route to expect only one variable in the URL. However, we can add as many as we like.

Let's create a new route with multiple variables that just prints the variables and returns a simple string to the client:

**app/app/views.py**

```python
@app.route("/multiple/<foo>/<bar>/<baz>")
def multiple(foo, bar, baz):

    print(f"foo is {foo}")
    print(f"bar is {bar}")
    print(f"baz is {baz}")

    return f"foo is {foo}, bar is {bar}, baz is {baz}"
```

Go to `/multiple/foo/bar/baz` in your browser, you'll see:

`foo is foo, bar is bar, baz is baz`

As you can see, we have full access to the variables captured in the URL and passed into our function!

In the next part of this series, we'll be covering how to work with query strings in Flask.

Last modified · 28 Feb 2019

> Written with [StackEdit](https://pythonise.com/series/learning-flask/generating-dynamic-urls-with-flask).

