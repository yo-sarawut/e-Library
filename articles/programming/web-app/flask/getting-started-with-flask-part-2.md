# Getting started with Python Flask framework \(Part 2\)

![enter image description here](https://miro.medium.com/max/1920/1*kvx5ly0fyVyhCYPYpKoOoQ.png)

Hello Devs, Welcome to our flask framework series part 2, in this blog post we will get to know some more interesting stuffs in python flask framework. But in case if you didn’t know any about python flask framework and want to just get start with it, then i would first suggest you to read my previous blog post on python flask framework. Below is link to my previous blog post.

So Basically In this post, I will be covering the following parts :-

1. **Render Static Files \(i.e Images, JS & CSS Files\) in HTML templates.**
2. **Introduction to HTTP Methods in Routes.**
3. **Template Inheritance & Display Messages in templates.**

**How Render Static Files In HTML Templates**

As, We all know that CSS files, JS files and images all of them are an integral part of any website. Attaching an CSS or JS file is very each to do in html and so as display an image as well, however it is not that easy to render these things when working with python, as the syntax for rendering these things are different from the one that you are currently aware of. But Luckily Python’s Flask Framework provide us an special method i.e “**url\_for\(\)**” for rendering all of these things in our HTML Templates.

**Note :** First of all you have to create a folder called `static` in project directory after that it will be now available at `/static` on your application.

So let’s get started.

**Example 1 -**

This example will show you how you can attach an CSS file to an template.

```markup
<!DOCTYPE html>  
<html>  
<head>  
 <title>Techylabs</title>  
 <link rel="stylesheet" href="{{ url_for('static', filename= style.css') }}">  
</head>  
<body>
```

**Explanation**

1. First we open up the link tag to attach the CSS file.
2. Then in  **href**  attribute we use  **url\_for\(\)**  provided by flask framework, in this function we passed ‘**static**’ as first argument which tells the flask that this would be an static file and then passed ‘**filename**’ as second argument and assigns the  **filename.extension\_of\_file** to it.
3. Lastly we put all this stuff in this special curly braces “” & what it does, it will just print the full path to file as show in picture below.

![](https://miro.medium.com/max/388/1*y8lZ852VujypFQq6E37YoQ.png)

**Note :** In above example, I am assuming that your CSS file is being stored directly in the static folder like this : “**static/style.css**”

Also your file name could be anything you want. In my case it was “**style**”.css

**Example 2 -**

This example will show you how you can attach an JS file to an template.

```markup
<!DOCTYPE html>  
<html>  
<head>  
 <title>Techylabs</title>  
</head>  
<body><!-- Attaching a JS file -->  
 <script src="{{ url_for('static', filename='app.js') }}"></script></body>  
</html>
```

**Explanation**

1. First we open up the script tag to attach the JS file.
2. Then in  **src**  attribute we use  **url\_for\(\)**  provided by flask framework, in this function we passed ‘**static**’ as first argument which tells the flask that this would be an static file and then passed ‘**filename**’ as second argument and assigns the  **filename.extension\_of\_file** to it.
3. Lastly we put all this stuff in this special curly braces “” & what it does, it will just print the full path to file as show in picture below.

![](https://miro.medium.com/max/407/1*-CN9hJ6uSaKLCN7tcfLq-w.png)

**Note :** In above example, I am assuming that your JS file is being stored directly in the static folder like this : “**static/app.js**”

Also your file name could be anything you want. In my case it was “**app**”.js

**Example 3-**

This example will show you how you can serve an Image file in templates.

```markup
<!DOCTYPE html>  
<html>  
<head>  
 <title>Techylabs</title>  
</head>  
<body><!-- Serving an Image -->  
 <img src="{{ url_for('static', filename='techkylabs.png' ) }}" alt="Techylabs"></body>  
</html>
```

**Explanation**

1. First we open up the img tag to serve an image.
2. Then in  **src**  attribute we use  **url\_for\(\)**  provided by flask framework, in this function we passed ‘**static**’ as first argument which tells the flask that this would be an static file and then passed ‘**filename**’ as second argument and assigns the  **filename.extension\_of\_file** to it.
3. Lastly we put all this stuff in this special curly braces “” & what it does, it will just print the full path to file & ultimately the image will be shown up in the browser.

![](https://miro.medium.com/max/155/1*XDk4SWsApr81rFS21tcpiw.png)

**Note :** In above example, I am assuming that your image file is being stored directly in the static folder like this : “**static/techkylabs.png**”

Also your file name could be anything you want. In my case it was “**techkylabs**”.png

**Special Note :** In Above examples, I assume that all of your static files are stored directly in your static folder but in case when you have all of CSS files in a sub directory called ‘**css**’ under the static folder, similarly Your JS files in ‘**js**’ and image files in ‘**images**’. Then you have to give relative path to your respective files in **filename** argument of **url\_for\(\)**

**Example For CSS File**

```markup
<!doctype html>  
<html>  
  <head>  
    <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">  
  </head>  
  <body>     
  </body>  
</html>
```

Similarly now you can assign relative path to your JS and image files.

**Introduction to HTTP Methods in Routes**

HTTP \(Hyper Text Transfer Protocol\) methods just tells the server what the client wants to do with the requested page.

There are lots of HTTP Methods available but generally only 4 of them are most commonly used methods, these are below :-

1. **GET** : This browser tells the server to just  _get_  the information stored on that page and send it.
2. **POST** : The browser tells the server that client wants to  _post_  some new information to that URL.
3. **PUT** : The browser tells the server that it wants to  _edit_  some information on that URL.
4. **Delete** : The browser tells the server that it wants to  _delete_  some information on that URL.

Now Let me show you, how we can use some of the above methods in python flask framework.

**Note :-** By default, a route only answers to `GET` requests, but that can be changed by providing the `methods` argument to the `[**r**](http://flask.pocoo.org/docs/0.12/api/#flask.Flask.route)**oute()**` decorator attached to the functions.

**Example :**

```python
from flask import Flask, request, render_templateapp = Flask(__name__)@app.route('/', methods=['GET', 'POST'])  
def home():  
 if request.method == 'POST':  
  return render_template('home.html')  
 else:  
  return render_template('index.html')if __name__ == '__main__':  
 app.run(host='0.0.0.0', port=8080, debug=True)
```

**Explanation**

1. First I just import Flask, request, render\_template from flask.
2. Create Instance of Flask.
3. Define a function and attached a route for it and in route, i used methods as second argument which is list in which i assigns two HTTP methods ‘**GET**’ & ‘**POST**’. This will make sure that this function will accepts only two types of request \(i.e get or post\).
4. In  **home\(\)**  Function, I check if request method is ‘**POST**’ then render the home.html template otherwise it will be get request and if it is so then render the index.html template.
5. Finally, I just call the  **run\(\)** function of Flask to run the server on global IP with a port no 8080.

**Template Inheritance & Display Messages in templates**

Many times we want certain things in our web pages \(i.e templates\) to be the same such as header, footer & navbar. So far what we have been doing was just copy and paste the same code over and over, again and again…

But Python’s Jinja Syntax makes it very easy to do and also time saving.

The most powerful part of Jinja is template inheritance. Template inheritance allows you to build a base “skeleton” template that contains all the common elements of your site and defines **blocks** that child templates can override.

Sounds complicated but don’t worry it is actually very simple.

**Example**

Suppose we make an template and named it **main\_layout.html,** this template defines a simple HTML skeleton document that you might in your other templates as well. So now, It’s the job of your all “child” templates \(i.e your other templates\) to fill the empty blocks with content.

**main\_layout.html**

```markup
<!doctype html>  
<html>  
  <head>  
    <title>{% block title %} {% endblock %}</title>  
  </head>  
  <body>  

    <main>  
      {% block content %}{% endblock %}  
    </main><footer>  
      {% block footer %}  
        &copy; Copyright 2017 by Techkylabs.  
      {% endblock %}        
    </footer></body>  
</html>
```

**Note :-** In above template I have taken 3 blocks named as \(title, content & footer\) But you can name it whatever you like. But then you will need to make sure that you call these blocks name correctly when you extends this template in other template.

**home.html**

```markup
{% extends 'main_layout.html' %}{% block title %}  
  Techkylabs  
{% endblock %}{% block content %}  
  <h1>Hello Devs</h1>  
{% endblock %}{% block footer %}  
  {{ super() }}  
{% endblock %}
```

**Explanation**

In **home.html** we use\`

\` tag which is the key here. It tells the template engine that this template “extends” another template which in our case is ‘**main\_layout.html**’. When the template system evaluates this template, first it locates the parent.

**Note 1 :** The extends tag must be the first tag in the template.

**Note 2 :** To render the contents of a block defined in the parent template, you can just use `{{ super() }}`. It will just print out all of the content defined in the parent template as it is in the child template.

Also note that in above example i assume that your both templates are in the same directory i.e **templates/main\_layout.html** & **templates/home.html**

If in case your templates are in sub directory of templates folder \(i.e **template/app/main\_layout.html**\) then your \`

`tag must have relative path to the parent template Such as`

\`

**Thanks for reading this article. If you found this article useful be sure to clap to recommend this article.**

For such related articles follow [**me**](https://medium.com/@rishu98) and [**TechkyLabs**](https://medium.com/techkylabs)**.**

Follow us on other social accounts: [Facebook](https://www.facebook.com/techkylabs), [Twitter](https://twitter.com/techkylabs), [Github](https://github.com/techkylabs)

**PS: Don’t forgot to give a clap :\)**

> Source : [medium.com](https://medium.com/techkylabs/getting-started-with-python-flask-framework-part-2-5838ddc5d9a7).

