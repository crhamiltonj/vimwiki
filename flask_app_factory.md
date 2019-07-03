# Application Factory

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

    # a simple page that says hello
    @app.route('/hello')
    def hello():
        return 'Hello World!'

    return app
```

* `create_app` does the following:
  1. `app = Flask(__name__, instance_relative_config=True)` -- creates a Flask instance
      * `__name__` is the name of the current module and is used to set up paths
      * `instance_relative_config=True` tells the app that the configuration files are relative to the instance folder. The instance folder is outside of the main app package and should not be commited to version control.
  2. `app.config.from_mapping()` -- sets the default configuration the app will use:
      * `SECRET_KEY` is used by flask to keep data safe.  It is set to `dev` during development but should be overriden with a random value when deploying.
      * `DATABASE` is the path where the local database filewill be saved.
  3. `app.config.from_pyfile()` -- overrides the default configuration with values from the config.py in the instance folder
      * `test_config` can be passed to the factory instead of the default configuration so test can be configured independantly of any developement values.
  4. `os.makedirs()` ensures the `app.instance_path` exists.
  5. `@app.route()` creates a simple route to see the application working

## To Run

Set the follwing environment variables and execure `flask run` from the root folder

```bash
export FLASK_APP=flaskr # the module where the __init__.py is stored
export FLASK_ENV=development # turn on debug mode and restart
flask run # flask run will import the module thereby executing the code in create_app
```

