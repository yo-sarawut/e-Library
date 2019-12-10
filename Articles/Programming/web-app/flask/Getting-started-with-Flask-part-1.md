
Getting started with Python Flask framework (Part 1)
===
![enter image description here](https://miro.medium.com/max/1920/1*kvx5ly0fyVyhCYPYpKoOoQ.png)

Flask is a python web framework based on Werkzeug, Jinja2. Flask is easy to understand and also a prerequisite for Django.

## Setting up the Flask (Ubuntu)

Setting up the Flask in Ubuntu is very easy just go to the terminal or press Ctrl+Alt+T , this will open up the terminal and paste the following below commands :-
```
$ sudo apt-get install python  
$ sudo pip install Flask
```
Since Flask is a python web framework, so you have to install Python first and then you can install python Flask Framework.

Note:- All python libraries are installed by using either  **pip install**  or  **easy_install**

Above two commands will install python and flask framework globally.

## Setting up the Flask (Windows)

Windows users needs to install Python from  [_here_](https://www.python.org/downloads/)_._

Also Download & Install Git Bash from below link.

[](https://git-scm.com/download/win?source=post_page-----a4931ce0ea13----------------------)

 
```
Git — Downloading Package
```


You are downloading the latest ( 2.15.1) 64-bit version of Git for Windows. This is the most recent maintained build…


```
git-scm.com
```
Git bash will allow the windows users to run terminal commands in windows operating system. So, After Installing Git Bash Run the below command to install the Flask Framework.
```py
$ pip install Flask
```


## Routing

Modern web applications have beautiful URLs. This helps people remember the URLs, which is especially handy for applications that are used from mobile devices with slower network connections. If the user can directly go to the desired page without having to hit the index page it is more likely they will like the page and come back next time.

So basically a route is just a URL which returns a template to a user.

**Syntax for building a Route**
```
@app.route(“make your url here”)
```
Here “**app**” is just an instance of the Class “**Flask**”.

**Example -**
```
@app.route("/"**)  
AND  
**@app.route("/home")
```
**Add variables to Routes**

Many times we need to send parameters and values in the url’s, either in the form of query parameters or in the relative url.

So we pass parameters in Routes or Url’s. Flask provides us various converters, we can call them as data types, by which we can send different types of values in the url parameters.

Given Below is a list of Converters that Flask supports.

1.  int -**accepts integer values**
2.  float -**accepts floating values**
3.  path -**used for sending slashes or values with slashes**
4.  uuid -**accepts UUID**
5.  string -**it is a default converter and used for sending names or text.**

Example:-
```py
@app.route('/home/<name>')
def home(name):
    return 'your name is %s' % name
@app.route('/home/<int:id>')
def showId(id):
    return 'your is %d' % id
```
Note:- Always remember that all parameters that you sends to the route, they must be passed in there respective functions.

As you can see above, I have made two functions and a route for each of them and i also passed the parameter in their respective functions which i sends to the route.

**URL Building Or Redirect**

Many times we need to redirect the users to a specific page after on happening of an event. So we do this in Flask by using  **url_for** function, this function accepts the name of an function as its first argument to which we want to redirect the user and the number of arguments, which are passed in route of the function to which we want to redirect.

**Example 1**:-
```py
# import the necessary libs & functions 
from flask import Flask, url_for
# Create instance of flask
app = Flask(__name__)
# home function
@app.route('/home/')
def home():
    return 'The project page'
# projects function
@app.route('/projects/')
def projects():
    return url_for('home')
```
**Explantion**

1.  First we need to import  **url_for**  from flask.
2.  Then, we create a instance of flask.
3.  Then, we define some functions.
4.  finally from  **projects**  function, we return  **url_for**  function to redirect the user to the  **home** function

**Example 2:-**

In this example i will show you how to use  **url_for** function to redirect a user to a function which have some parameters in their routes.
```py
# import the necessary libs & functions 
from flask import Flask, url_for
# Create instance of flask
app = Flask(__name__)
# home function
@app.route('/profile/<int:id>')
def myProfile(id):
    return 'The project page'
# projects function
@app.route('/projects/')
def projects():
    return url_for('myProfile', id=1)
```
**Explantion**

1.  First we had imported  **url_for**  from flask.
2.  Then, we create a instance of flask.
3.  Then, we define a function with route parameters and a non parameter function .
4.  Now, in  **projects**  function, we return  **url_for**  function and passed the name of the function as its first argument to which we need to redirect and also we passed an second argument as id because  **myProfile** function have an  **id** parameter in its route and then we assigns 1 to  **id.**

**Note:-** I have assign 1 to  **id** just for showing you that how to pass values to those arguments but you can assign an value to it from your database. Don’t worry we will be cover database part as well in our future coming parts of Flask Series.

**Rendering the Templates**

Generating HTML from within Python is not fun and actually pretty cumbersome because we have to do the HTML escaping on your own to keep the application secure. Because of that Flask configures the  [Jinja2](http://jinja.pocoo.org/)  template engine for you automatically.

So, To render a template you can use the  `render_template()(http://flask.pocoo.org/docs/0.12/api/#flask.render_template)`  method. All you have to do is provide the name of or path to the template and the variables you want to pass to the template engine as keyword arguments.

**Example 1:-**
```py
from flask import Flask, url_for, render_template

@app.route('/home/')
def home():
    return render_template('index.html')
```
**Example 2:-**

In this example I will show you how to pass some values in HMTL templates using Flask  **render_template().**
```py
from flask import Flask, url_for, render_template
@app.route('/user/')
def profile():
    return render_template('proifle.html', title="techkylabs")
```
**Explanation**

1.  First we need to import render_template from flask.
2.  Then , we define a function named  **profile** and returning the render_template function from it.
3.  In render_template we have passed two arguments first name of the HTML template file and Second I have passed  **title**  and assigns  **techkylabs** as its value.
4.  So, what it actually does when user goes to “**/user/**” Url then  **profile** function will trigger up and a  **profile.html** will be rendered to the user and there we can use value of  **title** that we have passed to be displayed in front of the user.

**Note: -** Conventionally, all of our HTML templates are stored in a folder named “templates” in their projects directory. Generally most of the people do this to store their templates but when we have a large scale project then it is not advisable to store all of the HTML templates files in just a templates folder, Infact I also make some folders in my  **templates** folder to store the my HTML templates files.

But In above example I am assuming that you have all of your HTML templates files in your  **templates** folder. Therefore I just typed “**profile.html**” which is the name of the template in my case, otherwise I need to specify the full path with the template name as the first argument of  **render_template**.

**profile.html**
```html
<!DOCTYPE html>  
<html>  
<head>  
 <title>Techkylabs</title>  
</head>  
<body><h1> hi {{ title }} </h1></body>  
</html>
```
So when this template will render to the user, then it will show  **hi techkylabs**

**Note:-** When we generate HTML template from python then we need to use Jinja to print or show something that is being generated from python, In my case I used  **{{}}** to print the value of title.

**Commonly used Jinja**

1.  {{}} We used dual curly braces when we need to just print something.

2. {% %} We used this wired braces with % when we need to print values of a list or also when we need to check if then else conditions in templates.

**Note:-** Always remember one thing that when we use  **{% %}** in our template then we need to close this as  **{% end %}**.

**Example with {% %} in templates :-**

First we write the code to render a template and passed a list of users to the template.
```py
from flask import Flask, url_for, render_template
@app.route('/user/')
def profile():
 users = [
  'Techkylabs',
  'Rishabh'
 ]
 return render_template('profile.html', names=users)
```
Now in our template we will print all of the users that we have just passed.
```html
<!DOCTYPE html>
<html>
<head>
 <title>Techkylabs</title>
</head>
<body>
<h1>Hello All</h1>
{% for name in names %}
  <p>{{ name }}</p>
{% endfor %}
</body>
</html>
```
So this is what i was talking about that we need to close the tag with a special  **end**.

Above template will print all of the users name.

Let us quickly wrap it up
```py
# Importing the Libraries & Functions
from flask import Flask, render_template, url_for
# Creating an instance of Flask
app = Flask(__name__)
# A route without parameter
@app.route('/')
@app.route('/home')
def home():
    return 'Hello World!'
# A route with parameter
@app.route('/home/<int:id>')
def myId(id):
    return 'hello my id is %d' % id
@app.route('/user/')
def profile():
    return render_template('proifle.html', title="techkylabs")
# projects function
@app.route('/projects/')
def projects():
    return url_for('home')
# home function
@app.route('/profile/<int:id>')
def myProfile(id):
    return 'The project page id is %d' %id
# projects function
@app.route('/projects/')
def projects():
    return url_for('myProfile', id=1)
if __name__ == '__main__':
  app.run(host='0.0.0.0', port=8080, debug=True)
```
Explanation to above python script

1.  First import the Flask from flask library
2.  Create an instance of Flask
3.  Define some functions that returns an Http response when user hits Url.
4.  In “**app.run()”** we set host equals to  **‘0.0.0.0’**  , set port number equals to  **‘8080’** & set debug equals to  **“True”**

Note:- When you set Debug equals to True then it will refresh your server when anything gets changed in your python script and ‘**0.0.0.0**’ means global IP address, you can also set it to  **‘localhost’** & last thing was port number which you can set anything above 1000.

`__name__`  is just a convenient way to get the import name of the place the app is defined. Flask uses the import name to know where to look up resources, templates, static files, instance folder, etc.

So, Now you can go ahead and run the above python script.

1.  Open up the terminal.
2.  Change the directory to where you stored your script.
3.  Run the script as ‘**python your_script_name.py’**.
4.  Now open your browser and type  **‘localhost:8080’** and you should see the  **‘hello World!’.**

So this is small tutorial to get started with python flask. Stay tunned with us to learn more about flask framework.


> Source :  [medium.com](https://medium.com/techkylabs/getting-started-with-python-flask-framework-part-1-a4931ce0ea13).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE3NTAwMjUwM119
-->