# Flask Design Patterns

<img src="https://www.vectorlogo.zone/logos/pocoo_flask/pocoo_flask-official.svg" >

## Basic One File Flask App

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello World'


if __name__ == '__main__':
    app.run()
```

## Application Factory

```python
# flaskr/__init__.py
import os

from flask import Flask


def create_app(test_config=None):
    # create and configure the app
    app = Flask(__name__, instance_relative_config=True)
    app.config.from_mapping(
        SECRET_KEY='dev',
        DATABASE=os.path.join(app.instance_path, 'flaskr.sqlite')
    )

    if test_config is None:
        # load the instance config, if it exists, when not testing
        app.config.from_pyfile('config.py', silent=True)
    else:
        # load the test_config if passed in
        app.config.from_mapping(test_config)

    # ensure the instance folder exists
    try:
        os.makedirs(app.instance_path)
    except OSError:
        pass

    from . import db
    db.init_app(app)

    from . import auth
    app.register_blueprint(auth.bp)

    return app

    # a simple page that says hello
    @app.route('/hello')
    def hello():
        return 'Hello World!'
```

- `create_app` does the following:
  1. `app = Flask(__name__, instance_relative_config=True)` -- creates a Flask instance
     - `__name__` is the name of the current module and is used to set up paths
     - `instance_relative_config=True` tells the app that the configuration files are relative to the instance folder. The instance folder is outside of the main app package and should not be commited to version control.
  2. `app.config.from_mapping()` -- sets the default configuration the app will use:
     - `SECRET_KEY` is used by flask to keep data safe. It is set to `dev` during development but should be overriden with a random value when deploying.
     - `DATABASE` is the path where the local database filewill be saved.
  3. `app.config.from_pyfile()` -- overrides the default configuration with values from the config.py in the instance folder
     - `test_config` can be passed to the factory instead of the default configuration so test can be configured independantly of any developement values.
  4. `os.makedirs()` ensures the `app.instance_path` exists.
  5. `@app.route()` creates a simple route to see the application working
  6. `db.init_app()` registers the database with the app returned from the app factory
  7. `app.register_blueprint(auth.bp)` registers the blueprint `bp` in the auth module to the app returned by `create_app`.

### To Run

Set the follwing environment variables and execure `flask run` from the root folder

```bash
export FLASK_APP=flaskr # the module where the __init__.py is stored
export FLASK_ENV=development # turn on debug mode and restart
flask run # flask run will import the module thereby executing the code in create_app
```

## Connect to Database

### Non SQLAlchemy Version

```python
# flaskr/db.py

import sqlite3

import click
from flask import current_app, g
from flask.cli import with_appcontext


def get_db():
    if 'db' not in g:
        g.db = sqlite3.connect(
            current_app.config['DATABASE'],
            detect_types=sqlite3.PARSE_DECLTYPES
        )
        g.db.row_factory = sqlite3.Row

    return g.db


def close_db(e=None):
    db = g.pop('db', None)

    if db is not None:
        db.close()


def init_db():
    db = get_db()

    with current_app.open_resource('schema.sql') as f:
        db.executescript(f.read().decode('utf-8'))


@click.command('init-db')
@with_appcontext
def init_db_command():
    """Clear the existing data and create new tables"""
    init_db()
    click.echo('Initialized the database.')

@click.command('init-db')
@with_appcontext
def init_db_command():
    """Clear the existing data and create new tables"""
    init_db()
    click.echo('Initialized the database.')

def init_app(app):
    app.teardown_appcontext(close_db)
    app.cli.add_comment(init_db_command)
```

- `get_db()` checks the global context and creates a database connection if it doesn't already exist.
  - `g` is a special object that is unique to each request. It is used to store data that might be accessed by multiple functions during a request. The connection is stored and reused instead of creating a new connection if get_db is called a second time in the same request.
  - `current_app` is another special object that points to the Flask application handling the request. WHen using the application factory pattern, there is no application object when writinf the rest of the code. `get_db` will be called when the application has been created nad is handling a request, so `current_app` should be used
  - `sqlite3.connect()` establishes a coneection to the file pointed at by the `DATABASE configuration key.
  - `sqlite3.Row` telles the connection to return rows that behave like dicts. This allows accessing the columns by name.
- `close_db()` check if a connection was created by checking if `g.db` was set. If the connection exists it is closed.
- `init_db` gets a handle to a database connection using `get_db()` and executes a SQL query that initializes the database.
  - `open_resource()` opens a file relative to the application's package
  - `click.command()` defines a command called init-db that calls the init_db function and show a success message to the user.
- `init_app()` is a callback function that initializes the database and set up a further callback to close the connection when the request completes

  - `app.teardown_appcontext` registers the `close_db` function for cleanup
  - `app.cli.add_command` adds a new command that can be called with the flask command

## Blueprints and Views

auth.py

```python
import functools
from flask import (
  Blueprint, flash, g redirect, render_template, request, session, url_for
)
from werkzeug.security import check_password_hash, generate_password_hash

from flaskr.db import get_db

bp=Blueprint('auth', __name__, url_prefix='/auth')

@bp.route('/register', methods=('GET', 'POST'))
def register():
  if request.method == 'POST':
    username = request.form['username']
    password = request.form['password']
    db = get_db()
    error = None

    if not username:
      error = "Username is required"
    elif not password:
      error = 'Password is required'
    elif db.execute ('SELECT id FROM user where USERNAME = ?', (username,)).fetchone() is not None:
      error = 'User {} is already registered.'.format(username)

    if error is None:
      db.execute(
        'INSERT INTO user (username, password) VALUES (?, ?)',
        (username, generate_password_hash(password))
      )
      db.commit()
      return redirect(url_for('auth_login'))

    flash(error)
  return render_template('auth/register.html')
```

Creates a blueprint named `auth`.

- `__name__` is passed in a an argument so other parts of the blueprint can know where it is defined.
- `url_prefix` is prepended to all URL associated with the blueprint.

## Tips and Tricks

When creating a blueprint that replaces the root path, the static folder won't be found automatically.  You have to set a static_url path that will point to the correct folder.

https://stackoverflow.com/questions/22152840/flask-blueprint-static-directory-does-not-work

## Databases and ORMs

- [SQLAlchemy Bare](./sqlalchemy-bare.md)
- [Flask-SQLAlchemy](./flask-sqlalchemy.md)
- [Flask-Migrate](./flask-migrate.md)

## Flask REST APIs

- [flask-restful](flask-restful.md)
- [flask-restplus](flask-restplus.md)
- [flask-marshmallow](flask-marshmallow.md)

[Back to Index](index.md)
