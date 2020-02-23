# Building a Simple Python Web APP using Flask framework and MongoDB

## Introduction

We are going to create a simple Python web application using Flask framework and MongoDB. It is very easy to work with Flask as well as MongoDB.

You can select the customized installation choice for adding Python environment variables. If you choose default installation, please set these variables manually.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image001.jpg)

Please click Add Python 3.7 to PATH option. It will add one entry in the environment variable.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image002.jpg)

If needed you can modify the installation path. Please check the Python environment variables.

After successful installation, if you check the system environment variable you can see the below two entries are added in the system.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image003.jpg)

We installed the Python 3.7 version, so it added as Python 37-32.

\Scripts folder is used for handling additional packages needed for Python.

Now you can check the Python and PIP version in the command prompt. PIP is the abbreviation for Python package index which is used for installing, upgrading or removing the additional Python libraries from our system.

> python --version and pip -- version

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image004.jpg)

By default, the pip version may not be 18. This is the latest version as of today. If your pip version is older than that, please upgrade it.

_>python -m pip install -__U pip_Now we are going to install Flask. Flask is a web framework for Python. Flask provides you with tools, libraries and technologies that allow you to build a web application in Python.

Its dependencies are,

-   Werkzeug a WSGI utility library
-   jinja2 which is its template engine

WSGI is basically a protocol defined so that the Python application can communicate with a web-server and thus be used as web-application outside of CGI.

Jinja2 is used for creating views in flask application. It holds all the static files like html, CSS and JavaScript files.

First install Flask using pip command in command prompt.

_>pip install Flask_It will install the latest version of flask library from its global repository and in Windows machines it saves the below file location

_C:\Program Files (x86)\Python\Python37-32\Lib\site-packages_

Our sample application uses MongoDB as database. So, we are going to install Mongo DB from below URL.

_[https://www.mongodb.com/download-center#community](https://www.mongodb.com/download-center#community)_

It is a free community version. After successful installation it is all set to run MongoDB instance.

Before running the MongoDB instance, we must create a data folder and run below command in command prompt.

_"C:\Program Files\MongoDB\Server\4.0\bin\mongod.exe" --dbpath="C:\mongo-data"_

Here C:\mongo-data folder is used for saving mongodb files.

While installing the MongoDB in windows system, you can choose the compass community edition also.

This is a free edition and will help to handle our MongoDB databases, collections (tables in MongoDB) and documents (records) graphically

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image005.jpg)

By default, MongoDB is running in localhost 27017 port.

We can see there are 3 databases, (admin, config and local) created automatically in the installation time.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image006.jpg)

Now we are going to install PyMongolibrary in python. PyMongo is a simple but powerful Python distribution containing tools for working with MongoDB and is the recommended way to work with MongoDB from Python. It's a kind of ODM (object document mapper). There is mongoengine and so many libraries also available as ODM for Python.

_>pip install pymongo_

We need to install another Python library, bson, too. It is used for getting objectId property of mongodb document.

_>pip install bson_

