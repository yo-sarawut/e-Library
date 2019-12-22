# Your first Flask app | Learning Flask Ep. 1

In the first part of this series, you'll learn how to create and run your very first Flask web application

### Creating a project directory and virtual environment

First of all, we need to create our new project directory. We're going to a new directory called  `app`  in our home directory.

> Tip - I advise using the same names for your project so it's easier to follow along

Go ahead and create the directory with the following:

`mkdir ~/app` 

Next, let's move into the  `app`  directory:

`cd ~/app` 

Now we need create out Python virtual environment. Do so with the following command:

`python -m venv env` 

This will create a new virtual environment called  `env`

You'll see a new directory appear inside the  `app`  directory called  `env`. Now we need to activate our virtual environment before we install Flask.

Go ahead and run the following command to activate the environment:

`source env/bin/activate` 

You should see  `(env)`  appear in front of your terminal prompt indicating the virtual environment is activated!

### Updating pip

It's best practice to update pip (Python's package manager) after creating a new virtual environment. We can do so with the following:

`pip install --upgrade pip` 

You should see a success message like the following

`Collecting pip
  Using cached https://files.pythonhosted.org/packages/46/dc/7fd5df840efb3e56c8b4f768793a237ec4ee59891959d6a215d63f727023/pip-19.0.1-py2.py3-none-any.whl
Installing collected packages: pip
  Found existing installation: pip 18.1
    Uninstalling pip-18.1:
      Successfully uninstalled pip-18.1
Successfully installed pip-19.0.1` 

Now we're ready to install Flask!

### Installing Flask

You install Flask just as you would any other Python package.

`pip install flask` 

If we now run  `pip list`, you'll see the following:

`Package      Version
------------ -------
Click        7.0
Flask        1.0.2
itsdangerous 1.1.0
Jinja2       2.10
MarkupSafe   1.1.0
pip          19.0.1
setuptools   40.6.2
Werkzeug     0.14.1` 

> Note - Flask comes with several other packages so don't be alarmed when you see  `MarkupSafe`  or  `itsdangerous`!

Ok so we've got everything we need to start building our very simple application. Let's get to it.

### Creating a Flask app

This guide is just to show you the most basic Flask application possible. You'll learn the correct way to structure a Flask application over the next couple of parts in this series.

The most basic Flask app can be just a single file. We're going to call it  `app.py`. Make sure you're in the  `app`  directory and run the following to create it:

`touch app.py` 

Let's write some code! Go ahead and open up  `app.py`  in your favourite editor and follow along.

First of all, we need to import  `Flask`  from  `flask`

`from flask import Flask` 

Now we need to create our  `Flask`  application. We're going to pass  `__name__`  to  `Flask`  and assign it to the variable  `app`

Don't worry about exactly why we're doing this. We'll cover it in a more advanced episode in this series.

`from flask import Flask

app = Flask(__name__)` 

Next up, we need to create a route or view (route and view are used interchangeably)

Let's create a route and explain it line by line after:

`from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello world!"` 

Let's talk through the 3 lines we just added:

`@app.route("/")` 

Routes in Flask are created using the  `@app.route`  decorator and passing in a URL or path.

In this example, we've passed  `"/"`  into the  `@app.route`  decorator.  `"/"`  is the root of the website or application.

This route will be triggered when someone goes to the root or index of our website, for example  `http://example.com`.

`def index():
    return "Hello world!"` 

Under the  `@app.route`  decorator, we simply write a standard Python function with a  `return`  statement.

Flask will return whatever we pass to the  `return`  statement! In this case, just a short  `"Hello world!"`  string.

We need to add 2 more lines of code before we can run our app. Add the following:

`from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello world!"

if __name__ == "__main__":
    app.run()` 

Let's take a look at what we added:

`if __name__ == "__main__":
    app.run()` 

Again, I don't want you to worry too much about what's happening here. For now just know that  `__name__`  is a special variable used by the Python interpreter to understand if a file is the main program.

Just as we passed  `__name__`  into the  `Flask()`  class, the special variable  `__name__`  is equal to  `__main__`. You'll learn more about this principle as you advance through the series.

### Running the Flask app

Time to see the app in action! We can run our Flask app in a couple of ways.

In your terminal, make sure you're in the same directory as  `app.py`  and run the following:

`python app.py` 

You'll see the following message in your terminal to let you know Flask is running:

 `* Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
127.0.0.1 - - [03/Feb/2019 14:35:04] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [03/Feb/2019 14:35:04] "GET /favicon.ico HTTP/1.1" 404 -` 

Great, our app is running! Ignore any of the warning messages in your terminal and open up a new browser tab and head to the following URL:

[http://127.0.0.1:5000/](http://127.0.0.1:5000/)

You should see  `Hello world!`  in your browser!

Head back over to your terminal and stop the app by hitting  `Ctrl + c`

So you've seen one way to run your Flask app but it's not recommended. There's a better way.

### Flask environment variables

To make running our app even easier, we're going to set a couple of environment variables in our shell. Run the following commands and we'll talk through them after:

`export FLASK_APP=app.py
export FLASK_ENV=development` 

Running  `export FLASK_APP=app.py`  will set the  `FLASK_APP`  variable to  `app.py`

Running  `export FLASK_ENV=development`  tells Flask we want to run our app in development mode

> Warning - Never run a live Flask application in production using development mode

We're quite a way from deploying our app to the web but I want to drill it home early, just so you know. We'll cover the reasons why later in the series.

We can now run our app using the following simple command:

`flask run` 

You'll see:

 `* Serving Flask app "app.py" (lazy loading)
 * Environment: development
 * Debug mode: on
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 201-167-879` 

You'll notice we don't get any of the warnings and that  `Environment`  is set to  `development`

Head back to  [http://127.0.0.1:5000/](http://127.0.0.1:5000/)  and you'll see the same  `Hello world!`  message as before.

Use  `Ctrl + c`  in your terminal to stop the app when you're ready.

To deactivate your virtual environment, simply enter:

`deactivate` 

### Wrapping up

You now know how to create and run a very basic Flask application, along with some best practices for setting environment variables and using the  `flask run`  command.

Next up, learning how to structure your Flask application properly!

Last modified  ·  28 Feb 2019


> Written with [StackEdit](https://pythonise.com/series/learning-flask/your-first-flask-app#creating-a-project-directory-and-virtual-environment).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY1MTEzNjYzNF19
-->