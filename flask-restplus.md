# Flask RestPlus

## With Blueprints

- In the routes file

```python
from flask import Blueprint
from flask_restplus import Api, Resource


blueprint = Blueprint('api', __name__)
api = Api(blueprint)

@api.route('/ping')
class PingResource(Resource)
    def get(self):
        return {'message', 'pong'}
```

- In the application factory

```python
from flask import Flask


def create_app():
    app = Flask(__name__)

    from apis import blueprint as api

    app.register_blueprint(api, url_prefix='/api/1')

    return app
```
