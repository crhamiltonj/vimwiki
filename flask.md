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

- [Application Factory](./flask_app_factory.md)
- [Connect to Database](./flask_connect_to_database.md)
- [Blueprints and Views](./flask_blueprints_and_views.md)
- [Databases and ORMs](./flask-databases-and-orms.md)
- [REST APIs](./flask-rest.md)

[Back to Index](index.md)
