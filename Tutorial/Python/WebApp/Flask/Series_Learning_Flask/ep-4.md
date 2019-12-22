# Serving static files | Learning Flask Ep. 4

Linking stylesheets, javascript files and serving images with Flask

In this episode of the Learning Flask series, we'll be making our HTML look prettier with some images, CSS and JavaScript, along with a few extra tips on working with static files.

Flask provides a few useful ways for working with static files so let's get started.

### Creating stylesheets

If you've worked with HTML and CSS before, you'll know that we have to import a stylesheet in the  `<head>`  tag of our HTML.

It's no dirrefent in Flask, however we need to cover a few bases before we try and import and stylesheets into our HTML files.

Flask requires a  `static`  directory. Just like the  `templates`  directory we created in the last episode.

Let's go ahead and create a  `static`  directory, a  `css`  directory and a stylesheet.

We'll create the  `static`  directory next to our  `templates`  directory. From the root  `app`  directory, enter the following:
```
cd app
mkdir static
cd static
mkdir css
cd css
touch style.css 
```
Your application filestructure should now look loike this:
```
app
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── static
│   │   └── css
│   │       └── style.css
│   ├── templates
│   │   ├── admin
│   │   │   └── dashboard.html
│   │   └── public
│   │       └── index.html
│   └── views.py
├── requirements.txt
└── run.py
```

Open up  `style.css`  in your editor and add the following:

**app/app/static/css/style.css**
```css
body {
  background-color: #f1f1f1;
}
```
Save and close the file for now.

Next up, we'll import our new stylesheet into our  `index.html`  file in the  `public`  directory.

Typically you would provide a relative path to your stylesheet in the  `<head>`, for example:
```html
<head>
  <link rel="stylesheet" href="path/to/your/stylesheet.css">
</head> 
```
You can use relative paths in Flask, but it'll get complicated real fast as we've split our HTML templates up into sub-directories.

Thankfully, there's a better way!

### Linking stylesheets

Flask has a function called  `url_for`  which can be used in our HTML to provide a path to any static files we want to fetch.

Go ahead and open up  `index.html`  in your editor and in the  `<head>`  tag, add the following:

**app/app/templates/public/index.html**
```html
<link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
```
> Notice the double curly braces  `{{ }}`

These double curly braces are part of the Jinja templating engine that Flask uses to render our HTML templates.

You'll learn all about Jinja in the next couple of episodes in this series! Just know for now, that before any of our HTML files are rendered in the browser, Flask will pass our HTML files through the Jinja templating engine and parse anything we provide in between the sets of curly braces.

In this case, Jinja will replace  `{{ url_for('static', filename='css/style.css') }}`  with the path to the CSS file.

The  `url_for`  function takes 2 arguments, and endpoint and some values. In this case, we've providing  `static`  as the endpoint and  `css/style.css`  as the filename value.

In this case, Flask will render the stylesheet we just created at  `static/css/style.css`.

Save the file and reload your browser to see the subtle changes to the background color.

Next up, you'll learn how to do something very similar with JavaScript files.

### Javascript files

We're going to create a Javascript directory and a JavaScript file and link them to our HTML templates in the exact same way as we did with the CSS.

We'll create a  `js`  directory inside our  `static`  directory, along with creating a new file called  `app.js`  in the  `js`  folder.

Our new app file structure will look like this:

`app
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── static
│   │   ├── css
│   │   │   └── style.css
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

From the  `app`  root directory, we'll run the following:

`cd app
cd static
mkdir js
cd js
touch app.js` 

Open up the  `app.js`  file and add the following:

`console.log("Hello from app.js!");` 

Let's link our  `js`  file to our HTML template.

Open up  `index.html`in your editor, and at the bottom of the page, just before the closing  `</body>`  tag, add the following:

`<script src="{{ url_for('static', filename='js/app.js') }}"></script>` 

Your  `index.html`  file should now look something like this:

**app/app/templates/public/index.html**

`<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
  <title>Index</title>
</head>

<body>
  <h1 style="color: blue">Index</h1>
  <p>This is an HTML file served up by Flask</p>
  <script src="{{ url_for('static', filename='js/app.js') }}"></script>
</body>

</html>` 

Just like we did with the stylesheet, we use  `url_for`  to provide a directory and a path to our filename.

Save the file, make sure your app is running with the  `flask run`  command and reload your browser.

> Tip - You must run the  `flask run`  command from the root directory of your application, in the same directory as  `run.py`

Open up the developer tools and click on the  `console`  tab to see the message from your JavaScript file.

`Hello from app.js!` 

Perfect! We've linked our stylesheet and our Javascript file. Let's talk about serving images in Flask.

### Serving images

Any guesses on how we're going to serve images?

We're going to do exactly what we did with our CSS and JavaScript files and create a new  `img`  directory in our  `static`  directory and place all of our pictures in there.

Our new app file structure will look like this:

`app
├── app
│   ├── __init__.py
│   ├── admin_views.py
│   ├── static
│   │   ├── css
│   │   │   └── style.css
│   │   ├── img
│   │   │   └── my-image.png
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

From the root  `app`  directory, we'll create our new directories with the following commands:

`cd app
cd static
mkdir img` 

Go ahead and drop any image into the  `img`  directory.

Next up, let's put an  `<img>`  tag in our  `index.html`  file and render an image to the browser.

open up  `index.html`  and add the following just under the  `<p>`  tag in the  `<body>`:

**app/app/templates/public/index.html**

`<img src="{{ url_for('static', filename='img/TEST-IMG.png') }}" alt="">` 

Your  `index.html`  should now look like this:

**app/app/templates/public/index.html**

`<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
  <title>Index</title>
</head>

<body>
  <h1 style="color: blue">Index</h1>
  <p>This is an HTML file served up by Flask</p>
  <img src="{{ url_for('static', filename='img/TEST-IMG.png') }}" alt="">
  <script src="{{ url_for('static', filename='js/app.js') }}"></script>
</body>

</html>` 

We're using the exact same  `url_for`  function to point to the path of our image.

Save the file, make sure your app is running and reload the browser windows to see your image rendered!

### Wrapping up

You've learned how to create the static directory, CSS, JavaScript and image directories and link static files to HTML templates, along with rendering images using the  `url_for`  function.

`url_for`  provides some other powerful uses that you'll learn about very soon.

At this point, your armed with the tools to be able to create a simple static website! If you're feeling confident, go ahead and create a few more pages, add some CSS and JavaScript and have some fun.

In the next part of this series, you'll be learning more about the Jinja templating engine, along with passing variables and objects into your HTML from Flask views.

Last modified  ·  28 Feb 2019




> Written with [StackEdit](https://pythonise.com/series/learning-flask/serving-static-files-with-flask).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkwNTMwNDIyNl19
-->