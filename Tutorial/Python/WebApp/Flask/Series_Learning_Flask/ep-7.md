
# Working with forms in Flask | Learning Flask Ep. 7

Creating forms, posting data to views and working with form data in Flask

In this part of the Learning Flask series, You'll learn how to post forms to a Flask view and work with the incoming data.

Forms (or input data in general) play a critical role in any kind of website or web allication as we need a way for the user to communicate with our app!

In this example, we'll start with a simple account sign-up form.

### Creating a new route

Let's get started by creating a new route in  `views.py`. We'll give it the URL  `sign-up`.

**app/app/views.py**
```py
@app.route("/sign-up")
def sign_up():
    return render_template("public/sign_up.html")
```
We're going to be accepting  `POST`  requests on this route so we need to pass another argument to  `@app.route`

We do this by passing the  `methods`  argument, along with a list of methods as the value.

Flask supports all of the common HTTP methods including:

-   `GET`
-   `POST`
-   `PUT`
-   `DELETE`

Let's privide our route with the  `methods`  argument and a list of methods we want the route to handle:

**app/app/views.py**
```py
@app.route("/sign-up", methods=["GET", "POST"])
def sign_up():
    return render_template("public/sign_up.html")
```
> Tip - Flask routes support  `GET`  requests by default, however must be declared if the  `methods`  argument is provided

We need to create a new template so go ahead and create a new file called  `sign_up.html`  and place it in the  `templates/public`  directory.

Open up  `sign_up.html`  in your editor and add the following:

**app/app/templates/public/sign_up.html**
```py
{% extends "public/templates/public_template.html" %}

{% block title %}Sign up{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">
      <h1>Sign up</h1>
      <hr>
    </div>
  </div>
</div>

{% endblock %}
```

Save the file and open go to the  `/sign-up`  route in your browser. You should see the new page render.

Let's create a form and add some input fields to our template. We're going to add fields for username, email and pasword. Go ahead and enter the following just under the  `<hr>`  tag:

**app/app/templates/public/sign_up.html**
```html
<form action="/sign-up" method="POST">

  <div class="form-group">
    <label>Username</label>
    <input type="text" class="form-control" id="username" name="username" placeholder="Select a username">
  </div>

  <div class="form-group">
    <label>Email</label>
    <input type="email" class="form-control" id="email" name="email" placeholder="Enter your email">
  </div>

  <div class="form-group">
    <label>Password</label>
    <input type="password" class="form-control" id="password" name="password" placeholder="Create a password">
  </div>

</form>` 

Lastly, we need to add a submit button. Add it just befor the closing  `</form>`  tag:

**app/app/templates/public/sign_up.html**

`<button type="submit" class="btn btn-primary">Sign up</button>` 

Your template should now look something like this:

**app/app/templates/public/sign_up.html**

`{% extends "public/templates/public_template.html" %}

{% block title %}Sign up{% endblock %}

{% block main %}

<div class="container">
  <div class="row">
    <div class="col">

      <h1>Sign up</h1>
      <hr>

      <form action="/sign-up" method="POST">

        <div class="form-group">
          <label>Username</label>
          <input type="text" class="form-control" id="username" name="username" placeholder="Select a username">
        </div>

        <div class="form-group">
          <label>Email</label>
          <input type="email" class="form-control" id="email" name="email" placeholder="Enter your email">
        </div>

        <div class="form-group">
          <label>Password</label>
          <input type="password" class="form-control" id="password" name="password" placeholder="Create a password">
        </div>

        <button type="submit" class="btn btn-primary">Sign up</button>

      </form>

    </div>
  </div>
</div>

{% endblock %}` 
```
> Tip - To access form data in Flask, you must provide the  `name`  attribute in each of the forms  `input`  tags

Pay attention to the opening  `<form>`  tag.

We pass the URL of the route we want to post the form data to in the  `action`  attribute of the form. In our case  `action="/sign-up"`.

You'll also need to pass the request method to the  `method`  attribute in the opening  `<form>`  tag. We've added  `method="POST"`  because we're POSTing data to the server.

Save the file and refresh the page to see your form.

### Posting form data to a route

Go ahead and hit the submit button and pay attention to your terminal or console. You'll see:

`127.0.0.1 - - [06/Feb/2019 22:00:25] "POST /sign-up HTTP/1.1" 200 -` 

Perfect, our form is posting to the  `sign-up`  route on our server!

Let's jump back into  `views.py`  and start working with our form data.

### Handling form data

Before we can access any of the request data, we need to import  `request`  from flask.

At the top of  `views.py`, go ahead and import  `request`  from  `flask`. We'll also import  `redirect`

**app/app/views.py**
```py
from flask import request, redirect` 
```
To access form data in our route, we use  `request.form`.

