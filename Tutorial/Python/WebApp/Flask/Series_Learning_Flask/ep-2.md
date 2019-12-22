
# Flask application structure | Learning Flask Ep. 2

Structuring your Flask application for

In this part of the Learning Flask series, you'll learn how to structure files and directories in your Flask application.

Flask is a very flexible framework and doesn't enforce that you follow any specific pattern for structuring your application. However there are some best practices and tips to make sure you don't run into issues down the line as your application grows!

Like I said, there's many ways to setup your structure. This is a pattern I've been using for the last couple of years and has worked very well for me.

Let's get started.

### You application as a package

By far the most popular way to structure your application is by using the package method, where we define our Flask application as a package and can import it! Just like we would any other Python package.

The package method allows you much more flexibility, as we can split our application up into multiple logical files, making working with our app much cleaner and easier to navigate.

As this is a beginner series, we're going to expand from our simple, single file application and break it up into multiple files and package it up.

In the last part of this series, we created a single directory called  `app`  in our home directory containing a single file called  `app.py`.

Let's take a look at how our new project structure is going to look from inside our  `app`  project directory:

```
├── app
│   ├── __init__.py
│   └── views.py
├── env
├── requirements.txt
└── run.py` 
```
We're going to go through each file step by step. But for now, let's go ahead and create our structure!

Make your way to the  `app`  directory you created in your home folder:

`cd ~/app` 

Running the  `ls`  command, your should see the single  `app.py`  file along with the virtual environment direcory named  `env`

We're going to keep our virtual environment but delete  `app.py`  and start from scratch. Delete the file with the following:

`rm app.py` 

While we're here in the root of our  `app`  directory. Go ahead and create a file called  `run.py`

We'll use this file as the entrypoint to our Flask app.

Now create another directory called  `app`  and move into it. This is going to contain our Flask application and become our package

`mkdir app
cd app` 

Once we're in our newly created  `app`  directory, we need to create the  `__init__.py`  and  `views.py`  files:

`touch __init__.py views.py` 

Great, we've created our basic application structure. Let's go through each file, add some code and explain what we've done.

We'll start with the  `__init__.py`  file. Go ahead and open it up in an editor and enter the following:

**app/app/__init__.py**
```py
from flask import Flask

app = Flask(__name__)

from app import views` 
```
You'll be familiar with the first 2 lines, just like we did in the last episode we're importing Flask and setting our  `app`  variable, however you'll noticed we've added  `from app import views`  at the bottom.

Using this method, we can import multiple python files into our Flask app (as you'll see later)

Think of the  `__init__.py`  file as a contructor that pulls all of the parts of our application together into a package and then tells Python to treat it as a package!

Now, let's add some views in  `views.py`

**app/app/views.py**
```py
`from app import app

@app.route("/")
def index():
    return "Hello world"` 
```
Just like in our first app, we're creating a new view using the  `@app.route`  decorator and passing it a URL. The only difference is the  `from app import app`  statement at the top of the file.

We're actually importing the  `app`  variable we created in the  `__init__.py`. Meaning we can access it anywhere in our package!

Let's add another view and pass it a different URL:

**app/app/views.py**

`from app import app

@app.route("/")
def index():
    return "Hello world"

@app.route("/about")
def about():
    return "All about Flask"` 

We've added another route with the URL  `"/about"`, changed the function name to  `about`  and then told it to return  `"All about Flask"`

> Tip - Routes in Flask must always start with a  `/`  slash

You'll learn more about routing in the next few parts of this series!

Before we can run our app, we need to create an entrypoint. This is where we'll instruct our app to run.

Go back up one directory into the parent  `app`  folder, open up  `run.py`  and add the following:

**app/run.py**

`from app import app

if __name__ == "__main__":
    app.run()` 

We're importing the  `app`  variable from the  `app`  package that we've just created.

We're then calling the  `app.run()`  method, just like in the previous tutorial by wrapping it in an  `if __name__ == "__main__":`  block.

Before we run our app, we need to set our environment variables

### Flask environment variables

> Tip - If you deactivated the virtual environment. Go ahead and re-activate it with  `source env.bin/activate`  from within the parent  `app`  directory

Just like last time, we're going to set 2 environment variables:

`export FLASK_APP=run.py
export FLASK_ENV=development` 

We've set the  `FLASK_APP`  variable to  `run.py`  which is our Flask entry point.

### Running our app

Run the app with the following:

`flask run` 

You'll see the following message, just like last time:

 `* Serving Flask app "run.py" (lazy loading)
 * Environment: development
 * Debug mode: on
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 306-421-612` 

Open up a new browser tab and head to:

[http://127.0.0.1:5000/](http://127.0.0.1:5000/)

You'll see our "Hello world!" message just as before.

Now head over to the other route we created at  [http://127.0.0.1:5000/about](http://127.0.0.1:5000/about)

You should see "All about Flask"

Boom! We're up and running with our application as a package.

Let's add some more views in another file and import them into our  `__init__.py`  file.

### Splitting up views

Let's say we want an admin section of our app. Rather than stuffing all of our views into one folder, let's separate them out into their own seperate file.

Stop your app by hitting  `Ctrl + c`  in your terminal.

Move into the  `app`  package directory

`cd app` 

Create a new file called  `admin_views.py`

`touch admin_views.py` 

Your project file structure should now look like this:

`.
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   └── views.py
└── run.py` 

Open up  `admin_views.py`  and add the following:

**app/app/admin_views.py**

`from app import app

@app.route("/admin/dashboard")
def admin_dashboard():
    return "Admin dashboard"` 

We've done exactly the same as what we did in  `views.py`. Imported  `app`  from  `app`  and declared a new route.

You'll also notice the URL is longer and contains 2 parts! You'll learn all about routing in detail later on in this series.

But before we can access this new route, we need to import  `admin_views.py`  in out  `__init__.py`  file.

Got ahead and open up  `__init__.py`  and  `from app import admin_views`  down at the bottom. It should then look like this:

**app/app/__init__.py**

`from flask import Flask

app = Flask(__name__)

from app import views
from app import admin_views` 

Save the file and head back to the root  `app`  directory containing  `run.py`. It's time to run our app again.

Once there, run the following command to run the app:

`flask run` 

Open up your browser. Let's check out our new admin route.

[http://127.0.0.1:5000/admin/dashboard](http://127.0.0.1:5000/admin/dashboard)

You'll see "Admin dashboard", just like we told the view to return!

We're still missing our  `requirements.txt`  file from our original structure. Let's go ahead and generate it with  `pip`

Hit  `Ctrl + c`  to stop your application.

### Requirements

From the root  `app`  directory, run the following command:

`pip freeze > requirements.txt` 

This command will create a  `requirements.txt`  file and place it in our current directory, listing all of the packages we've installed.

It will look like this:
```
Click==7.0
Flask==1.0.2
itsdangerous==1.1.0
Jinja2==2.10
MarkupSafe==1.1.0
Werkzeug==0.14.1` 
```
> Tip - To install packages from a  `requirements.txt`  file, run  `pip install -r requirements.txt`

### Wrapping up

Awesome. You've learned how to structure your Flask application as a package, break out your code into separate files and work with  `requirements.txt`  files.

Next up, You'll learn how to build a website and render HTML files!

Last modified  ·  28 Feb 2019



> Written with [StackEdit](https://pythonise.com/series/learning-flask/flask-application-structure).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5MjYxMzIwMl19
-->