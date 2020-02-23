
# Build a CRUD Web App with Python and Flask

In this three-part tutorial, we'll build a CRUD (Create, Read, Update, Delete) employee management web app using Flask, a microframework for Python.

## Python Flask for Beginners: Build a CRUD Web App with Python and Flask - Part One

I’ve named the app Project Dream Team, and it will have the following features:

1.  Users will be able to register and login as employees
2.  The administrator will be able to create, update, and delete departments and roles
3.  The administrator will be able to assign employees to a department and assign them roles
4.  The administrator will be able to view all employees and their details

Part One will cover:

1.  Users will be able to register and login as employees
2.  The administrator will be able to create, update, and delete departments and roles
3.  The administrator will be able to assign employees to a department and assign them roles
4.  The administrator will be able to view all employees and their details

Ready? Here we go!

### Prerequisites

This tutorial builds on my introductory tutorial,  [_Getting Started With Flask_](https://morioh.com/p/5d8eca44372e "*Getting Started With Flask*"), picking up where it left off. It assumes you have, to begin with, the following dependencies installed:

1.  Users will be able to register and login as employees
2.  The administrator will be able to create, update, and delete departments and roles
3.  The administrator will be able to assign employees to a department and assign them roles
4.  The administrator will be able to view all employees and their details

You should have a virtual environment set up and activated. You should also have the following file and directory structure:

```
&#x251C;&#x2500;&#x2500; dream-team
    &#xA0;&#xA0; &#x251C;&#x2500;&#x2500; app
    &#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; __init__.py
    &#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; templates
    &#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; models.py
     &#xA0; &#x2502;&#xA0;&#xA0; &#x2514;&#x2500;&#x2500; views.py
    &#xA0;&#xA0; &#x251C;&#x2500;&#x2500; config.py
   &#xA0; &#xA0; &#x251C;&#x2500;&#x2500; requirements.txt
   &#xA0;&#xA0;  &#x2514;&#x2500;&#x2500; run.py
```

This project structure groups the similar components of the application together. The  `dream-team`  directory houses all the project files. The  `app`  directory is the application package, and houses different but interlinked modules of the application. All templates are stored in the  `templates`  directory, all models are in the  `models.py`  file, and all routes are in the  `views.py`  file. The  `run.py`  file is the application's entry point, the  `config.py`  file contains the application configurations, and the  `requirements.txt`  file contains the software dependencies for the application.

If you don't have these set up, please visit the introductory tutorial and catch up!

### Database Setup

Flask has support for several relational database management systems, including  [SQLite](https://on.morioh.net/b0a3f595aa?r=https://sqlite.org/ "SQLite"),  [MySQL](https://on.morioh.net/b0a3f595aa?r=https://www.mysql.com/ "MySQL"), and  [PostgreSQL](https://on.morioh.net/b0a3f595aa?r=https://www.postgresql.org/ "PostgreSQL"). For this tutorial, we will be using MySQL. It’s popular and therefore has a lot of support, in addition to being scalable, secure, and rich in features.

We will install the following (remember to activate your virtual environment):

1.  Users will be able to register and login as employees
2.  The administrator will be able to create, update, and delete departments and roles
3.  The administrator will be able to assign employees to a department and assign them roles
4.  The administrator will be able to view all employees and their details

```
$ pip install flask-sqlalchemy mysql-python
```

We'll then create the MySQL database. Ensure you have MySQL installed and running, and then log in as the root user:

```
$ mysql -u root

mysql> CREATE USER &apos;dt_admin&apos;@&apos;localhost&apos; IDENTIFIED BY &apos;dt2016&apos;;
Query OK, 0 rows affected (0.00 sec)

mysql> CREATE DATABASE dreamteam_db;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON dreamteam_db . * TO &apos;dt_admin&apos;@&apos;localhost&apos;;
Query OK, 0 rows affected (0.00 sec)
```

We have now created a new user  `dt_admin`  with the password  `dt2016`, created a new database  `dreamteam_db`, and granted the new user all database privileges.

Next, let's edit the  `config.py`. Remove any exisiting code and add the following:

```py
# config.py

class Config(object):
    """
    Common configurations
    """

    # Put any configurations here that are common across all environments

class DevelopmentConfig(Config):
    """
    Development configurations
    """

    DEBUG = True
    SQLALCHEMY_ECHO = True

class ProductionConfig(Config):
    """
    Production configurations
    """

    DEBUG = False

app_config = {
    &apos;development&apos;: DevelopmentConfig,
    &apos;production&apos;: ProductionConfig
}
```

It is good practice to specify configurations for different environments. In the file above, we have specifed configurations for development, which we will use while building the app and running it locally, as well as production, which we will use when the app is deployed.

Some useful configuration variables are:

1.  Users will be able to register and login as employees
2.  The administrator will be able to create, update, and delete departments and roles
3.  The administrator will be able to assign employees to a department and assign them roles
4.  The administrator will be able to view all employees and their details

You can find more Flask configuration variables  [here](https://on.morioh.net/b0a3f595aa?r=http://flask.pocoo.org/docs/0.11/config/ "here")  and SQLAlchemy configuration variables  [here](https://on.morioh.net/b0a3f595aa?r=http://flask-sqlalchemy.pocoo.org/2.1/config/ "here").

Next, create an  `instance`  directory in the  `dream-team`  directory, and then create a  `config.py`  file inside it. We will put configuration variables here that will not be pushed to version control due to their sensitive nature. In this case, we put the secret key as well as the database URI which contains the database user password.

```py
# instance/config.py

SECRET_KEY = &apos;p9Bv<3Eid9%$i01&apos;
SQLALCHEMY_DATABASE_URI = &apos;mysql://dt_admin:dt2016@localhost/dreamteam_db&apos;
```

Now, let's edit the  `app/__init__.py`  file. Remove any existing code and add the following:

```py
# app/__init__.py

# third-party imports
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

# local imports
from config import app_config

# db variable initialization
db = SQLAlchemy()

def create_app(config_name):
    app = Flask(__name__, instance_relative_config=True)
    app.config.from_object(app_config[config_name])
    app.config.from_pyfile(&apos;config.py&apos;)
    db.init_app(app)

    return app
```

We've created a function,  `create_app`  that, given a configuration name, loads the correct configuration from the  `config.py`  file, as well as the configurations from the  `instance/config.py`  file. We have also created a  `db`  object which we will use to interact with the database.

Next, let's edit the  `run.py`  file:

```py
# run.py

import os

from app import create_app

config_name = os.getenv(&apos;FLASK_CONFIG&apos;)
app = create_app(config_name)

if __name__ == &apos;__main__&apos;:
    app.run()
```

We create the app by running the  `create_app`  function and passing in the configuration name. We get this from the OS environment variable  `FLASK_CONFIG`. Because we are in development, we should set the environment variable to  `development`.

Let's run the app to ensure everything is working as expected. First, delete the  `app/views.py`  file as well as the  `app/templates`  directory as we will not be needing them going forward. Next, add a temporary route to the  `app/__init__.py`  file as follows:

```py
# app/__init__.py

# existing code remains

def create_app(config_name):
    # existing code remains

    # temporary route
    @app.route(&apos;/&apos;)
    def hello_world():
        return &apos;Hello, World!&apos;

    return app
```

Make sure you set the  `FLASK_CONFIG`  and  `FLASK_APP`  environment variables before running the app:

```py
$ export FLASK_CONFIG=development
$ export FLASK_APP=run.py
$ flask run
 * Serving Flask app "run"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

We can see the “Hello, World” string we set in the route. The app is working well so far.

### Models

Now to work on the models. Remember that a model is a representation of a database table in code. We'll need three models:  `Employee`,  `Department`, and  `Role`.

But first, let’s install  [Flask-Login](https://on.morioh.net/b0a3f595aa?r=https://flask-login.readthedocs.io/en/latest/ "Flask-Login"), which will help us with user management and handle logging in, logging out, and user sessions. The  `Employee`  model will inherit from Flask-Login’s  `UserMixin`  class which will make it easier for us to make use of its properties and methods.

```py
$ pip install flask-login
```

To use Flask-Login, we need to create a LoginManager object and initialize it in the  `app/__init__.py`  file. First, remove the route we added earlier, and then add the following:

```py
# app/__init__.py

# after existing third-party imports
from flask_login import LoginManager

# after the db variable initialization
login_manager = LoginManager()

def create_app(config_name):
    # existing code remains

    login_manager.init_app(app)
    login_manager.login_message = "You must be logged in to access this page."
    login_manager.login_view = "auth.login"

    return app
```

In addition to initializing the LoginManager object, we've also added a  `login_view`  and  `login_message`  to it. This way, if a user tries to access a page that they are not authorized to, it will redirect to the specified view and display the specified message. We haven't created the  `auth.login`  view yet, but we will when we get to authentication.

Now add the following code to the  `app/models.py`  file:

```py
# app/models.py

from flask_login import UserMixin
from werkzeug.security import generate_password_hash, check_password_hash

from app import db, login_manager

class Employee(UserMixin, db.Model):
    """
    Create an Employee table
    """

    # Ensures table will be named in plural and not in singular
    # as is the name of the model
    __tablename__ = &apos;employees&apos;

    id = db.Column(db.Integer, primary_key=True)
    email = db.Column(db.String(60), index=True, unique=True)
    username = db.Column(db.String(60), index=True, unique=True)
    first_name = db.Column(db.String(60), index=True)
    last_name = db.Column(db.String(60), index=True)
    password_hash = db.Column(db.String(128))
    department_id = db.Column(db.Integer, db.ForeignKey(&apos;departments.id&apos;))
    role_id = db.Column(db.Integer, db.ForeignKey(&apos;roles.id&apos;))
    is_admin = db.Column(db.Boolean, default=False)

    @property
    def password(self):
        """
        Prevent pasword from being accessed
        """
        raise AttributeError(&apos;password is not a readable attribute.&apos;)

    @password.setter
    def password(self, password):
        """
        Set password to a hashed password
        """
        self.password_hash = generate_password_hash(password)

    def verify_password(self, password):
        """
        Check if hashed password matches actual password
        """
        return check_password_hash(self.password_hash, password)

    def __repr__(self):
        return &apos;<Employee: {}>&apos;.format(self.username)

# Set up user_loader
@login_manager.user_loader
def load_user(user_id):
    return Employee.query.get(int(user_id))

class Department(db.Model):
    """
    Create a Department table
    """

    __tablename__ = &apos;departments&apos;

    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(60), unique=True)
    description = db.Column(db.String(200))
    employees = db.relationship(&apos;Employee&apos;, backref=&apos;department&apos;,
                                lazy=&apos;dynamic&apos;)

    def __repr__(self):
        return &apos;<Department: {}>&apos;.format(self.name)

class Role(db.Model):
    """
    Create a Role table
    """

    __tablename__ = &apos;roles&apos;

    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(60), unique=True)
    description = db.Column(db.String(200))
    employees = db.relationship(&apos;Employee&apos;, backref=&apos;role&apos;,
                                lazy=&apos;dynamic&apos;)

    def __repr__(self):
        return &apos;<Role: {}>&apos;.format(self.name)
```

In the  `Employee`  model, we make use of some of Werkzeug's handy security helper methods,  `generate_password_hash`, which allows us to hash passwords, and  `check_password_hash`, which allows us ensure the hashed password matches the password. To enhance security, we have a  `password`  method which ensures that the password can never be accessed; instead an error will be raised. We also have two foreign key fields,  `department_id`  and  `role_id`, which refer to the ID's of the department and role assigned to the employee.

Note that we have an  `is_admin`  field which is set to  `False`  by default. We will override this when creating the admin user. Just after the  `Employee`  model, we have a  `user_loader`  callback, which Flask-Login uses to reload the user object from the user ID stored in the session.

The  `Department`  and  `Role`  models are quite similar. Both have  `name`  and  `description`  fields. Additionally, both have a one-to-many relationship with the  `Employee`  model (one department or role can have many employees). We define this in both models using the  `employees`  field.  `backref`  allows us to create a new property on the  `Employee`  model such that we can use  `employee.department`  or  `employee.role`  to get the department or role assigned to that employee.  `lazy`  defines how the data will be loaded from the database; in this case it will be loaded dynamically, which is ideal for managing large collections.

### Migration

Migrations allow us to manage changes we make to the models, and propagate these changes in the database. For example, if later on we make a change to a field in one of the models, all we will need to do is create and apply a migration, and the database will reflect the change.

We’ll begin by installing  [Flask-Migrate](https://on.morioh.net/b0a3f595aa?r=https://flask-migrate.readthedocs.io/en/latest/ "Flask-Migrate"), which will handle the database migrations using Alembic, a lightweight database migration tool. Alembic emits  `ALTER`  statements to a database thus implememting changes made to the models. It also auto-generates minimalistic migration scripts, which may be complex to write.

```py
$ pip install flask-migrate
```

We'll need to edit the  `app/__init__.py`  file:

```py
# app/__init__.py

# after existing third-party imports
from flask_migrate import Migrate

# existing code remains

def create_app(config_name):
    # existing code remains

    migrate = Migrate(app, db)

    from app import models

    return app
```

We have created a  `migrate`  object which will allow us to run migrations using Flask-Migrate. We have also imported the models from the  `app`  package. Next, we'll run the following command to create a migration repository:

```py
$ flask db init
```

This creates a  `migrations`  directory in the  `dream-team`  directory:

```py
&#x2514;&#x2500;&#x2500; migrations
    &#x251C;&#x2500;&#x2500; README
    &#x251C;&#x2500;&#x2500; alembic.ini
    &#x251C;&#x2500;&#x2500; env.py
    &#x251C;&#x2500;&#x2500; script.py.mako
    &#x2514;&#x2500;&#x2500; versions
```

Next, we will create the first migration:

```py
$ flask db migrate
```

Finally, we'll apply the migration:

```py
$ flask db upgrade
```

We've sucessfully created tables based on the models we wrote! Let's check the MySQL database to confirm this:

```py
$ mysql -u root

mysql> use dreamteam_db;

mysql> show tables;
+------------------------+
| Tables_in_dreamteam_db |
+------------------------+
| alembic_version        |
| departments            |
| employees              |
| roles                  |
+------------------------+
4 rows in set (0.00 sec)
```

### Blueprints

Blueprints are great for organising a flask app into components, each with its own views and forms. I find that blueprints make for a cleaner and more organised project structure because each blueprint is a distinct component that addresses a specific functionality of the app. Each blueprint can even have its own cutsom URL prefix or subdomain. Blueprints are particularly convenient for large applications.

We're going to have three blueprints in this app:

1.  Users will be able to register and login as employees
2.  The administrator will be able to create, update, and delete departments and roles
3.  The administrator will be able to assign employees to a department and assign them roles
4.  The administrator will be able to view all employees and their details

Create the relevant files and directories so that your directory structure resembles this:

```
&#x2514;&#x2500;&#x2500; dream-team
    &#x251C;&#x2500;&#x2500; app
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; __init__.py
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; admin
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; __init__.py
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; forms.py
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x2514;&#x2500;&#x2500; views.py
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; auth
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; __init__.py
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; forms.py
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x2514;&#x2500;&#x2500; views.py
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; home
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; __init__.py
    &#x2502;&#xA0;&#xA0; &#x2502;&#xA0;&#xA0; &#x2514;&#x2500;&#x2500; views.py
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; models.py
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; static
    &#x2502;&#xA0;&#xA0; &#x2514;&#x2500;&#x2500; templates
    &#x251C;&#x2500;&#x2500; config.py
    &#x251C;&#x2500;&#x2500; instance
    &#x2502;&#xA0;&#xA0; &#x2514;&#x2500;&#x2500; config.py
    &#x251C;&#x2500;&#x2500; migrations
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; README
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; alembic.ini
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; env.py
    &#x2502;&#xA0;&#xA0; &#x251C;&#x2500;&#x2500; script.py.mako
    &#x2502;&#xA0;&#xA0; &#x2514;&#x2500;&#x2500; versions
    &#x2502;&#xA0;&#xA0;     &#x2514;&#x2500;&#x2500; a1a1d8b30202_.py
    &#x251C;&#x2500;&#x2500; requirements.txt
    &#x2514;&#x2500;&#x2500; run.py
```

I chose not to have  `static`  and  `templates`  directories for each blueprint, because all the application templates will inherit from the same base template and use the same CSS file. Instead, the  `templates`  directory will have sub-directories for each blueprint so that blueprint templates can be grouped together.

In each blueprint's  `__init__.py`  file, we need to create a Blueprint object and initialize it with a name. We also need to import the views.

```py
# app/admin/__init__.py

from flask import Blueprint

admin = Blueprint(&apos;admin&apos;, __name__)

from . import views
# app/auth/__init__.py

from flask import Blueprint

auth = Blueprint(&apos;auth&apos;, __name__)

from . import views
# app/home/__init__.py

from flask import Blueprint

home = Blueprint(&apos;home&apos;, __name__)

from . import views
```

Then, we can register the blueprints on the app in the  `app/__init__.py`  file, like so:

```py
# app/__init__.py

# existing code remains

def create_app(config_name):
    # existing code remains

    from app import models

    from .admin import admin as admin_blueprint
    app.register_blueprint(admin_blueprint, url_prefix=&apos;/admin&apos;)

    from .auth import auth as auth_blueprint
    app.register_blueprint(auth_blueprint)

    from .home import home as home_blueprint
    app.register_blueprint(home_blueprint)

    return app
```

We have imported each blueprint object and registered it. For the  `admin`  blueprint, we have added a url prefix,  `/admin`. This means that all the views for this blueprint will be accessed in the browser with the url prefix  `admin`.

### Home Blueprint

Time to work on fleshing out the blueprints! We'll start with the  `home`  blueprint, which will have the homepage as well as the dashboard.

```py
# app/home/views.py

from flask import render_template
from flask_login import login_required

from . import home

@home.route(&apos;/&apos;)
def homepage():
    """
    Render the homepage template on the / route
    """
    return render_template(&apos;home/index.html&apos;, title="Welcome")

@home.route(&apos;/dashboard&apos;)
@login_required
def dashboard():
    """
    Render the dashboard template on the /dashboard route
    """
    return render_template(&apos;home/dashboard.html&apos;, title="Dashboard")
```

Each view function has a decorator,  `home.route`, which has a URL route as a parameter (remember that  `home`  is the name of the blueprint as specified in the  `app/home/__init__.py`  file). Each view handles requests to the specified URL.

The  `homepage`  view renders the home template, while the  `dashboard`  view renders the dashboard template. Note that the  `dashboard`  view has a  `login_required`  decorator, meaning that users must be logged in to access it.

Now to work on the base template, which all other templates will inherit from. Create a  `base.html`  file in the  `app/templates`  directory and add the following code:

```html
<!-- app/templates/base.html -->

<!DOCTYPE html>
<html lang="en">
<head>
    <title>{{ title }} | Project Dream Team</title>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <link href="{{ url_for(&apos;static&apos;, filename=&apos;css/style.css&apos;) }}" rel="stylesheet">
    <link rel="shortcut icon" href="{{ url_for(&apos;static&apos;, filename=&apos;img/favicon.ico&apos;) }}">
</head>
<body>
    <nav class="navbar navbar-default navbar-fixed-top topnav" role="navigation">
        <div class="container topnav">
          <div class="navbar-header">
              <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                  <span class="sr-only">Toggle navigation</span>
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
              </button>
              <a class="navbar-brand topnav" href="{{ url_for(&apos;home.homepage&apos;) }}">Project Dream Team</a>
          </div>
          <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
              <ul class="nav navbar-nav navbar-right">
                  <li><a href="{{ url_for(&apos;home.homepage&apos;) }}">Home</a></li>
                  <li><a href="#">Register</a></li>
                  <li><a href="#">Login</a></li>
              </ul>
          </div>
        </div>
    </nav>
    <div class="wrapper">
      {% block body %}
      {% endblock %}
      <div class="push"></div>
    </div>
    <footer>
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <ul class="list-inline">
                        <li><a href="{{ url_for(&apos;home.homepage&apos;) }}">Home</a></li>
                        <li class="footer-menu-divider">&#x22C5;</li>
                        <li><a href="#">Register</a></li>
                        <li class="footer-menu-divider">&#x22C5;</li>
                        <li><a href="#">Login</a></li>
                    </ul>
                    <p class="copyright text-muted small">Copyright &#xA9; 2016. All Rights Reserved</p>
                </div>
            </div>
        </div>
    </footer>
</body>
</html>
```

Note that we use  `#`  for the Register and Login links. We will update this when we are working on the  `auth`  blueprint.

Next, create a  `home`  directory inside the  `app/templates`  directory. The homepage template,  `index.html`, will go inside it:

```html
<!-- app/templates/home/index.html -->

{% extends "base.html" %}
{% block title %}Home{% endblock %}
{% block body %}
<div class="intro-header">
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <div class="intro-message">
                    <h1>Project Dream Team</h1>
                    <h3>The best company in the world!</h3>
                    <hr class="intro-divider">
                    </ul>
                </div>
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

Inside the  `static`  directory, add  `css`  and  `img`  directories. Add the following CSS file,  `style.css`, to your  `static/css`  directory (note that you will need a background image,  `intro-bg.jpg`, as well as a favicon in your  `static/img`  directory):

```css
/* app/static/css/style.css */

body, html {
    width: 100%;
    height: 100%;
}

body, h1, h2, h3 {
    font-family: "Lato", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-weight: 700;
}

a, .navbar-default .navbar-brand, .navbar-default .navbar-nav>li>a {
  color: #aec251;
}

a:hover, .navbar-default .navbar-brand:hover, .navbar-default .navbar-nav>li>a:hover {
  color: #687430;
}

footer {
    padding: 50px 0;
    background-color: #f8f8f8;
}

p.copyright {
    margin: 15px 0 0;
}

.alert-info {
    width: 50%;
    margin: auto;
    color: #687430;
    background-color: #e6ecca;
    border-color: #aec251;
}

.btn-default {
    border-color: #aec251;
    color: #aec251;
}

.btn-default:hover {
    background-color: #aec251;
}

.center {
    margin: auto;
    width: 50%;
    padding: 10px;
}

.content-section {
    padding: 50px 0;
    border-top: 1px solid #e7e7e7;
}

.footer, .push {
  clear: both;
  height: 4em;
}

.intro-divider {
    width: 400px;
    border-top: 1px solid #f8f8f8;
    border-bottom: 1px solid rgba(0,0,0,0.2);
}

.intro-header {
    padding-top: 50px;
    padding-bottom: 50px;
    text-align: center;
    color: #f8f8f8;
    background: url(../img/intro-bg.jpg) no-repeat center center;
    background-size: cover;
    height: 100%;
}

.intro-message {
    position: relative;
    padding-top: 20%;
    padding-bottom: 20%;
}

.intro-message > h1 {
    margin: 0;
    text-shadow: 2px 2px 3px rgba(0,0,0,0.6);
    font-size: 5em;
}

.intro-message > h3 {
    text-shadow: 2px 2px 3px rgba(0,0,0,0.6);
}

.lead {
    font-size: 18px;
    font-weight: 400;
}

.topnav {
    font-size: 14px;
}

.wrapper {
  min-height: 100%;
  height: auto !important;
  height: 100%;
  margin: 0 auto -4em;
}
```

Run the app; you should be able to see the homepage now.

### Auth Blueprint

For the  `auth`  blueprint, we’ll begin by creating the registration and login forms. We’ll use  [Flask-WTF](https://on.morioh.net/b0a3f595aa?r=https://flask-wtf.readthedocs.io/en/stable/ "Flask-WTF"), which will allow us to create forms that are secure (thanks to CSRF protection and reCAPTCHA support).

```py
pip install Flask-WTF
```

Now to write the code for the forms:

```py
# app/auth/forms.py

from flask_wtf import FlaskForm
from wtforms import PasswordField, StringField, SubmitField, ValidationError
from wtforms.validators import DataRequired, Email, EqualTo

from ..models import Employee

class RegistrationForm(FlaskForm):
    """
    Form for users to create new account
    """
    email = StringField(&apos;Email&apos;, validators=[DataRequired(), Email()])
    username = StringField(&apos;Username&apos;, validators=[DataRequired()])
    first_name = StringField(&apos;First Name&apos;, validators=[DataRequired()])
    last_name = StringField(&apos;Last Name&apos;, validators=[DataRequired()])
    password = PasswordField(&apos;Password&apos;, validators=[
                                        DataRequired(),
                                        EqualTo(&apos;confirm_password&apos;)
                                        ])
    confirm_password = PasswordField(&apos;Confirm Password&apos;)
    submit = SubmitField(&apos;Register&apos;)

    def validate_email(self, field):
        if Employee.query.filter_by(email=field.data).first():
            raise ValidationError(&apos;Email is already in use.&apos;)

    def validate_username(self, field):
        if Employee.query.filter_by(username=field.data).first():
            raise ValidationError(&apos;Username is already in use.&apos;)

class LoginForm(FlaskForm):
    """
    Form for users to login
    """
    email = StringField(&apos;Email&apos;, validators=[DataRequired(), Email()])
    password = PasswordField(&apos;Password&apos;, validators=[DataRequired()])
    submit = SubmitField(&apos;Login&apos;)
```

Flask-WTF has a number of validators that make writing forms much easier. All the fields in the models have the  `DataRequired`  validator, which means that users will be required to fill all of them in order to register or login.

For the registration form, we require users to fill in their email address, username, first name, last name, and their password twice. We use the  `Email`  validator to ensure valid email formats are used (e.g  `some-name@some-domain.com`.) We use the  `EqualTo`  validator to confirm that the  `password`  and  `confirm_password`  fields in the  `RegistrationForm`  match. We also create methods (`validate_email`  and  `validate_username`) to ensure that the email and username entered have not been used before.

The  `submit`  field in both forms will be represented as a button that users will be able to click to register and login respectively.

With the forms in place, we can write the views:

```py
# app/auth/views.py

from flask import flash, redirect, render_template, url_for
from flask_login import login_required, login_user, logout_user

from . import auth
from forms import LoginForm, RegistrationForm
from .. import db
from ..models import Employee

@auth.route(&apos;/register&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
def register():
    """
    Handle requests to the /register route
    Add an employee to the database through the registration form
    """
    form = RegistrationForm()
    if form.validate_on_submit():
        employee = Employee(email=form.email.data,
                            username=form.username.data,
                            first_name=form.first_name.data,
                            last_name=form.last_name.data,
                            password=form.password.data)

        # add employee to the database
        db.session.add(employee)
        db.session.commit()
        flash(&apos;You have successfully registered! You may now login.&apos;)

        # redirect to the login page
        return redirect(url_for(&apos;auth.login&apos;))

    # load registration template
    return render_template(&apos;auth/register.html&apos;, form=form, title=&apos;Register&apos;)

@auth.route(&apos;/login&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
def login():
    """
    Handle requests to the /login route
    Log an employee in through the login form
    """
    form = LoginForm()
    if form.validate_on_submit():

        # check whether employee exists in the database and whether
        # the password entered matches the password in the database
        employee = Employee.query.filter_by(email=form.email.data).first()
        if employee is not None and employee.verify_password(
                form.password.data):
            # log employee in
            login_user(employee)

            # redirect to the dashboard page after login
            return redirect(url_for(&apos;home.dashboard&apos;))

        # when login details are incorrect
        else:
            flash(&apos;Invalid email or password.&apos;)

    # load login template
    return render_template(&apos;auth/login.html&apos;, form=form, title=&apos;Login&apos;)

@auth.route(&apos;/logout&apos;)
@login_required
def logout():
    """
    Handle requests to the /logout route
    Log an employee out through the logout link
    """
    logout_user()
    flash(&apos;You have successfully been logged out.&apos;)

    # redirect to the login page
    return redirect(url_for(&apos;auth.login&apos;))
```

Just like in the  `home`  blueprint, each view here handles requests to the specified URL. The  `register`  view creates an instance of the  `Employee`  model class using the registration form data to populate the fields, and then adds it to the database. This esentially registers a new employee.

The  `login`  view queries the database to check whether an employee exists with an email address that matches the email provided in the login form data. It then uses the  `verify_password`  method to check that the password in the database for the employee matches the password provided in the login form data. If both of these are true, it proceeds to log the user in using the  `login_user`  method provided by Flask-Login.

The  `logout`  view has the  `login_required`  decorator, which means that a user must be logged in to access it. It calles the  `logout_user`  method provided by Flask-Login to log the user out.

Note the use of  `flash`  method, which allows us to use Flask’s  [message flashing](https://on.morioh.net/b0a3f595aa?r=http://flask.pocoo.org/docs/0.11/patterns/flashing/ "message flashing")  feature. This allows us to communicate feedback to the user, such as informing them of successful registration or unsuccessful login.

Finally, let’s work on the templates. First, we’ll install  [Flask-Bootstrap](https://on.morioh.net/b0a3f595aa?r=https://pythonhosted.org/Flask-Bootstrap/index.html "Flask-Bootstrap")  so we can use its  `wtf`  and  `utils`  libraries. The  `wtf`  library will allow us to quickly generate forms in the templates based on the forms in the  `forms.py`  file. The  `utils`  library will allow us to display the flash messages we set earlier to give feedback to the user.

```py
pip install flask-bootstrap
```

We need to edit the  `app/__init__.py`  file to use Flask-Bootstrap:

```py
# app/__init__.py

# after existing third-party imports
from flask_bootstrap import Bootstrap

# existing code remains

def create_app(config_name):
    # existing code remains

    Bootstrap(app)

    from app import models

    # blueprint registration remains here

    return app
```

We've made quite a number of edits to the  `app/__init__.py`  file. This is the final version of the file and how it should look at this point (note that I have re-arranged the imports and variables in alphabetical order):

```py
# app/__init__.py

# third-party imports
from flask import Flask
from flask_bootstrap import Bootstrap
from flask_login import LoginManager
from flask_migrate import Migrate
from flask_sqlalchemy import SQLAlchemy

# local imports
from config import app_config

db = SQLAlchemy()
login_manager = LoginManager()

def create_app(config_name):
    app = Flask(__name__, instance_relative_config=True)
    app.config.from_object(app_config[config_name])
    app.config.from_pyfile(&apos;config.py&apos;)

    Bootstrap(app)
    db.init_app(app)
    login_manager.init_app(app)
    login_manager.login_message = "You must be logged in to access this page."
    login_manager.login_view = "auth.login"
    migrate = Migrate(app, db)

    from app import models

    from .admin import admin as admin_blueprint
    app.register_blueprint(admin_blueprint, url_prefix=&apos;/admin&apos;)

    from .auth import auth as auth_blueprint
    app.register_blueprint(auth_blueprint)

    from .home import home as home_blueprint
    app.register_blueprint(home_blueprint)

    return app
```

We need two templates for the  `auth`  blueprint:  `register.html`  and  `login.html`, which we'll create in an  `auth`  directory inside the  `templates`  directory.

```html
<!-- app/templates/auth/register.html -->

{% import "bootstrap/wtf.html" as wtf %}
{% extends "base.html" %}
{% block title %}Register{% endblock %}
{% block body %}
<div class="content-section">
  <div class="center">
    <h1>Register for an account</h1>
    <br/>
    {{ wtf.quick_form(form) }}
  </div>
</div>
{% endblock %}
<!-- app/templates/auth/login.html -->

{% import "bootstrap/utils.html" as utils %}
{% import "bootstrap/wtf.html" as wtf %}
{% extends "base.html" %}
{% block title %}Login{% endblock %}
{% block body %}
<div class="content-section">
  <br/>
  {{ utils.flashed_messages() }}
  <br/>
  <div class="center">
    <h1>Login to your account</h1>
    <br/>
    {{ wtf.quick_form(form) }}
  </div>
</div>
{% endblock %}
```

The forms are loaded from the  `app/auth/views.py`  file, where we specified which template files to display for each view. Remember the Register and Login links in the base template? Let's update them now so we can access the pages from the menus:

```html
<!-- app/templates/base.html -->

<!-- Modify nav bar menu -->
<ul class="nav navbar-nav navbar-right">
    <li><a href="{{ url_for(&apos;home.homepage&apos;) }}">Home</a></li>
    <li><a href="{{ url_for(&apos;auth.register&apos;) }}">Register</a></li>
    <li><a href="{{ url_for(&apos;auth.login&apos;) }}">Login</a></li>
</ul>

<!-- Modify footer menu -->
<ul class="list-inline">
    <li><a href="{{ url_for(&apos;home.homepage&apos;) }}">Home</a></li>
    <li class="footer-menu-divider">&#x22C5;</li>
    <li><a href="{{ url_for(&apos;auth.register&apos;) }}">Register</a></li>
    <li class="footer-menu-divider">&#x22C5;</li>
    <li><a href="{{ url_for(&apos;auth.login&apos;) }}">Login</a></li>
</ul>
```

Run the app again and click on the Register and Login menu links. You should see the templates loaded with the appropriate form.

Try to fill out the registration form; you should be able to register a new employee. After registration, you should be redirected to the login page, where you will see the flash message we configured in the  `app/auth/views.py`  file, inviting you to login.

Logging in should be successful; however you should get a  `Template Not Found`  error after logging in, because the  `dashboard.html`  template has not been created yet. Let's do that now:

```html
<!-- app/templates/home/dashboard.html -->

{% extends "base.html" %}
{% block title %}Dashboard{% endblock %}
{% block body %}
<div class="intro-header">
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <div class="intro-message">
                    <h1>The Dashboard</h1>
                    <h3>We made it here!</h3>
                    <hr class="intro-divider">
                    </ul>
                </div>
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

Refresh the page. You'll notice that the navigation menu still has the register and login links, even though we are already logged in. We'll need to modify it to show a logout link when a user is already authenticated. We will also include a  `Hi, username!`  message in the nav bar:

```html
<!-- app/templates/base.html -->

<!-- In the head tag, include link to Font Awesome CSS so we can use icons -->
<link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet">

<!-- Modify nav bar menu -->
<ul class="nav navbar-nav navbar-right">
    {% if current_user.is_authenticated %}
      <li><a href="{{ url_for(&apos;home.dashboard&apos;) }}">Dashboard</a></li>
      <li><a href="{{ url_for(&apos;auth.logout&apos;) }}">Logout</a></li>
      <li><a><i class="fa fa-user"></i>  Hi, {{ current_user.username }}!</a></li>
    {% else %}
      <li><a href="{{ url_for(&apos;home.homepage&apos;) }}">Home</a></li>
      <li><a href="{{ url_for(&apos;auth.register&apos;) }}">Register</a></li>
      <li><a href="{{ url_for(&apos;auth.login&apos;) }}">Login</a></li>
    {% endif %}
</ul>

<!-- Modify footer menu -->
<ul class="list-inline">
    <li><a href="{{ url_for(&apos;home.homepage&apos;) }}">Home</a></li>
    <li class="footer-menu-divider">&#x22C5;</li>
    {% if current_user.is_authenticated %}
      <li><a href="{{ url_for(&apos;auth.logout&apos;) }}">Logout</a></li>
    {% else %}
      <li><a href="{{ url_for(&apos;auth.register&apos;) }}">Register</a></li>
      <li class="footer-menu-divider">&#x22C5;</li>
      <li><a href="{{ url_for(&apos;auth.login&apos;) }}">Login</a></li>
    {% endif %}
</ul>
```

Note how we use  `if-else`  statements in the templates. Also, take note of the  `current_user`  proxy provided by Flask-Login, which allows us to check whether the user is authenticated and to get the user's username.

Logging out will take you back to the login page:

Attempting to access the dashboard page without logging in will redirect you to the login page and display the message we set in the  `app/__init__.py`  file:

Notice that the URL is configured such that once you log in, you will be redirected to the page you initially attempted to access, which in this case is the dashboard.

### Conclusion

That's it for Part One! We've covered quite a lot: setting up a MySQL database, creating models, migrating the database, and handling registration, login, and logout. Good job for making it this far!

Watch this space for Part Two, which will cover the CRUD functionality of the app, allowing admin users to add, list, edit, and delete departments and roles, as well as assign them to employees.

## Python Flask for Beginners: Build a CRUD Web App with Python and Flask - Part Two

This is Part Two of a three-part tutorial to build an employee management web app, named Project Dream Team. In Part One) of the tutorial, we set up a MySQL database using MySQL-Python and Flask-SQLAlchemy. We created models, migrated the database, and worked on the  `home`  and  `auth`  blueprints and templates. By the end of Part One, we had a working app that had a homepage, registration page, login page, and dashboard. We could register a new user, login, and logout.

In Part Two, we will work on:

1.  Creating an admin user and admin dashboard
2.  Creating, listing, editing and deleting departments
3.  Creating, listing, editing and deleting roles
4.  Assigning departments and roles to employees

### Admin User

We'll start by creating an admin user through the command line. Flask provides a handy command,  `flask shell`, that allows us to use an interactive Python shell for use with Flask apps.

```py
$ flask shell
>>> from app.models import Employee
>>> from app import db
>>> admin = Employee(email="admin@admin.com",username="admin",password="admin2016",is_admin=True)
>>> db.session.add(admin)
>>> db.session.commit()


```

We've just created a user with a username,  `admin`, and a password,  `admin2016`. Recall that we set the  `is_admin`  field to default to  `False`  in the  `Employee`  model. To create the admin user above, we override the default value of  `is_admin`  and set it to  `True`.

### Admin Dashboard

Now that we have an admin user, we need to add a view for an admin dashboard. We also need to ensure that once the admin user logs in, they are redirected to the admin dashboard and not the one for non-admin users. We will do this in the  `home`  blueprint.

```py
# app/home/views.py

# update imports
from flask import abort, render_template
from flask_login import current_user, login_required

# add admin dashboard view
@home.route(&apos;/admin/dashboard&apos;)
@login_required
def admin_dashboard():
    # prevent non-admins from accessing the page
    if not current_user.is_admin:
        abort(403)

    return render_template(&apos;home/admin_dashboard.html&apos;, title="Dashboard")
# app/auth/views.py

# Edit the login view to redirect to the admin dashboard if employee is an admin

@auth.route(&apos;/login&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
def login():
    form = LoginForm()
    if form.validate_on_submit():

        # check whether employee exists in the database and whether
        # the password entered matches the password in the database
        employee = Employee.query.filter_by(email=form.email.data).first()
        if employee is not None and employee.verify_password(
                form.password.data):
            # log employee in
            login_user(employee)

            # redirect to the appropriate dashboard page
            if employee.is_admin:
                return redirect(url_for(&apos;home.admin_dashboard&apos;))
            else:
                return redirect(url_for(&apos;home.dashboard&apos;))

        # when login details are incorrect
        else:
            flash(&apos;Invalid email or password.&apos;)

    # load login template
    return render_template(&apos;auth/login.html&apos;, form=form, title=&apos;Login&apos;)
```

Next we'll create the admin dashboard template. Create an  `admin_dashboard.html`  file in the  `templates/home`  directory, and then add the following code in it:

```html
<!-- app/templates/home/admin_dashboard.html -->

{% extends "base.html" %}
{% block title %}Admin Dashboard{% endblock %}
{% block body %}
<div class="intro-header">
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <div class="intro-message">
                    <h1>Admin Dashboard</h1>
                    <h3>For administrators only!</h3>
                    <hr class="intro-divider">
                    </ul>
                </div>
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

Now we need to edit the base template to show a different menu for the admin user.

```html
<!-- app/templates/base.html -->

<!-- Modify nav bar menu -->
<ul class="nav navbar-nav navbar-right">
    {% if current_user.is_authenticated %}
      {% if current_user.is_admin %}
        <li><a href="{{ url_for(&apos;home.admin_dashboard&apos;) }}">Dashboard</a></li>
        <li><a href="#">Departments</a></li>
        <li><a href="#">Roles</a></li>
        <li><a href="#">Employees</a></li>
      {% else %}
        <li><a href="{{ url_for(&apos;home.dashboard&apos;) }}">Dashboard</a></li>
      {% endif %}
      <li><a href="{{ url_for(&apos;auth.logout&apos;) }}">Logout</a></li>
      <li><a><i class="fa fa-user"></i>  Hi, {{ current_user.username }}!</a></li>
    {% else %}
      <li><a href="{{ url_for(&apos;home.homepage&apos;) }}">Home</a></li>
      <li><a href="{{ url_for(&apos;auth.register&apos;) }}">Register</a></li>
      <li><a href="{{ url_for(&apos;auth.login&apos;) }}">Login</a></li>
    {% endif %}
</ul>
```

In the menu above, we make use of the  `current_user`  proxy from Flask-Login to check whether the current user is an admin. If they are, we display the admin menu which will allow them to navigate to the Departments, Roles and Employees pages. Notice that we use  `#`  for the links in the admin menu. We will update this after we have created the respective views.

Now run the app and login as the admin user that we just created. You should see the admin dashboard:

Let's test the error we set in the  `home/views.py`  file to prevent non-admin users from accessing the admin dashboard. Log out and then log in as a regular user. In your browser's address bar, manually enter the following URL:  `<a href="http://127.0.0.1:5000/admin/dashboard" target="_blank">http://127.0.0.1:5000/admin/dashboard</a>`. You should get a  `403 Forbidden`  error. It looks pretty boring now, but don't worry, we'll create custom error pages in Part Three!

### Departments

Now we'll start working on the  `admin`  blueprint, which has the bulk of the functionality in the application. We'll begin by building out CRUD functionality for the departments.

### Forms

We'll start with the  `admin/forms.py`  file, where we'll create a form to add and edit departments.

```py
# app/admin/forms.py

from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

class DepartmentForm(FlaskForm):
    """
    Form for admin to add or edit a department
    """
    name = StringField(&apos;Name&apos;, validators=[DataRequired()])
    description = StringField(&apos;Description&apos;, validators=[DataRequired()])
    submit = SubmitField(&apos;Submit&apos;)
```

The form is pretty simple and has only two fields,  `name`  and  `department`, both of which are required. We enforce this using the  `DataRequired()`  validator from WTForms. Note that we will use the same form for adding and editing departments.

### Views

Now, let's work on the views:

```py
# app/admin/views.py

from flask import abort, flash, redirect, render_template, url_for
from flask_login import current_user, login_required

from . import admin
from forms import DepartmentForm
from .. import db
from ..models import Department

def check_admin():
    """
    Prevent non-admins from accessing the page
    """
    if not current_user.is_admin:
        abort(403)

# Department Views

@admin.route(&apos;/departments&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def list_departments():
    """
    List all departments
    """
    check_admin()

    departments = Department.query.all()

    return render_template(&apos;admin/departments/departments.html&apos;,
                           departments=departments, title="Departments")

@admin.route(&apos;/departments/add&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def add_department():
    """
    Add a department to the database
    """
    check_admin()

    add_department = True

    form = DepartmentForm()
    if form.validate_on_submit():
        department = Department(name=form.name.data,
                                description=form.description.data)
        try:
            # add department to the database
            db.session.add(department)
            db.session.commit()
            flash(&apos;You have successfully added a new department.&apos;)
        except:
            # in case department name already exists
            flash(&apos;Error: department name already exists.&apos;)

        # redirect to departments page
        return redirect(url_for(&apos;admin.list_departments&apos;))

    # load department template
    return render_template(&apos;admin/departments/department.html&apos;, action="Add",
                           add_department=add_department, form=form,
                           title="Add Department")

@admin.route(&apos;/departments/edit/<int:id>&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def edit_department(id):
    """
    Edit a department
    """
    check_admin()

    add_department = False

    department = Department.query.get_or_404(id)
    form = DepartmentForm(obj=department)
    if form.validate_on_submit():
        department.name = form.name.data
        department.description = form.description.data
        db.session.commit()
        flash(&apos;You have successfully edited the department.&apos;)

        # redirect to the departments page
        return redirect(url_for(&apos;admin.list_departments&apos;))

    form.description.data = department.description
    form.name.data = department.name
    return render_template(&apos;admin/departments/department.html&apos;, action="Edit",
                           add_department=add_department, form=form,
                           department=department, title="Edit Department")

@admin.route(&apos;/departments/delete/<int:id>&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def delete_department(id):
    """
    Delete a department from the database
    """
    check_admin()

    department = Department.query.get_or_404(id)
    db.session.delete(department)
    db.session.commit()
    flash(&apos;You have successfully deleted the department.&apos;)

    # redirect to the departments page
    return redirect(url_for(&apos;admin.list_departments&apos;))

    return render_template(title="Delete Department")
```

We begin by creating a function,  `check_admin`, which throws a  `403 Forbidden`  error if a non-admin user attempts to access these views. We will call this function in every admin view.

The  `list_departments`  view queries the database for all departments and assigns them to the variable  `departments`, which we will use to list them in the template.

The  `add_department`  view creates a new department object using the form data, and adds it to the database. If the department name already exists, an error message is displayed. This view redirects to the  `list_departments`. This means that once the admin user creates a new department, they will be redirected to the Departments page.

The  `edit_department`  view takes one parameter:  `id`  . This is the department ID, and will be passed to the view in the template. The view queries the database for a department with the ID specified. If the department doesn't exist, a  `404 Not Found`  error is thrown. If it does, it is updated with the form data.

The  `delete_department`  view is similar to the  `edit_department`  one, in that it takes a department ID as a parameter and throws an error if the specified department doesn't exist. If it does, it is deleted from the database.

Note that we render the same template for adding and editing individual departments:  `department.html`. This is why we have the  `add_department`  variable in the  `add_department`  view (where it is set to  `True`), as well as in the  `edit_department`  view (where it is set to  `False`). We'll use this variable in the  `department.html`  template to determine what wording to use for the title and heading.

### Templates

Create an  `templates/admin`  directory, and in it, add a  `departments`  directory. Inside it, add the  `departments.html`  and  `department.html`  files:

```html
<!-- app/templates/admin/departments/departments.html -->

{% import "bootstrap/utils.html" as utils %}
{% extends "base.html" %}
{% block title %}Departments{% endblock %}
{% block body %}
<div class="content-section">
  <div class="outer">
    <div class="middle">
      <div class="inner">
        <br/>
        {{ utils.flashed_messages() }}
        <br/>
        <h1 style="text-align:center;">Departments</h1>
        {% if departments %}
          <hr class="intro-divider">
          <div class="center">
            <table class="table table-striped table-bordered">
              <thead>
                <tr>
                  <th width="15%"> Name </th>
                  <th width="40%"> Description </th>
                  <th width="15%"> Employee Count </th>
                  <th width="15%"> Edit </th>
                  <th width="15%"> Delete </th>
                </tr>
              </thead>
              <tbody>
              {% for department in departments %}
                <tr>
                  <td> {{ department.name }} </td>
                  <td> {{ department.description }} </td>
                  <td>
                    {% if department.employees %}
                      {{ department.employees.count() }}
                    {% else %}
                      0
                    {% endif %}
                  </td>
                  <td>
                    <a href="{{ url_for(&apos;admin.edit_department&apos;, id=department.id) }}">
                      <i class="fa fa-pencil"></i> Edit 
                    </a>
                  </td>
                  <td>
                    <a href="{{ url_for(&apos;admin.delete_department&apos;, id=department.id) }}">
                      <i class="fa fa-trash"></i> Delete 
                    </a>
                  </td>
                </tr>
              {% endfor %}
              </tbody>
            </table>
          </div>
          <div style="text-align: center">
        {% else %}
          <div style="text-align: center">
            <h3> No departments have been added. </h3>
            <hr class="intro-divider">
        {% endif %}
          <a href="{{ url_for(&apos;admin.add_department&apos;) }}" class="btn btn-default btn-lg">
            <i class="fa fa-plus"></i>
            Add Department
          </a>
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
```

We've created a table in the template above, where we will display all the departments with their name, description, and number of employees. Take note of the  `count()`  function, which we use in this case to get the number of employees. Each department listed will have an edit and delete link. Notice how we pass the  `department.id`  value to the  `edit_department`  and  `delete_department`  views in the respective links.

If there are no departments, the page will display “No departments have been added”. There is also a button which can be clicked to add a new department.

Now let's work on the template for adding and editing departments:

```html
<!-- app/templates/admin/departments/department.html -->

{% import "bootstrap/wtf.html" as wtf %}
{% extends "base.html" %}
{% block title %}
    {% if add_department %}
        Add Department
    {% else %}
        Edit Department
    {% endif %}
{% endblock %}
{% block body %}
<div class="content-section">
 <div class="outer">
    <div class="middle">
      <div class="inner">
        <div class="center">
            {% if add_department %}
                <h1>Add Department</h1>
            {% else %}
                <h1>Edit Department</h1>
            {% endif %}
            <br/>
            {{ wtf.quick_form(form) }}
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
```

Notice that we use the  `add_department`  variable which we initialized in the  `admin/views.py`  file, to determine whether the page title will be “Add Department” or “Edit Department”.

Add the following lines to your  `style.css`  file:

```css
/* app/static/css/style.css */

.outer {
    display: table;
    position: absolute;
    height: 70%;
    width: 100%;
}

.middle {
    display: table-cell;
    vertical-align: middle;
}

.inner {
    margin-left: auto;
    margin-right: auto;
}
```

The  `.middle`,  `.inner`, and  `.outer`  classes are to center the content in the middle of the page.

Lastly, let's put the correct link to the Departments page in the admin menu:

```html
<!-- app/templates/base.html -->

<!-- Modify nav bar menu -->
<li><a href="{{ url_for(&apos;admin.list_departments&apos;) }}">Departments</a></li>
```

Re-start the flask server, and then log back in as the admin user and click on the Departments link. Because we have not added any departments, loading the page will display:

Let's try adding a department:

It worked! We get the success message we configured in the  `add_department`  view, and can now see the department displayed.

Now let's edit it:

Notice that the current department name and description are already pre-loaded in the form. Also, take note of the URL, which has the ID of the department we are editing.

Editing the department is successful as well. Clicking the Delete link deletes the department and redirects to the Departments page, where a confirmation message is displayed:

### Roles

Now to work on the roles. This will be very similar to the departments code because the functionality for roles and departments is exactly the same.

### Forms

We'll start by creating the form to add and edit roles. Add the following code to the  `admin/forms.py`  file:

```py
# app/admin/forms.py

# existing code remains

class RoleForm(FlaskForm):
    """
    Form for admin to add or edit a role
    """
    name = StringField(&apos;Name&apos;, validators=[DataRequired()])
    description = StringField(&apos;Description&apos;, validators=[DataRequired()])
    submit = SubmitField(&apos;Submit&apos;)
```

### Views

Next we'll write the views to add, list, edit, and delete roles. Add the following code to the admin/views.py file:

```py
# app/admin/views.py

# update imports
from forms import DepartmentForm, RoleForm
from ..models import Department, Role

# existing code remains

# Role Views

@admin.route(&apos;/roles&apos;)
@login_required
def list_roles():
    check_admin()
    """
    List all roles
    """
    roles = Role.query.all()
    return render_template(&apos;admin/roles/roles.html&apos;,
                           roles=roles, title=&apos;Roles&apos;)

@admin.route(&apos;/roles/add&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def add_role():
    """
    Add a role to the database
    """
    check_admin()

    add_role = True

    form = RoleForm()
    if form.validate_on_submit():
        role = Role(name=form.name.data,
                    description=form.description.data)

        try:
            # add role to the database
            db.session.add(role)
            db.session.commit()
            flash(&apos;You have successfully added a new role.&apos;)
        except:
            # in case role name already exists
            flash(&apos;Error: role name already exists.&apos;)

        # redirect to the roles page
        return redirect(url_for(&apos;admin.list_roles&apos;))

    # load role template
    return render_template(&apos;admin/roles/role.html&apos;, add_role=add_role,
                           form=form, title=&apos;Add Role&apos;)

@admin.route(&apos;/roles/edit/<int:id>&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def edit_role(id):
    """
    Edit a role
    """
    check_admin()

    add_role = False

    role = Role.query.get_or_404(id)
    form = RoleForm(obj=role)
    if form.validate_on_submit():
        role.name = form.name.data
        role.description = form.description.data
        db.session.add(role)
        db.session.commit()
        flash(&apos;You have successfully edited the role.&apos;)

        # redirect to the roles page
        return redirect(url_for(&apos;admin.list_roles&apos;))

    form.description.data = role.description
    form.name.data = role.name
    return render_template(&apos;admin/roles/role.html&apos;, add_role=add_role,
                           form=form, title="Edit Role")

@admin.route(&apos;/roles/delete/<int:id>&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def delete_role(id):
    """
    Delete a role from the database
    """
    check_admin()

    role = Role.query.get_or_404(id)
    db.session.delete(role)
    db.session.commit()
    flash(&apos;You have successfully deleted the role.&apos;)

    # redirect to the roles page
    return redirect(url_for(&apos;admin.list_roles&apos;))

    return render_template(title="Delete Role")
```

These list, add, edit, and delete views are similar to the ones for departments that we created earlier.

### Templates

Create a  `roles`  directory in the  `templates/admin`  directory. In it, create the  `roles.html`  and  `role.html`  files:

```html
<!-- app/templates/admin/roles/roles.html -->

{% import "bootstrap/utils.html" as utils %}
{% extends "base.html" %}
{% block title %}Roles{% endblock %}
{% block body %}
<div class="content-section">
  <div class="outer">
    <div class="middle">
      <div class="inner">
        <br/>
        {{ utils.flashed_messages() }}
        <br/>
        <h1 style="text-align:center;">Roles</h1>
        {% if roles %}
          <hr class="intro-divider">
          <div class="center">
            <table class="table table-striped table-bordered">
              <thead>
                <tr>
                  <th width="15%"> Name </th>
                  <th width="40%"> Description </th>
                  <th width="15%"> Employee Count </th>
                  <th width="15%"> Edit </th>
                  <th width="15%"> Delete </th>
                </tr>
              </thead>
              <tbody>
              {% for role in roles %}
                <tr>
                  <td> {{ role.name }} </td>
                  <td> {{ role.description }} </td>
                  <td>
                    {% if role.employees %}
                      {{ role.employees.count() }}
                    {% else %}
                      0
                    {% endif %}
                  </td>
                  <td>
                    <a href="{{ url_for(&apos;admin.edit_role&apos;, id=role.id) }}">
                      <i class="fa fa-pencil"></i> Edit 
                    </a>
                  </td>
                  <td>
                    <a href="{{ url_for(&apos;admin.delete_role&apos;, id=role.id) }}">
                      <i class="fa fa-trash"></i> Delete 
                    </a>
                  </td>
                </tr>
              {% endfor %}
              </tbody>
            </table>
          </div>
          <div style="text-align: center">
        {% else %}
          <div style="text-align: center">
            <h3> No roles have been added. </h3>
            <hr class="intro-divider">
        {% endif %}
          <a href="{{ url_for(&apos;admin.add_role&apos;) }}" class="btn btn-default btn-lg">
            <i class="fa fa-plus"></i>
            Add Role
          </a>
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
```

Just like we did for the departments, we have created a table where we will display all the roles with their name, description, and number of employees. Each role listed will also have an edit and delete link. If there are no roles, a message of the same will be displayed. There is also a button which can be clicked to add a new role.

```html
<!-- app/templates/admin/roles/role.html -->

{% import "bootstrap/wtf.html" as wtf %}
{% extends "base.html" %}
{% block title %}
    {% if add_department %}
        Add Role
    {% else %}
        Edit Role
    {% endif %}
{% endblock %}
{% block body %}
<div class="content-section">
 <div class="outer">
    <div class="middle">
      <div class="inner">
        <div class="center">
            {% if add_role %}
                <h1>Add Role</h1>
            {% else %}
                <h1>Edit Role</h1>
            {% endif %}
            <br/>
            {{ wtf.quick_form(form) }}
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
```

We use the  `add_role`  variable above the same way we used the  `add_department`  variable for the  `department.html`  template.

Once again, let's update the admin menu with the correct link:

```html
<!-- app/templates/base.html -->

<!-- Modify nav bar menu -->
<li><a href="{{ url_for(&apos;admin.list_roles&apos;) }}">Roles</a></li>
```

Re-start the server. You should now be able to access the Roles page, and add, edit and delete roles.

### Employees

Now to work on listing employees, as well as assigning them departments and roles.

### Forms

We'll need a form to assign each employee a department and role. Add the following to the  `admin/forms.py`  file:

```py
# app/admin/forms.py

# update imports
from wtforms.ext.sqlalchemy.fields import QuerySelectField

from ..models import Department, Role

# existing code remains

class EmployeeAssignForm(FlaskForm):
    """
    Form for admin to assign departments and roles to employees
    """
    department = QuerySelectField(query_factory=lambda: Department.query.all(),
                                  get_label="name")
    role = QuerySelectField(query_factory=lambda: Role.query.all(),
                            get_label="name")
    submit = SubmitField(&apos;Submit&apos;)
```

We have imported a new field type,  `QuerySelectField`, which we use for both the department and role fields. This will query the database for all departments and roles. The admin user will select one department and one role using the form on the front-end.

### Views

Add the following code to the  `admin/views.py`  file:

```py
# app/admin/views.py

# update imports
from forms import DepartmentForm, EmployeeAssignForm, RoleForm
from ..models import Department, Employee, Role

# existing code remains

# Employee Views

@admin.route(&apos;/employees&apos;)
@login_required
def list_employees():
    """
    List all employees
    """
    check_admin()

    employees = Employee.query.all()
    return render_template(&apos;admin/employees/employees.html&apos;,
                           employees=employees, title=&apos;Employees&apos;)

@admin.route(&apos;/employees/assign/<int:id>&apos;, methods=[&apos;GET&apos;, &apos;POST&apos;])
@login_required
def assign_employee(id):
    """
    Assign a department and a role to an employee
    """
    check_admin()

    employee = Employee.query.get_or_404(id)

    # prevent admin from being assigned a department or role
    if employee.is_admin:
        abort(403)

    form = EmployeeAssignForm(obj=employee)
    if form.validate_on_submit():
        employee.department = form.department.data
        employee.role = form.role.data
        db.session.add(employee)
        db.session.commit()
        flash(&apos;You have successfully assigned a department and role.&apos;)

        # redirect to the roles page
        return redirect(url_for(&apos;admin.list_employees&apos;))

    return render_template(&apos;admin/employees/employee.html&apos;,
                           employee=employee, form=form,
                           title=&apos;Assign Employee&apos;)
```

The  `list_employees`  view queries the database for all employees and assigns them to the variable  `employees`, which we will use to list them in the template.

The  `assign_employee`  view takes an employee ID. First, it checks whether the employee is an admin user; if it is, a  `403 Forbidden`  error is thrown. If not, it updates the  `employee.department`  and  `employee.role`  with the selected data from the form, essentially assigning the employee a new department and role.

### Templates

Create a  `employees`  directory in the  `templates/admin`  directory. In it, create the  `employees.html`  and  `employee.html`  files:

```html
<!-- app/templates/admin/employees/employees.html -->

{% import "bootstrap/utils.html" as utils %}
{% extends "base.html" %}
{% block title %}Employees{% endblock %}
{% block body %}
<div class="content-section">
  <div class="outer">
    <div class="middle">
      <div class="inner">
        <br/>
        {{ utils.flashed_messages() }}
        <br/>
        <h1 style="text-align:center;">Employees</h1>
        {% if employees %}
          <hr class="intro-divider">
          <div class="center">
            <table class="table table-striped table-bordered">
              <thead>
                <tr>
                  <th width="15%"> Name </th>
                  <th width="30%"> Department </th>
                  <th width="30%"> Role </th>
                  <th width="15%"> Assign </th>
                </tr>
              </thead>
              <tbody>
              {% for employee in employees %}
                {% if employee.is_admin %}
                    <tr style="background-color: #aec251; color: white;">
                        <td> <i class="fa fa-key"></i> Admin </td>
                        <td> N/A </td>
                        <td> N/A </td>
                        <td> N/A </td>
                    </tr>
                {% else %}
                    <tr>
                      <td> {{ employee.first_name }} {{ employee.last_name }} </td>
                      <td>
                        {% if employee.department %}
                          {{ employee.department.name }}
                        {% else %}
                          -
                        {% endif %}
                      </td>
                      <td>
                        {% if employee.role %}
                          {{ employee.role.name }}
                        {% else %}
                          -
                        {% endif %}
                      </td>
                      <td>
                        <a href="{{ url_for(&apos;admin.assign_employee&apos;, id=employee.id) }}">
                          <i class="fa fa-user-plus"></i> Assign
                        </a>
                      </td>
                    </tr>
                {% endif %}
              {% endfor %}
              </tbody>
            </table>
          </div>
        {% endif %}
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
```

The  `employees.html`  template shows a table of all employees. The table shows their full name, department and role, or displays a  `-`  in case no department and role has been assigned. Each employee has an assign link, which the admin user can click to assign them a department and role.

Because the admin user is an employee as well, they will be displayed in the table. However, we have formatted the table such that admin users stand out with a green background and white text.

```html
<!-- app/templates/admin/employees/employee.html -->

{% import "bootstrap/wtf.html" as wtf %}
{% extends "base.html" %}
{% block title %}Assign Employee{% endblock %}
{% block body %}
<div class="content-section">
 <div class="outer">
    <div class="middle">
      <div class="inner">
        <div class="center">
            <h1> Assign Departments and Roles </h1>
            <br/>
            <p>
                Select a department and role to assign to
                <span style="color: #aec251;">
                    {{ employee.first_name }} {{ employee.last_name }}
                </span>
            </p>
            <br/>
            {{ wtf.quick_form(form) }}
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
```

We need to update the admin menu once more:

```html
<!-- app/templates/base.html -->

<!-- Modify nav bar menu -->
<li><a href="{{ url_for(&apos;admin.list_employees&apos;) }}">Employees</a></li>
```

Navigate to the Employees page now. If there are no users other than the admin, this is what you should see:

When there is an employee registered, this is displayed:

Feel free to add a variety of departments and roles so that you can start assigning them to employees.

You can re-assign departments and roles as well.

### Conclusion

We now have a completely functional CRUD web app! In Part Two of the tutorial, we've been able to create an admin user and an admin dashboard, as well as customise the menu for different types of users. We've also built out the core functionality of the app, and can now add, list, edit, and delete departments and roles, as well as assign them to employees. We have also taken security into consideration by protecting certain views from unauthorized access.

## Python Flask for Beginners: Build a CRUD Web App with Python and Flask - Part Three

This is the last part of a three-part tutorial to build an employee management web app, named Project Dream Team. In Part Two of the tutorial, we built out the CRUD functionality of the app.

We created forms, views, and templates to list, add, edit and delete departments and roles. By the end of Part Two, we could assign (and re-assign) departments and roles to employees.

In Part Three, we will cover:

1.  Custom error pages
2.  Unit tests
3.  Deployment on PythonAnywhere

### Custom Error Pages

Web applications make use of HTTP errors to let users know that something has gone wrong. Default error pages are usually quite plain, so we will create our own custom ones for the following common HTTP errors:

1.  Custom error pages
2.  Unit tests
3.  Deployment on PythonAnywhere

We'll start by writing the views for the custom error pages. In your  `app/__init__.py`  file, add the following code:

```py
# app/__init__.py

# update imports
from flask import Flask, render_template

# existing code remains

def create_app(config_name):

    # existing code remains

    @app.errorhandler(403)
    def forbidden(error):
        return render_template(&apos;errors/403.html&apos;, title=&apos;Forbidden&apos;), 403

    @app.errorhandler(404)
    def page_not_found(error):
        return render_template(&apos;errors/404.html&apos;, title=&apos;Page Not Found&apos;), 404

    @app.errorhandler(500)
    def internal_server_error(error):
        return render_template(&apos;errors/500.html&apos;, title=&apos;Server Error&apos;), 500

    return app


```

We make use of Flask's  `@app.errorhandler`  decorator to define the error page views, where we pass in the status code as a parameter.

Next, we'll create the template files. Create a  `app/templates/errors`  directory, and in it, create  `403.html`,  `404.html`, and  `500.html`.

```
<!-- app/templates/errors/403.html -->

{% extends "base.html" %}
{% block title %}Forbidden{% endblock %}
{% block body %}
<div class="content-section">
  <div class="outer">
    <div class="middle">
      <div class="inner">
        <div style="text-align: center">
            <h1> 403 Error </h1>
            <h3> You do not have sufficient permissions to access this page. </h3>
            <hr class="intro-divider">
            <a href="{{ url_for(&apos;home.homepage&apos;) }}" class="btn btn-default btn-lg">
                <i class="fa fa-home"></i>
                Home
            </a>
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
<!-- app/templates/errors/404.html -->

{% extends "base.html" %}
{% block title %}Page Not Found{% endblock %}
{% block body %}
<div class="content-section">
  <div class="outer">
    <div class="middle">
      <div class="inner">
        <div style="text-align: center">
            <h1> 404 Error </h1>
            <h3> The page you&apos;re looking for doesn&apos;t exist. </h3>
            <hr class="intro-divider">
            <a href="{{ url_for(&apos;home.homepage&apos;) }}" class="btn btn-default btn-lg">
                <i class="fa fa-home"></i>
                Home
            </a>
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}
<!-- app/templates/errors/500.html -->

{% extends "base.html" %}
{% block title %}Internal Server Error{% endblock %}
{% block body %}
<div class="content-section">
  <div class="outer">
    <div class="middle">
      <div class="inner">
        <div style="text-align: center">
            <h1> 500 Error </h1>
            <h3> The server encountered an internal error. That&apos;s all we know. </h3>
            <hr class="intro-divider">
            <a href="{{ url_for(&apos;home.homepage&apos;) }}" class="btn btn-default btn-lg">
                <i class="fa fa-home"></i>
                Home
            </a>
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock %}


```

All the templates give a brief description of the error, and a button that links to the homepage.

Run the app and log in as a non-admin user, then attempt to access  `<a href="http://127.0.0.1:5000/admin/departments" target="_blank">http://127.0.0.1:5000/admin/departments</a>`. You should get the following page:

Now attempt to access this non-existent page:  `<a href="http://127.0.0.1:5000/nothinghere" target="_blank">http://127.0.0.1:5000/nothinghere</a>`. You should see:

To view the internal server error page, we'll create a temporary route where we'll use Flask's  `abort()`  function to raise a 500 error. In the  `app/__init__.py`  file, add the following:

```
# app/__init__.py

# update imports
from flask import abort, Flask, render_template

# existing code remains

def create_app(config_name):
   # existing code remains

    @app.route(&apos;/500&apos;)
    def error():
        abort(500)

    return app


```

Go to  `<a href="http://127.0.0.1:5000/500" target="_blank">http://127.0.0.1:5000/500</a>`; you should see the following page:

Now you can remove the temporary route we just created for the internal server error.

### Tests

Now, let's write some tests for the app. The importance of testing software can't be overstated. Tests help ensure that your app is working as expected, without the need for you to manually test all of your app's functionality.

We’ll begin by creating a test database, and give the database user we created in  [Part One](https://on.morioh.net/b0a3f595aa?r=https://scotch.io/tutorials/build-a-crud-web-app-with-python-and-flask-part-one "Part One")  all privileges on it:

```
$ mysql -u root

mysql> CREATE DATABASE dreamteam_test;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON dreamteam_test . * TO &apos;dt_admin&apos;@&apos;localhost&apos;;
Query OK, 0 rows affected (0.00 sec)


```

Now we need to edit the  `config.py`  file to add configurations for testing. Delete the current contents and replace them with the following code:

```
# config.py

class Config(object):
    """
    Common configurations
    """

    DEBUG = True

class DevelopmentConfig(Config):
    """
    Development configurations
    """

    SQLALCHEMY_ECHO = True

class ProductionConfig(Config):
    """
    Production configurations
    """

    DEBUG = False

class TestingConfig(Config):
    """
    Testing configurations
    """

    TESTING = True

app_config = {
    &apos;development&apos;: DevelopmentConfig,
    &apos;production&apos;: ProductionConfig,
    &apos;testing&apos;: TestingConfig
}


```

We have put  `DEBUG = True`  in the base class,  `Config`, so that it is the default setting. We override this in the  `ProductionConfig`  class. In the  `TestingConfig`  class, we set the  `TESTING`  configuration variable to  `True`.

We will be writing unit tests. Unit tests are written to test small, individual, and fairly isolated units of code, such as functions. We will make use of  [Flask-Testing](https://on.morioh.net/b0a3f595aa?r=https://pythonhosted.org/Flask-Testing/ "Flask-Testing"), an extension that provides unit testing utilities for Flask.

```
$ pip install Flask-Testing


```

Next, create a  `tests.py`  file in the root directory of your app. In it, add the following code:

```
# tests.py

import unittest

from flask_testing import TestCase

from app import create_app, db
from app.models import Employee

class TestBase(TestCase):

    def create_app(self):

        # pass in test configurations
        config_name = &apos;testing&apos;
        app = create_app(config_name)
        app.config.update(
            SQLALCHEMY_DATABASE_URI=&apos;mysql://dt_admin:dt2016@localhost/dreamteam_test&apos;
        )
        return app

    def setUp(self):
        """
        Will be called before every test
        """

        db.create_all()

        # create test admin user
        admin = Employee(username="admin", password="admin2016", is_admin=True)

        # create test non-admin user
        employee = Employee(username="test_user", password="test2016")

        # save users to database
        db.session.add(admin)
        db.session.add(employee)
        db.session.commit()

    def tearDown(self):
        """
        Will be called after every test
        """

        db.session.remove()
        db.drop_all()

if __name__ == &apos;__main__&apos;:
    unittest.main()


```

In the base class above,  `TestBase`, we have a  `create_app`  method, where we pass in the configurations for testing.

We also have two other methods:  `setUp`  and  `tearDown`. The  `setUp`  method will be called automatically before every test we run. In it, we create two test users, one admin and one non-admin, and save them to the database. The  `tearDown`  method will be called automatically after every test. In it, we remove the database session and drop all database tables.

To run the tests, we will run the  `tests.py`  file:

```
$ python tests.py

----------------------------------------------------------------------
Ran 0 tests in 0.000s

OK


```

The output above lets us know that our test setup is OK. Now let's write some tests.

```

# tests.py

# update imports

import os

from flask import abort, url_for

from app.models import Department, Employee, Role

# add the following after the TestBase class

class TestModels(TestBase):

    def test_employee_model(self):
        """
        Test number of records in Employee table
        """
        self.assertEqual(Employee.query.count(), 2)

    def test_department_model(self):
        """
        Test number of records in Department table
        """

        # create test department
        department = Department(name="IT", description="The IT Department")

        # save department to database
        db.session.add(department)
        db.session.commit()

        self.assertEqual(Department.query.count(), 1)

    def test_role_model(self):
        """
        Test number of records in Role table
        """

        # create test role
        role = Role(name="CEO", description="Run the whole company")

        # save role to database
        db.session.add(role)
        db.session.commit()

        self.assertEqual(Role.query.count(), 1)

class TestViews(TestBase):

    def test_homepage_view(self):
        """
        Test that homepage is accessible without login
        """
        response = self.client.get(url_for(&apos;home.homepage&apos;))
        self.assertEqual(response.status_code, 200)

    def test_login_view(self):
        """
        Test that login page is accessible without login
        """
        response = self.client.get(url_for(&apos;auth.login&apos;))
        self.assertEqual(response.status_code, 200)

    def test_logout_view(self):
        """
        Test that logout link is inaccessible without login
        and redirects to login page then to logout
        """
        target_url = url_for(&apos;auth.logout&apos;)
        redirect_url = url_for(&apos;auth.login&apos;, next=target_url)
        response = self.client.get(target_url)
        self.assertEqual(response.status_code, 302)
        self.assertRedirects(response, redirect_url)

    def test_dashboard_view(self):
        """
        Test that dashboard is inaccessible without login
        and redirects to login page then to dashboard
        """
        target_url = url_for(&apos;home.dashboard&apos;)
        redirect_url = url_for(&apos;auth.login&apos;, next=target_url)
        response = self.client.get(target_url)
        self.assertEqual(response.status_code, 302)
        self.assertRedirects(response, redirect_url)

    def test_admin_dashboard_view(self):
        """
        Test that dashboard is inaccessible without login
        and redirects to login page then to dashboard
        """
        target_url = url_for(&apos;home.admin_dashboard&apos;)
        redirect_url = url_for(&apos;auth.login&apos;, next=target_url)
        response = self.client.get(target_url)
        self.assertEqual(response.status_code, 302)
        self.assertRedirects(response, redirect_url)

    def test_departments_view(self):
        """
        Test that departments page is inaccessible without login
        and redirects to login page then to departments page
        """
        target_url = url_for(&apos;admin.list_departments&apos;)
        redirect_url = url_for(&apos;auth.login&apos;, next=target_url)
        response = self.client.get(target_url)
        self.assertEqual(response.status_code, 302)
        self.assertRedirects(response, redirect_url)

    def test_roles_view(self):
        """
        Test that roles page is inaccessible without login
        and redirects to login page then to roles page
        """
        target_url = url_for(&apos;admin.list_roles&apos;)
        redirect_url = url_for(&apos;auth.login&apos;, next=target_url)
        response = self.client.get(target_url)
        self.assertEqual(response.status_code, 302)
        self.assertRedirects(response, redirect_url)

    def test_employees_view(self):
        """
        Test that employees page is inaccessible without login
        and redirects to login page then to employees page
        """
        target_url = url_for(&apos;admin.list_employees&apos;)
        redirect_url = url_for(&apos;auth.login&apos;, next=target_url)
        response = self.client.get(target_url)
        self.assertEqual(response.status_code, 302)
        self.assertRedirects(response, redirect_url)

class TestErrorPages(TestBase):

    def test_403_forbidden(self):
        # create route to abort the request with the 403 Error
        @self.app.route(&apos;/403&apos;)
        def forbidden_error():
            abort(403)

        response = self.client.get(&apos;/403&apos;)
        self.assertEqual(response.status_code, 403)
        self.assertTrue("403 Error" in response.data)

    def test_404_not_found(self):
        response = self.client.get(&apos;/nothinghere&apos;)
        self.assertEqual(response.status_code, 404)
        self.assertTrue("404 Error" in response.data)

    def test_500_internal_server_error(self):
        # create route to abort the request with the 500 Error
        @self.app.route(&apos;/500&apos;)
        def internal_server_error():
            abort(500)

        response = self.client.get(&apos;/500&apos;)
        self.assertEqual(response.status_code, 500)
        self.assertTrue("500 Error" in response.data)

if __name__ == &apos;__main__&apos;:
    unittest.main()


```

We've added three classes:  `TestModels`,  `TestViews`  and  `TestErrorPages`.

The first class has methods to test that each of the models in the app are working as expected. This is done by querying the database to check that the correct number of records exist in each table.

The second class has methods that test the views in the app to ensure the expected status code is returned. For non-restricted views, such as the homepage and the login page, the  `200 OK`  code should be returned; this means that everything is OK and the request has succeeded. For restricted views that require authenticated access, a  `302 Found`  code is returned. This means that the page is redirected to an existing resource, in this case, the login page. We test both that the  `302 Found`  code is returned and that the page redirects to the login page.

The third class has methods to ensure that the error pages we created earlier are shown when the respective error occurs.

Note that each test method begins with  `test`. This is deliberate, because  `unittest`, the Python unit testing framework, uses the  `test`  prefix to automatically identify test methods. Also note that we have not written tests for the front-end to ensure users can register and login, and to ensure administrators can create departments and roles and assign them to employees. This can be done using a tool like  [Selenium Webdriver](https://on.morioh.net/b0a3f595aa?r=http://www.seleniumhq.org/projects/webdriver/ "Selenium Webdriver"); however this is outside the scope of this tutorial.

Run the tests again:

```

$ python tests.py
..............
----------------------------------------------------------------------
Ran 14 tests in 2.313s

OK


```

Success! The tests are passing.

### Deploy!

Now for the final part of the tutorial: deployment. So far, we’ve been running the app locally. In this stage, we will publish the application on the internet so that other people can use it. We will use  [PythonAnywhere](https://on.morioh.net/b0a3f595aa?r=https://www.pythonanywhere.com/ "PythonAnywhere"), a Platform as a Service (PaaS) that is easy to set up, secure, and scalable, not to mention free for basic accounts!

### PythonAnywhere Set-Up

Create a free PythonAnywhere account  [here](https://on.morioh.net/b0a3f595aa?r=https://www.pythonanywhere.com/registration/register/beginner/ "here")  if you don’t already have one. Be sure to select your username carefully since the app will be accessible at  `your-username.pythonanywhere.com`.

Once you've signed up,  `your-username.pythonanywhere.com`  should show this page:

We will use git to upload the app to PythonAnywhere. If you’ve been pushing your code to cloud repository management systems like  [Bitbucket](https://on.morioh.net/b0a3f595aa?r=https://bitbucket.org/ "Bitbucket"),  [Gitlab](https://on.morioh.net/b0a3f595aa?r=https://about.gitlab.com/ "Gitlab")  or  [Github](https://on.morioh.net/b0a3f595aa?r=https://codequs.com/p/Hk3CYrFJG/github.com/ "Github"), that’s great! If not, now’s the time to do it. Remember that we won’t be pushing the  `instance`  directory, so be sure to include it in your  `.gitignore`  file, like so:

```
# .gitignore

*.pyc
instance/


```

Also, ensure that your  `requirements.txt`  file is up to date using the  `pip freeze`  command before pushing your code:

```
$ pip freeze > requirements.txt


```

Now, log in to your PythonAnywhere account. In your dashboard, there's a  `Consoles`  tab; use it to start a new Bash console.

In the PythonAnywhere Bash console, clone your repository.

```
$ git clone https://github.com/andela-mnzomo/project-dream-team-three


```

Next we will create a virtualenv, then install the dependencies from the  `requirements.txt`  file. Because PythonAnywhere installs  [virtualenvwrapper](https://on.morioh.net/b0a3f595aa?r=https://virtualenvwrapper.readthedocs.io/en/latest/ "virtualenvwrapper")  for all users by default, we can use its commands:

```
$ mkvirtualenv dream-team
$ cd project-dream-team-three
$ pip install -r requirements.txt


```

We've created a virtualenv called  `dream-team`. The virtualenv is automatically activated. We then entered the project directory and installed the dependencies.

Now, in the Web tab on your dashboard, create a new web app.

Select the Manual Configuration option (**not**  the Flask option), and choose Python 2.7 as your Python version. Once the web app is created, its configurations will be loaded. Scroll down to the Virtualenv section, and enter the name of the virtualenv you just created:

### Database Configuration

Next, we will set up the MySQL production database. In the Databases tab of your PythonAnywhere dashboard, set a new password and then initialize a MySQL server:

The password above will be your database user password. Next, create a new database if you wish. PythonAnywhere already has a default database which you can use.

By default, the database user is your username, and has all privileges granted on any databases created. Now, we need to migrate the database and populate it with the tables. In a Bash console on PythonAnywhere, we will run the  `flask db upgrade`  command, since we already have the migrations directory that we created locally. Before running the commands, ensure you are in your virtualenv as well as in the project directory.

```
$ export FLASK_CONFIG=production
$ export FLASK_APP=run.py
$ export SQLALCHEMY_DATABASE_URI=&apos;mysql://your-username:your-password@your-host-address/your-database-name&apos;
$ flask db upgrade


```

When setting the  `SQLALCHEMY_DATABASE_URI`  environment variable, remember to replace  `your-username`,  `your-password`,  `your-host-address`  and  `your-database-name`  with their correct values. The username, host address and database name can be found in the MySQL settings in the Databases tab on your dashboard. For example, using the information below, my database URI is:  `mysql://projectdreamteam:password@projectdreamteam.mysql.pythonanywhere-services.com/projectdreamteam$dreamteam_db`

### WSGI File

Now we will edit the WSGI file, which PythonAnywhere uses to serve the app. Remember that we are not pushing the  `instance`  directory to version control. We therefore need to configure the environment variables for production, which we will do in the WSGI file.

In the Code section of the Web tab on your dashboard, click on the link to the WSGI configuration file.

Delete all the current contents of the file, and replace them with the following:

```
import os
import sys

path = &apos;/home/your-username/your-project-directory-name&apos;
if path not in sys.path:
    sys.path.append(path)

os.environ[&apos;FLASK_CONFIG&apos;] = &apos;production&apos;
os.environ[&apos;SECRET_KEY&apos;] = &apos;p9Bv<3Eid9%$i01&apos;
os.environ[&apos;SQLALCHEMY_DATABASE_URI&apos;] = &apos;mysql://your-username:your-password@your-host-address/your-database-name&apos;

from run import app as application


```

In the file above, we tell PythonAnywhere to get the variable  `app`  from the  `run.py`  file, and serve it as the application. We also set the  `FLASK_CONFIG`,  `SECRET_KEY`  and  `SQLALCHEMY_DATABASE_URI`  environment variables. Feel free to alter the secret key. Note that the  `path`  variable should contain your username and project directory name, so be sure to replace it with the correct values. The same applies for the database URI environment variable.

We also need to edit our local  `app/__init__py`  file to prevent it from loading the  `instance/config.py`  file in production, as well as to load the configuration variables we've set:

```
# app/__init__.py

# update imports

import os

# existing code remains

def create_app(config_name):
    if os.getenv(&apos;FLASK_CONFIG&apos;) == "production":
        app = Flask(__name__)
        app.config.update(
            SECRET_KEY=os.getenv(&apos;SECRET_KEY&apos;),
            SQLALCHEMY_DATABASE_URI=os.getenv(&apos;SQLALCHEMY_DATABASE_URI&apos;)
        )
    else:
        app = Flask(__name__, instance_relative_config=True)
        app.config.from_object(app_config[config_name])
        app.config.from_pyfile(&apos;config.py&apos;)

    # existing code remains


```

Push your changes to version control, and pull them on the PythonAnywhere Bash console:

```
$ git pull origin master


```

Now let's try loading the app on PythonAnywhere. First, we need to reload the app on the Web tab in the dashboard:

Now go to your app URL:

Great, it works! Try registering a new user and logging in. This should work just as it did locally.

### Admin User

We will now create an admin user the same way we did locally. Open the Bash console, and run the following commands:

```
$ flask shell
>>> from app.models import Employee
>>> from app import db
>>> admin = Employee(email="admin@admin.com",username="admin",password="admin2016",is_admin=True)
>>> db.session.add(admin)
>>> db.session.commit()


```

Now you can login as an admin user and add departments and roles, and assign them to employees.

### Conclusion

Congratulations on successfully deploying your first Flask CRUD web app! From setting up a MySQL database, to creating models, blueprints (with forms and views), templates, custom error pages, tests, and finally deploying the app on PythonAnywhere, you now have a strong foundation in web development with Flask. I hope this has been as fun and educational for you as it has for me! I'm looking forward to hearing about your experiences in the comments below.

> [Source : ](https://morioh.com/p/b59f7df2e1f5).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyODg4Njg4NF19
-->