Now we are all set and ready to start our python program.Create a folder named FlaskwithMongo and add two sub folders, static and templates, inside it. There is a convention to name static and templates used in jinja2 framework. Please open the folder in any of the code editors. I am using Visual Studio code as an IDE. Create a new file named  [app.py](http://app.py/). This is the only Python file we are using in this application. First, we are going to import the required libraries into our application.

1.  from flask import Flask, render_template,request,redirect,url_for
2.  from bson import ObjectId
3.  from pymongo import MongoClient
4.  import os

Now we are going to declare the app variable in our program.

_app = Flask(**name**)_

This app variable is used in the entire application.

Now we are going to declare twovariable titles and headings which are later used in jinja2 template.

```
title = "TODO sample application with Flask and MongoDB"  
heading = "TODO Reminder with Flask and MongoDB" 

```

We must declare the connection string for MongoDB and select a database. Also, we are going to select our collection name to a variable.

```
client = MongoClient("mongodb://127.0.0.1:27017") #host uri  
db = client.mymongodb #Select the database  
todos = db.todo #Select the collection name 

```

As I mentioned earlier mongodb is running in the port 27017 by default. Please note that we have selected mymongodb as database and todo as collection name. When we create our first transaction, pymongo will generate the database and collection automatically. Unlike SQL server or any other RDBMS mongodb doesn’t require predefined schemas.

In flask, it is easy to implement routing unlike any other programming language.

For that, we are using  _render_template_, request, redirect and url_for. All these methods help us to establish redirection and show html templates in the browser

```
def redirect_url():    
return request.args.get('next') or \    
request.referrer or \    
url_for('index')  

```

In the above code we defined a method named _redirect_url _and it is used to redirect page to index page.

```
@app.route("/")    
@app.route("/uncompleted")    
def tasks ():    
#Display the Uncompleted Tasks    
todos_l = todos.find({"done":"no"})    
a2="active"    
return render_template('index.html',a2=a2,todos=todos_l,t=title,h=heading) 

```

In the above code, we defined a method named  _tasks_  and it is used for two routes. One for default “/” route and another for “/uncompleted” route. In this code we defined a variable todos_l and it gets the documents from mongodb filter by condition done equal to no. We defined one more variable named a2 and it is used for controlling active records. Both todos_land a2 variables passed with the other two variables, title, and heading, and passed to the jinja2 template index.html which we must create in the template folder.

Now we are going to finish all the remaining route definitions for adding and deleting the documents to mongodb

**[app.py](http://app.py/) **

```
from flask import Flask, render_template,request,redirect,url_for # For flask implementation    
from bson import ObjectId # For ObjectId to work    
from pymongo import MongoClient    
import os    
    
app = Flask(__name__)    
title = "TODO sample application with Flask and MongoDB"    
heading = "TODO Reminder with Flask and MongoDB"    
    
client = MongoClient("mongodb://127.0.0.1:27017") #host uri    
db = client.mymongodb    #Select the database    
todos = db.todo #Select the collection name    
    
def redirect_url():    
    return request.args.get('next') or \    
           request.referrer or \    
           url_for('index')    
  
@app.route("/list")    
def lists ():    
    #Display the all Tasks    
    todos_l = todos.find()    
    a1="active"    
    return render_template('index.html',a1=a1,todos=todos_l,t=title,h=heading)    
  
@app.route("/")    
@app.route("/uncompleted")    
def tasks ():    
    #Display the Uncompleted Tasks    
    todos_l = todos.find({"done":"no"})    
    a2="active"    
    return render_template('index.html',a2=a2,todos=todos_l,t=title,h=heading)    
  
  
@app.route("/completed")    
def completed ():    
    #Display the Completed Tasks    
    todos_l = todos.find({"done":"yes"})    
    a3="active"    
    return render_template('index.html',a3=a3,todos=todos_l,t=title,h=heading)    
  
@app.route("/done")    
def done ():    
    #Done-or-not ICON    
    id=request.values.get("_id")    
    task=todos.find({"_id":ObjectId(id)})    
    if(task[0]["done"]=="yes"):    
        todos.update({"_id":ObjectId(id)}, {"$set": {"done":"no"}})    
    else:    
        todos.update({"_id":ObjectId(id)}, {"$set": {"done":"yes"}})    
    redir=redirect_url()        
    
    return redirect(redir)    
  
@app.route("/action", methods=['POST'])    
def action ():    
    #Adding a Task    
    name=request.values.get("name")    
    desc=request.values.get("desc")    
    date=request.values.get("date")    
    pr=request.values.get("pr")    
    todos.insert({ "name":name, "desc":desc, "date":date, "pr":pr, "done":"no"})    
    return redirect("/list")    
  
@app.route("/remove")    
def remove ():    
    #Deleting a Task with various references    
    key=request.values.get("_id")    
    todos.remove({"_id":ObjectId(key)})    
    return redirect("/")    
  
@app.route("/update")    
def update ():    
    id=request.values.get("_id")    
    task=todos.find({"_id":ObjectId(id)})    
    return render_template('update.html',tasks=task,h=heading,t=title)    
  
@app.route("/action3", methods=['POST'])    
def action3 ():    
    #Updating a Task with various references    
    name=request.values.get("name")    
    desc=request.values.get("desc")    
    date=request.values.get("date")    
    pr=request.values.get("pr")    
    id=request.values.get("_id")    
    todos.update({"_id":ObjectId(id)}, {'$set':{ "name":name, "desc":desc, "date":date, "pr":pr }})    
    return redirect("/")    
  
@app.route("/search", methods=['GET'])    
def search():    
    #Searching a Task with various references    
    
    key=request.values.get("key")    
    refer=request.values.get("refer")    
    if(key=="_id"):    
        todos_l = todos.find({refer:ObjectId(key)})    
    else:    
        todos_l = todos.find({refer:key})    
    return render_template('searchlist.html',todos=todos_l,t=title,h=heading)    
    
if __name__ == "__main__":    
    
    app.run()   

```

We must add the below three HTML files in the templates folder. (index.html, searchlist.html and update.html)

**index.html**

```
<html>    
    <head>    
        <title>{{t}}</title>    
        <!-- href="/static/assets/style.css"-->    
        <link rel="stylesheet" type="text/css"  href="{{ url_for('static',filename='assets/style.css')}}" >    
        <link rel="stylesheet" type="text/css"  href="{{ url_for('static',filename='assets/emoji.css')}}" >    
        <script src="{{ url_for('static',filename='assets/twemoji.min.js')}}"></script>      
        <script src="{{ url_for('static',filename='assets/emoji.js')}}"></script>    
    </head>    
<body>    
    <h1>{{ h }}</h1>    
    <ul>    
        <li><a href="/list" class="{{ a1 }}">ALL</a></li>    
        <li><a href="/" class="{{ a2 }}">Uncompleted</a></li>    
        <li><a href="/completed" class="{{ a3 }}">Completed</a></li>    
    </ul>    
    <hr>    
    {% if todos[0] %}    
    <div span="right">    
    <form action="/search"   method="GET" >    
        <table class="none" id="close">    
        <tr>    
        <td></td><td></td>    
        <td><big><b>Search Reference:</b></big></td>    
        <td><select name="refer" required>    
            <option value="name">Task Name</option>    
            <option value="desc">Description</option>    
            <option value="date">Date</option>    
            <option value="pr">Priority</option>    
        </select></td>    
        <td><input type="text" name="key" placeholder="Search Task" size="15" /></td>    
        <td><button type="submit">Search</button></td>    
        </tr>    
        </table>    
    </form>    
    </div>    
    <b><big>To-Do LIST :</big></b>    
    <table>    
        <tr id="row">    
            <th class="status">Status</th>    
            <th class="name">Task Name</th>    
            <th class="desc">Description Name</th>    
            <th class="date">Date</th>    
            <th class="pr">Priority</th>    
        <th class="func1">Remove</th>    
        <th class="func2">Modify</th>    
        </tr>    
    {% for todo in todos %}    
        <tr class="datas">    
            <td><a href="./done?_id={{ todo['_id'] }}"><input type="image" src="static/images/{{todo['done']}}.png" alt="Submit ME"></a></td>    
            <td class="name">{{ todo["name"] }}</td>    
            <td class="desc">{{ todo["desc"] }}</td>    
            <td class="date">{{ todo["date"] }}</td>    
            <td class="pr">{{ todo["pr"] }}</td>    
            <td class="func1"><a href="./remove?_id={{ todo['_id'] }}"><button type="submit">DELETE</button></a></td>    
            <td class="func1"><a href="./update?_id={{ todo['_id'] }}"><button type="submit">EDIT</button></a></td>    
        </tr>    
    {% endfor %}    
    </table>    
    {% else %}    
    <h4>No Tasks in the List !!</h4>    
    {% endif %}    
    <hr/>    
    <form action="/action" method="POST">    
    <table class="none">    
        <tr>    
            <td><b><big><label>Add a Task : </label></big></b></td>    
        </tr>    
        <tr>    
        <td><input type="text" name="name" placeholder="Taskname" ></td>    
        <td><textarea name="desc" rows="1" cols="30" placeholder="Enter Description here..." required></textarea></td>    
        <td><input type="text" name="date" placeholder="Date" /></td>    
        <td><input type="text" name="pr" placeholder="Priority" /></td>    
        <td><button type="submit"> Create </button></td>    
        </tr>    
    </form>    
    </table>    
    <script>    
        
    </script>    
</body>    
</html>   

```

**searchlist.html**

```
<html>    
    <head>    
        <title>{{t}}</title>    
        <link rel="stylesheet" type="text/css"  href="{{ url_for('static',filename='assets/style.css')}}" >    
    </head>    
<body>    
    <h1>{{h}}</h1>    
    <hr>    
        {% if todos[0] %}    
    <h3>Result of the Search : ToDO List</h3>    
    <table>    
        <tr id="row">    
           <td class="status">Status</td>    
            <td class="name">Task Name</td>    
            <td class="desc">Task Description</td>    
            <td class="date">Date</td>    
            <td class="pr">Project</td>    
        <td class="func">Delete</td>    
        <td class="func">Modify</td>    
        </tr>    
        {% for todo in todos %}    
        <tr class="datas">    
            <td><a href="./done?_id={{ todo['_id'] }}"><input type="image" src="static/images/{{todo['done']}}.png" alt="Submit ME"></a></td>    
            <td class="name">{{ todo["name"] }}</td>    
            <td class="desc">{{ todo["desc"] }}</td>    
            <td class="date">{{ todo["date"] }}</td>    
            <td class="pr">{{ todo["pr"] }}</td>    
            <td class="func1"><a href="./remove?_id={{ todo['_id'] }}"><button type="submit">DELETE</button></a></td>    
            <td class="func1"><a href="./update?_id={{ todo['_id'] }}"><button type="submit">EDIT</button></a></td>    
        </tr>    
        {% endfor %}    
    {% else %}    
        <h4>No Result Found !!</h4>    
    {% endif %}    
    </table>    
   <a href="/">Return to TaskList</a>    
</body>    
</html>  

```

**update.html**

```
<html>    
   <head>    
            <title>{{t}}</title>    
        </head>    
        <style>       
            h1{    
                font-family:"Arial Black", Gadget, sans-serif;    
            }    
            body{    
                background-color:white;    
            }    
        </style>    
    <body>    
        <h1>{{h}}</h1>    
        <hr>    
        <h3>Update tasks with a reference</h3>    
        <form action="/action3" method="POST">    
        {% for task in tasks %}    
            Unique Object ID : {{ task['_id'] }}<br/>    
        <input type="text" name="_id" value="{{ task['_id'] }}" hidden>    
        
        <table>    
        <tr>    
        <td>Task Name</td><td> : </td><td><input type="text" name="name" value="{{ task['name'] }}" placeholder="{{ task['name'] }}"></td>    
        </tr>    
        <tr>    
        <td>Description</td><td> : </td><td><textarea type="text" name="desc" rows=3 cols=30 placeholder="{{ task['desc'] }}"> {{ task['desc'] }} </textarea></td>    
        </tr>    
        <tr>    
        <td>Date</td><td> : </td><td><input type="text" name="date" value="{{ task['date'] }}" placeholder="{{ task['date'] }}"></td>    
        </tr>    
        <tr>    
        <td>Priority</td><td> : </td><td><input type="text" name="pr" value="{{ task['pr'] }}" placeholder="{{ task['pr'] }}"></td>    
        </tr>    
        </table>    
        {% endfor %}    
            <button type="submit"> Update Task </button>    
            <br/>    
        </form>    
        <a href="/">Return to TaskList</a>    
</body>    
</html>   

```

All three of these files used the features of jinja2 framework to render the model values from  [app.py](http://app.py/).

In addition, we must add emoji.css, emoji.js, style.css and twemoji.min.js files in the static\assets folder

**emoji.css**

```
img.emoji {      
// Override any img styles to ensure Emojis are displayed inline      
margin: 0px !important;      
display: inline !important;      
}    

```

**emoji.js**

```
window.onload = function() {    
      // Set the size of the rendered Emojis    
      // This can be set to 16x16, 36x36, or 72x72    
     twemoji.size = '16x16';    
      // Parse the document body and    
      // insert <img> tags in place of Unicode Emojis    
      twemoji.parse(document.body);    
}   

```

**style.css**

```
h1{    
/*  font-family:"Arial Black", Gadget, sans-serif;*/    
    font-family:"Times New Romans", Gadget, sans-serif;    
}    
body{    
   color:black;    
    background-color:white;    
    left-margin:10px;    
    right-margin:10px;    
}    
table{    
    width:95%;    
    border-collapse:collapse;    
    table-layout:fixed;    
}    
td    
{    
    border: rgba(224, 119, 70, 1) 2px solid;    
    word-wrap:break-word;    
}    
table#close{    
       
    table-layout:default;    
    border-collapse:seperate;    
    border-spacing: 5px 5px;    
    border:none;    
    vertical-align:top;    
}    
table.none    
{    
    border:none;    
    vertical-align:top;    
}    
table.none td    
{    
    border: none;    
}    
tr.row td{    
    text-decoration:italic;    
}    
th.status{    
    width:5%;    
}    
th.name{    
    width:20%;    
}    
th.des{    
    width:40%;    
    padding:5px 5px 5px 5px;    
}    
th.date{    
    width:8%;    
}    
th.pr{    
    width:7%;    
}    
th.func1{    
   width:6%;    
}    
th.func2{    
   width:5%;    
}    
input[type=submit] {    
    width: 20em;  height: 2em;    
}    
ul {    
    list-style-type: none;    
   margin: 0;    
   padding: 0;    
   overflow: hidden;    
   background-color: #333;    
}    
li {    
    float: left;    
}    
li a {    
    display: block;    
    color: white;    
   text-align: center;    
   padding: 14px 16px;    
   text-decoration: none;    
}    
a.active {    
   background-color: #4CAF50;    
}    
/* Change the link color to #111 (black) on hover */    
li a:hover {    
    background-color: #111;    
}   

```

There are two images, _no.__png_, and _yes.__png,_  in static\images folder.

We are ready to run our sample application.

Please start our mongodb instance with the below command

_"C:\Program Files\MongoDB\Server\4.0\bin\mongod.exe" --dbpath="C:\mongo-data"_

Please note that mongodb now runs with data folder C:\mongo-data

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image007.jpg)

By default, it is listening the port 27017.

Please open another command prompt window in the same Python application folder and run Python with the below command.

For example:

_D:\Python\FlaskWithMongo>python  [app.py](http://app.py/)_

Our local server is running in the port 5000 by default.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image008.jpg)

The application is now running successfully.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image009.jpg)

You can now add a sample task as task name “Test task for mongo with flask application”, description “Sample description”, date “05-08-2018" and priority “High”

After clicking the Create button we can immediately view the task details in the grid.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image010.jpg)

Please note that there is a new database named mymongodb and collection todo is created now. Using this application, you can edit and remove the existing documents easily.

You can check the document details in the mongodb compass community too.

![This is image title](https://www.c-sharpcorner.com/article/a-sample-python-flask-application-with-mongodb/Images/image011.jpg)

Happy coding with Flask and MongoDB!!!

You can download the source code from  [Github](https://on.morioh.net/b0a3f595aa?r=https://github.com/sarathlalsaseendran/FlaskWithMongoDB "Github Source code for Sample TODO application with python flask and mongo db").

Thank you!


> [Source : ](https://).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyNDI2NzE2OV19
-->