Let's capture our incoming form data to a variable called  `req`, but first, we should add a conditional to validate we're receiving  `POST`  data.

We can do so by testing  `request.method`  for the  `"POST"`  method:

**app/app/views.py**
```py
@app.route("/sign-up", methods=["GET", "POST"])
def sign_up():

    if request.method == "POST":

        req = request.form

        return redirect(request.url)

    return render_template("public/sign_up.html")` 
```
The  `redirect`  function, amongst many other things allows us to redirect the client to different parts our app. We'll be exploring  `redirect`  in more detail in a future part of this series.

In this case, we're instructing  `redirect`  to redirect the client to the URL of the request.

If you were to  `print(type(req))`  you'll see that the  `request.form`  object a special type called  `werkzeug.datastructures.ImmutableMultiDict`  which we can essentially treat it like a dictionary.

Let's just  `print(req)`  and inspect the results.

**app/app/views.py**
```
@app.route("/sign-up", methods=["GET", "POST"])
def sign_up():

    if request.method == "POST":

        req = request.form
        print(req)

        return redirect(request.url)

    return render_template("public/sign_up.html")
```
Depending on whether you supplied any input, you'll see:

`ImmutableMultiDict([('username', ''), ('email', ''), ('password', '')])` 

We can treat our  `req`  object just like a normal Python dictionary, for example, to access the individual inputs from the form, we can use any of the following:

**app/app/views.py**
```py
@app.route("/sign-up", methods=["GET", "POST"])
def sign_up():

    if request.method == "POST":

        req = request.form

        username = req.get("username")
        email = req["email"]
        password = request.form["password"]

        # You could also use 
        password = request.form.get("password")

        return redirect(request.url)

    return render_template("public/sign_up.html")` 
```
You could bypass capturing and storing the form data as a variable with the following:

**app/app/views.py**
```py
@app.route("/sign-up", methods=["GET", "POST"])
def sign_up():

    if request.method == "POST":

        username = request.form.get("username")
        email = request.form.get("email")
        password = request.form.get("password")

        # Alternatively

        username = request.form["username"]
        email = request.form["email"]
        password = request.form["password"]

        return redirect(request.url)

    return render_template("public/sign_up.html")
```
We've now got each of the form values stored as a Python variable to do as we please.

### Validating form data

There's lots of things we could do to validate, however they're very much application specific. Let's keep it simple and just validate that we've got some data for all 3 fields. We'll cover validating a sign up form later in this series.

Let's iterate through the keys and values of our  `req`  object and look for missing fields, then return a response and message to the user:

**app/app/views.py**
```py
@app.route("/sign-up", methods=["GET", "POST"])
def sign_up():

    if request.method == "POST":

        req = request.form

        missing = list()

        for k, v in req.items():
            if v == "":
                missing.append(k)

        if missing:
            feedback = f"Missing fields for {', '.join(missing)}"
            return render_template("public/sign_up.html", feedback=feedback)

        return redirect(request.url)

    return render_template("public/sign_up.html")` 
```
We'll add a message in  `sign_up.html`  to give some feedback to the user. Open up  `sign_up.html`  and add the following just under the  `<button>`  tag inside the form:

**app/app/templates/public/sign_up.html**
```html
{% if feedback %}
<p class="text-danger float-right">{{ feedback }}</p>
{% endif %}` 
```
Save and close the file.

Refresh your browser and submit an empty form. You should see the error message appear to the bottom right of the form. When you submit values for all 3 fields, the feedback message doesn't appear.

We could use the  `required`  attribute in the HTML form and let the browser do the validation for us but that's not much fun is it. And besides, this series is about Flask!

In the next part, you'll be learning about dynamic URL's

Last modified  ·  28 Feb 2019

> Written with [StackEdit](https://pythonise.com/series/learning-flask/flask-working-with-forms).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2ODM0MTQ4NV19
-->