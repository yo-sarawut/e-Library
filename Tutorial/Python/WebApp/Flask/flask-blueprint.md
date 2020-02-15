
---
bookFlatSection: true
title: Read and Write Files
bookToc: true

---
Use a Flask Blueprint to Architect Your Applications
===
![enter image description here](https://files.realpython.com/media/What-Can-You-Do-With-Flask-Blueprints_Watermarked.faba402ad037.jpg)

[Flask](https://palletsprojects.com/p/flask/)  is a very popular web application framework that leaves almost all design and architecture decisions up to the developer. In this tutorial, you’ll learn how a  **Flask Blueprint**, or  **Blueprint**  for short, can help you structure your Flask application by grouping its functionality into reusable components.

**In this tutorial, you’ll learn:**

-   What Flask Blueprints are and how they work
-   How to create and use a Flask Blueprint to organize your code
-   How to improve code reusability using your own or a third-party Flask Blueprint

This tutorial assumes that you have some experience using Flask and that you’ve built some applications before. If you haven’t used Flask before, then check out  [Python Web Applications with Flask (Tutorial Series)](https://realpython.com/python-web-applications-with-flask-part-i/).

**Free Bonus:**  [Click here to get access to a free Flask + Python video tutorial](https://realpython.com/bonus/discover-flask-video-tutorial/)  that shows you how to build Flask web app, step-by-step.

## What a Flask Application Looks Like

Let’s start by reviewing the structure of a small Flask application. You can create a small web application by following the steps in this section. To get started, you need to install the  `Flask`  Python package. You can run the following command to install Flask using  [`pip`](https://realpython.com/what-is-pip/):
```py
$ pip install Flask==1.1.1
```

The above command installs Flask version  `1.1.1`. This is the version you’ll use throughout this tutorial, though you can apply what you’ll learn here to other versions, as well.

**Note:**  For more information on how to install Flask in a virtual environment and other  `pip`  options, check out  [Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/)  and  [What Is Pip? A Guide for New Pythonistas](https://realpython.com/what-is-pip/).

After you install Flask, you’re ready to start implementing its functionality. Since Flask doesn’t impose any restrictions on project structure, you can organize your project’s code as you want. For your first application, you can use a very straightforward layout, as shown below. A single file will contain all the application logic:
```
`app/
|
└── app.py` 

The file  `app.py`  will contain the definition of the application and its views.

When you create a Flask application, you start by creating a  `Flask`  object that represents your application, and then you associate  **views**  to  **routes**. Flask takes care of dispatching incoming requests to the correct view based on the request URL and the routes you’ve defined.

In Flask, views can be any callable (like a function) that receives  **requests**  and returns the  **response**  for that request. Flask is responsible for sending the response back to the user.

The following code block is your application’s full source code:

`from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return "This is an example app"` 

This code creates the object  `app`, which belongs to the  `Flask`  class. The view function  `index()`  is linked to the route  `/`  using the  `app.route`  decorator. To learn more about decorators, check out  [Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/)  and  [Python Decorators 101](https://realpython.com/courses/python-decorators-101/).

You can run the application with the following command:

`$ flask run` 

By default, Flask will run the application you defined in  `app.py`  on port 5000. While the application is running, go to  `http://localhost:5000`  using your web browser. You’ll see a page showing the message,  `This is an example app`.

The chosen project layout is great for very small applications, but it doesn’t scale well. As your code grows, it can become harder for you to maintain everything in a single file. So, when your application grows in size or complexity, you may want to  **structure**  your code in a different way to keep it maintainable and clear to understand. Throughout this tutorial, you’ll learn how to use a Flask Blueprint to achieve this.

## What a Flask Blueprint Looks Like

Flask Blueprints encapsulate  **functionality**, such as views, templates, and other resources. To get a taste for how a Flask Blueprint would work, you can refactor the previous application by moving the  `index`  view into a Flask Blueprint. To do so, you have to create a Flask Blueprint that contains the  `index`  view and then use it in the application.

This is what the file structure looks like for this new application:

`app/
|
├── app.py
└── example_blueprint.py` 

`example_blueprint.py`  will contain the Flask Blueprint implementation. You’ll then modify  `app.py`  to use it.

The following code block shows how you can implement this Flask Blueprint in  `example_blueprint.py`. It contains a view at the route  `/`  that returns the text  `This is an example app`:

`from flask import Blueprint

example_blueprint = Blueprint('example_blueprint', __name__)

@example_blueprint.route('/')
def index():
    return "This is an example app"` 

In the above code, you can see the steps common to most Flask Blueprint definitions:

1.  **Create**  a  `Blueprint`  object called  `example_blueprint`.
2.  **Add**  views to  `example_blueprint`  using the  `route`  decorator.

The following code block shows how your application imports and uses the Flask Blueprint:

`from flask import Flask
from example_blueprint import example_blueprint

app = Flask(__name__)
app.register_blueprint(example_blueprint)` 

To use any Flask Blueprint, you have to import it and then  **register**  it in the application using  `register_blueprint()`. When a Flask Blueprint is registered, the application is extended with its contents.

You can run the application with the following command:

`$ flask run` 

While the application is running, go to  `http://localhost:5000`  using your web browser. You’ll see a page showing the message,  `This is an example app`.

## How Flask Blueprints Work

In this section, you’ll learn in detail how a Flask Blueprint is implemented and used. Each Flask Blueprint is an  **object**  that works very similarly to a Flask application. They both can have resources, such as static files, templates, and views that are associated with routes.

However, a Flask Blueprint is not actually an application. It needs to be registered in an application before you can run it. When you register a Flask Blueprint in an application, you’re actually  **extending**  the application with the contents of the Blueprint.

This is the key concept behind any Flask Blueprint.  **They record operations to be executed later when you register them on an application.**  For example, when you associate a view to a route in a Flask Blueprint, it records this association to be made later in the application when the Blueprint is registered.

### Making a Flask Blueprint

Let’s revisit the Flask Blueprint definition that you’ve seen previously and review it in detail. The following code shows the  `Blueprint`  object creation:

`from flask import Blueprint

example_blueprint = Blueprint('example_blueprint', __name__)` 

Note that in the above code, some arguments are specified when creating the  `Blueprint`  object. The first argument,  `"example_blueprint"`, is the Blueprint’s  **name**, which is used by Flask’s routing mechanism. The second argument,  `__name__`, is the Blueprint’s  **import name**, which Flask uses to locate the Blueprint’s resources.

There are other optional arguments that you can provide to alter the Blueprint’s behavior:

-   **static_folder:**  the folder where the Blueprint’s static files can be found
    
-   **static_url_path:**  the URL to serve static files from
    
-   **template_folder:**  the folder containing the Blueprint’s templates
    
-   **url_prefix:**  the path to prepend to all of the Blueprint’s URLs
    
-   **subdomain:**  the subdomain that this Blueprint’s routes will match on by default
    
-   **url_defaults:**  a  [dictionary](https://realpython.com/courses/dictionaries-python/)  of default values that this Blueprint’s views will receive
    
-   **root_path:**  the Blueprint’s root directory path, whose default value is obtained from the Blueprint’s import name
    

Note that all paths, except  `root_path`, are relative to the Blueprint’s directory.

The  `Blueprint`  object  `example_blueprint`  has methods and decorators that allow you to record operations to be executed when registering the Flask Blueprint in an application to extend it. One of the most used decorators is  `route`. It allows you to associate a view function to a URL route. The following code block shows how this decorator is used:

`@example_blueprint.route('/')
def index():
    return "This is an example app"` 

You decorate  `index()`  using  `example_blueprint.route`  and associate the function to the URL  `/`.

`Blueprint`  objects also provide other methods that you may find useful:

-   **.errorhandler()**  to register an error handler function
-   **.before_request()**  to execute an action before every request
-   **.after_request()**  to execute an action after every request
-   **.app_template_filter()**  to register a template filter at the application level

You can learn more about using Blueprints and the  `Blueprint`  class in the  [Flask Blueprints Documentation](https://flask.palletsprojects.com/en/1.1.x/blueprints/).

### Registering the Blueprint in Your Application

Recall that a Flask Blueprint is not actually an application. When you register the Flask Blueprint in an application, you  **extend**  the application with its contents. The following code shows how you can register the previously-created Flask Blueprint in an application:

`from flask import Flask
from example_blueprint import example_blueprint

app = Flask(__name__)
app.register_blueprint(example_blueprint)` 

When you call  `.register_blueprint()`, you apply all operations recorded in the Flask Blueprint  `example_blueprint`  to  `app`. Now, requests to the app for the URL  `/`  will be served using  `.index()`  from the Flask Blueprint.

You can customize how the Flask Blueprint extends the application by providing some parameters to  `register_blueprint`:

-   **url_prefix**  is an optional prefix for all the Blueprint’s routes.
-   **subdomain**  is a subdomain that Blueprint routes will match.
-   **url_defaults**  is a  [dictionary](https://realpython.com/courses/python-dictionary-iteration/)  with default values for view arguments.

Being able to do some customization at registration time, instead of at creation time, is particularly useful when you’re sharing the same Flask Blueprint in different projects.

In this section, you’ve seen how Flask Blueprints work and how you can create them and use them. In the following sections, you’ll learn how you can leverage a Flask Blueprint to  **architect**  your applications, structuring them into independent components. In some cases, it’s also possible for you to reuse these components in different applications to reduce development time!

## How to Use Flask Blueprints to Architect Your Application’s Code

In this section, you’re going to see how you can  **refactor**  an example application using a Flask Blueprint. The example application is an  **e-commerce**  site with the following features:

-   Visitors can sign up, log in, and recover  **passwords**.
-   Visitors can search for  **products**  and view their details.
-   Users can add products to their  **cart**  and checkout.
-   An API enables external systems to search and retrieve  **product information**.

You don’t need to care much about the details of the implementation. Instead, you’ll focus mainly on how a Flask Blueprint can be used to improve the application’s architecture.

### Understanding Why Project Layout Matters

Remember, Flask does not enforce any particular project layout. It’s completely feasible to organize this application’s code as follows:

`ecommerce/
|
├── static/
|   ├── logo.png
|   ├── main.css
|   ├── generic.js
|   └── product_view.js
|
├── templates/
|   ├── login.html
|   ├── forgot_password.html
|   ├── signup.html
|   ├── checkout.html
|   ├── cart_view.html
|   ├── index.html
|   ├── products_list.html
|   └── product_view.html
|
├── app.py
├── config.py
└── models.py` 

This application’s code is organized using these directories and files:

-   **static/**  contains the application’s static files.
-   **templates/**  contains the application’s templates.
-   **models.py**  contains the definition of the application’s models.
-   **app.py**  contains the application logic.
-   **config.py**  contains the application configuration parameters.

This is an example of how many applications begin. Although this layout is pretty straightforward, it has several drawbacks that arise as the app complexity increases. For example, it will be hard for you to reuse the application logic in other projects because all the functionality is bundled in  `app.py`. If you split this functionality into modules instead, then you could  **reuse complete modules across different projects**.

Also, if you have just one file for the application logic, then you would end up with a very large  `app.py`  that mixes code that’s nearly unrelated. This can make it hard for you to navigate and maintain the script.

What’s more, large code files are a source of  **conflicts**  when you’re working in a team, since everybody will be making changes to the same file. These are just a few reasons why the previous layout is only good for very small applications.

### Organizing Your Projects

Instead of structuring the application using the previous layout, you can leverage a Flask Blueprint to  **split the code into different modules**. In this section, you’ll see how to architect the previous application to make Blueprints that encapsulate related functionality. In this layout, there are five Flask Blueprints:

1.  **API Blueprint**  to enable external systems to search and retrieve product information
2.  **Authentication Blueprint**  to enable users to log in and recover their password
3.  **Cart Blueprint**  for cart and checkout functionality
4.  **General Blueprint**  for the homepage
5.  **Products Blueprint**  for searching and viewing products

If you use a separate directory for each Flask Blueprint and its resources, then the project layout would look as follows:

`ecommerce/
|
├── api/
|   ├── __init__.py
|   └── api.py
|
├── auth/
|   ├── templates/
|   |   └── auth/
|   |       ├── login.html
|   |       ├── forgot_password.html
|   |       └── signup.html
|   |
|   ├── __init__.py
|   └── auth.py
|
├── cart/
|   ├── templates/
|   |   └── cart/
|   |       ├── checkout.html
|   |       └── view.html
|   |
|   ├── __init__.py
|   └── cart.py
|
├── general/
|   ├── templates/
|   |   └── general/
|   |       └── index.html
|   |
|   ├── __init__.py
|   └── general.py
|
├── products/
|   ├── static/
|   |   └── view.js
|   |
|   ├── templates/
|   |   └── products/
|   |       ├── list.html
|   |       └── view.html
|   |
|   ├── __init__.py
|   └── products.py
|
├── static/
|   ├── logo.png
|   ├── main.css
|   └── generic.js
|
├── app.py
├── config.py
└── models.py` 

To organize code in this way, you move all views from  `app.py`  into the corresponding Flask Blueprint. You also moved templates and non-global static files. This structure makes it easier for you to find the code and resources related to a given functionality. For example, if you want to find the application logic about products, then you can go to the Products Blueprint in  `products/products.py`  instead of scrolling through  `app.py`.

Let’s see the Products Blueprint implementation in  `products/products.py`:

`from flask import Blueprint, render_template
from ecommerce.models import Product

products_bp = Blueprint('products_bp', __name__,
    template_folder='templates',
    static_folder='static', static_url_path='assets')

@products_bp.route('/')
def list():
    products = Product.query.all()
    return render_template('products/list.html', products=products)

@products_bp.route('/view/<int:product_id>')
def view(product_id):
    product = Product.query.get(product_id)
    return render_template('products/view.html', product=product)` 

This code defines the  `products_bp`  Flask Blueprint and contains only the code that’s related to product functionality. Since this Flask Blueprint has its own templates, you need to specify the  `template_folder`  relative to the Blueprint’s root in the  `Blueprint`  object creation. Since you specify  `static_folder='static'`  and  `static_url_path='assets'`, files in  `ecommerce/products/static/`  will be served under the  `/assets/`  URL.

Now you can move the rest of your code’s functionality to the corresponding Flask Blueprint. In other words, you can create Blueprints for API, authentication, cart, and general functionality. Once you’ve done so, the only code left in  `app.py`  will be code that deals with application initialization and Flask Blueprint registration:

`from flask import Flask

from ecommmerce.api.api import api_bp
from ecommmerce.auth.auth import auth_bp
from ecommmerce.cart.cart import cart_bp
from ecommmerce.general.general import general_bp
from ecommmerce.products.products import products_bp

app = Flask(__name__)

app.register_blueprint(api_bp, url_prefix='/api')
app.register_blueprint(auth_bp)
app.register_blueprint(cart_bp, url_prefix='/cart')
app.register_blueprint(general_bp)
app.register_blueprint(products_bp, url_prefix='/products')` 

Now,  `app.py`  simply imports and registers the Blueprints to extend the application. Since you use  `url_prefix`, you can avoid URL collisions between Flask Blueprint routes. For example, the URLs  `/products/`  and  `/cart/`  resolve to different endpoints defined in the  `products_bp`  and  `cart_bp`  Blueprints for the same route,  `/`.

### Including Templates

In Flask, when a view renders a template, the template file is searched in all the directories that were registered in the application’s  **template search path**. By default, this path is  `["/templates"]`, so templates are only searched for in the  `/templates`  directory inside the application’s root directory.

If you set the  `template_folder`  argument in a Blueprint’s creation, then its templates folder is added to the application’s template search path when the Flask Blueprint is registered. However, if there are duplicated file paths under different directories that are part of the template search path, then  **one will take precedence**, depending on their registration order.

For example, if a view requests the template  `view.html`  and there are files with this same name in different directories in the template search path, then one of these will take precedence over the other. Since it may be hard to remember the precedence order, it’s best to  **avoid having files under the same path**  in different template directories. That’s why the following structure for the templates in the application makes sense:

`ecommerce/
|
└── products/
    └── templates/
        └── products/
            ├── search.html
            └── view.html` 

At first, it may look redundant to have the Flask Blueprint name appear twice:

1.  As the Blueprint’s  **root**  directory
2.  Inside the  **templates**  directory

However, know that by doing this, you can avoid possible  **template name collisions**  between different Blueprints. Using this directory structure, any views requiring the  `view.html`  template for products can use  `products/view.html`  as the template file name when calling  `render_template`. This avoids conflicts with the  `view.html`  that belongs to the Cart Blueprint.

As a final note, it’s important to know that templates in the application’s  `template`  directory have  **greater precedence**  than those inside the Blueprint’s template directory. This can be useful to know if you want to override Flask Blueprint templates without actually modifying the template file.

For example, if you wanted to override the template  `products/view.html`  in the Products Blueprint, then you can accomplish this by creating a new file  `products/view.html`  in the application  `templates`  directory:

`ecommerce/
|
├── products/
|   └── templates/
|       └── products/
|           ├── search.html
|           └── view.html
|
└── templates/
        └── products/
            └── view.html` 

When you do this, your program will use  `templates/products/view.html`  instead of  `products/templates/products/view.html`  whenever a view requires the template  `products/view.html`.

### Providing Functionality Other Than Views

So far, you’ve only seen Blueprints that extend applications with views, but Flask Blueprints don’t have to provide just views! They can extend applications with  **templates, static files, and template filters**. For example, you could create a  **Flask Blueprint**  to provide a set of icons and use it across your applications. This would be the file structure for such a Blueprint:

`app/
|
└── icons/
    ├── static/
    |   ├── add.png
    |   ├── remove.png
    |   └── save.png
    |
    ├── __init__.py
    └── icons.py` 

The  `static`  folder contains the icon files and  `icons.py`  is the Flask Blueprint definition.

This is how  `icons.py`  might look:

`from flask import Blueprint

icons_bp = Blueprint('icons_bp', __name__,
    static_folder='static',
    static_url_path='icons')` 

This code defines the  `icons_bp`  Flask Blueprint that exposes the files in the static directory under the  `/icons/`  URL. Note that this Blueprint does not define any route.

When you can create Blueprints that package views and other types of content, you make your code and assets more reusable across your applications. You’ll learn more about Flask Blueprint reusability in the following section.

## How to Use Flask Blueprints to Improve Code Reuse

Besides code organization, there’s another advantage to structuring your Flask application as a  **collection of independent components**. You can reuse these components even across different applications! For example, if you created a Flask Blueprint that provides functionality for a contact form, then you can reuse it in all your applications.

You can also leverage Blueprints created by other developers to accelerate your work. While there’s no centralized repository for existing Flask Blueprints, you can find them using the  [Python Package Index](https://pypi.org/),  [GitHub Search](https://github.com/search?q=flask+blueprint), and web search engines. You can learn more about searching PyPI packages in  [What Is Pip? A Guide for New Pythonistas](https://realpython.com/what-is-pip/).

There are various Flask Blueprints and  **Flask Extensions**  (which are implemented using Blueprints) that provide functionality that you may find useful:

-   Authentication
-   Admin/CRUD generation
-   CMS functionality
-   And more!

Instead of coding your application from scratch, you may consider searching for an existing Flask Blueprint or Extension that you can reuse. Leveraging third-party Blueprints and Extensions can help you to reduce development time and keep your focus on your application’s core logic!

## Conclusion

In this tutorial, you’ve seen how Flask Blueprints work, how to use them, and how they can help you to organize your application’s code. Flask Blueprints are a great tool for dealing with application complexity as it increases.

**You’ve learned:**

-   What  **Flask Blueprints**  are and how they work
-   How you can  **implement and use**  a Flask Blueprint
-   How Flask Blueprints can help you to  **organize**  your application’s code
-   How you can use Flask Blueprints to ease the  **reusability**  of your own and third-party components
-   How using a Flask Blueprint in your project can reduce development time

You can use what you’ve learned in this tutorial to start organizing your applications as a set of blueprints. When you architect your applications this way, you’ll improve code reuse, maintainability, and teamwork!

> [Source : ](https://realpython.com/flask-blueprint/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyODkzODIzOV19
-->