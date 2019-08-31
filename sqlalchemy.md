# SQLAlchemy

<img src="https://www.sqlalchemy.org/img/sqla_logo.png" width=128px>
## Creating an engine

Creates an object that to represent the database we are trying to connect to.

```python
from sqlalchemy import create_engine


engine = create_engine('sqlite:///:memory:', echo=True)
```

## Running an ad hoc query

```python
engine = create_engine('sqlite:///:memory:', echo=True)

result = engine.execute([YOUR_QUERY_IN_SQL])

for row in results:
    ...
results.close()
```

## Connections

Create a persistent connection to the database

```python
engine = create_engine('sqlite:///:memory:')
connection = engine.connect()
result = connection.execute([YOUR_QUERY_IN_SQL])
for row in result:
    ...
connection.close()
```

## Sessions

Create a persistent connection that allows adding, removing and undo.

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker


engine=create_engine('sqlite:///:memory:', echo=True)
Session = sessionmake(bind-engine)
session = Session()
```

## Creating Models

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
