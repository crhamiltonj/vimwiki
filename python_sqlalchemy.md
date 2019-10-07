# SQLAlchemy

<img src="https://www.sqlalchemy.org/img/sqla_logo.png" width=128px>

## SQLAlchemy Core

SQLAlchemy Core is use for lower level access to the database.

### Connection

```python
from sqlalchemy import create_engine
engine = create_engine('sqlite:///:memory:', echo=True)
```

### Define and Create Tables

```python
from sqlalchemy import Table, Column, Integer, String, MetaData, ForeignKey
metadata = MetaData()

users = Table('users', metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String),
    Column('fullname', String)
)

addresses = Table('addresses', metadata
    Column('id', Integer, primary_key=True),
    Column('user_id', None, ForeignKey('users.id')),
    Column('email_address', String, nullable=False)
)

metadata.create_all(engine)
```

### Inserting Data

```python
ins = users.insert().values(name='jack', fullname='Jack Jones')
```

### Executing Queries

```python
conn = engine.connect()
result = conn.execute(ins)
```

### Executing Multiple Statements

```python
conn.execute(addresses.insert(), [
...    {'user_id': 1, 'email_address' : 'jack@yahoo.com'},
...    {'user_id': 1, 'email_address' : 'jack@msn.com'},
...    {'user_id': 2, 'email_address' : 'www@www.org'},
...    {'user_id': 2, 'email_address' : 'wendy@aol.com'},
... ])
```

### Selecting

```python
from sqlalchemy.sql import select
s = select([users])
result = conn.execute(s)
```

## SQLAlchemy with ORM

### Creating an engine

Creates an object that to represent the database we are trying to connect to.

```python
from sqlalchemy import create_engine


engine = create_engine('sqlite:///:memory:', echo=True)
```

### Running an ad hoc query

```python
engine = create_engine('sqlite:///:memory:', echo=True)

result = engine.execute([YOUR_QUERY_IN_SQL])

for row in results:
    ...
results.close()
```

### Connections

Create a persistent connection to the database

```python
engine = create_engine('sqlite:///:memory:')
connection = engine.connect()
result = connection.execute([YOUR_QUERY_IN_SQL])
for row in result:
    ...
connection.close()
```

### Sessions

Create a persistent connection that allows adding, removing and undo.

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker


engine=create_engine('sqlite:///:memory:', echo=True)
Session = sessionmake(bind-engine)
session = Session()
```

### Creating Models

Models are python classes that represent records in the database. To create a database extend the declaritive_base object from sqlalchemy.ext.declaritive.

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declaritive import declaritive_base

Base = declaritive_base()

class SomeClass(Base):
    __tablename__ = 'some_table'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
```

### Full Example

```python
from sqlalchemy import create_engine
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker


engine = create_engine('sqlite:///:memory:', echo=False)
Base = declarative_base()
Session = sessionmaker(bind = engine)
session = Session()

class Entries(Base):
    __tablename__ = 'entries'

    id = Column(Integer, primary_key = True)
    body = Column(String)

Base.metadata.create_all(engine)

def add_entry(body):
    entry = Entries(body=body)
    session.add(entry)
    session.commit()

def get_entry(_id):
    result = None
    result = session.query(Entries).get(_id)
    if result:
        return result.body
    else:
        return 'Not found'

def delete_entry(_id):
    result = session.query(Entries).get(_id)
    if result:
        session.delete(result)
        session.commit()

    return 'Not found'

def update_entry(_id, new_body):
    result = session.query(Entries).get(_id)
    result.body = new_body
    session.commit()

def get_entry_list():
    results = session.query(Entries).all()
    return results

if __name__ == '__main__':
    add_entry('This is a test')
    print(get_entry(1))
    update_entry(1,'This is a update')
    print(get_entry(1))
    print('Deleting entry...')
    delete_entry(1)
    print(get_entry(1))
    print('List all records: ')
    print(get_entry_list())
```

## Flask-SQLAlchemy

### Installing

`pip install flask-sqlalchemy`

### Minimal Application

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:////tmp/test.db'
db = SQLAlchemy(app)


class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

    def __repr__(self):
        return '<User %r>' % self.username
```

[Back to Python](python.md)
[Back to Index](index.md)
