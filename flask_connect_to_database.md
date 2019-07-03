# Connect to Database

## Non SQLAlchemy Version

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

```

* `get_db()` checks the global context and creates a database connection if it doesn't already exist.
  * `g` is a special object that is unique to each request. It is used to store data that might be accessed by multiple functions during a request. The connection is stored and reused instead of creating a new connection if get_db is called a second time in the same request.
  * `current_app` is another special object that points to the Flask application handling the request. WHen using the application factory pattern, there is no application object when writinf the rest of the code. `get_db` will be called when the application has been created nad is handling a request, so `current_app` should be used
  * `sqlite3.connect()` establishes a coneection to the file pointed at by the `DATABASE configuration key.
  * `sqlite3.Row` telles the connection to return rows that behave like dicts.  This allows accessing the columns by name.
* `close_db()` check  if a connection was created by checking if `g.db` was set. If the connection exists it is closed.
* `init_db` gets a handle to a database connection using `get_db()` and executes a SQL query that initializes the database.
  * `open_resource()` opens a file relative to the application's package
  * `click.command()` defines a command called init-db that calls the init_db function and show a success message to the user.
  