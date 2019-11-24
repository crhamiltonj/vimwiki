# SQLAlchemy - Bare

## Connecting

```python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///:memory:', echo=True)
```

## Declaring a Mapping

### Establishing the Base class

All ORM objects are derived from this class

```python
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()
```

### Defining the Class

```python
from sqlalchemy import Column, Integer, String


class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=true)
    name = Column(String)
    fullname = Column(String)
    nickname = Column(String)

    def __repr__(self):
        return f"<User {self.name}, {self.fullname}, {self.nickname}>"
```

## Creating a Session

```python
from sqlalchemy.orm import sessionmaker
Session = sessionmaker(bind=engine)
```

If you don't have an engine to connect to:

```python
Session = sessionmaker()

Session.configure(bind=engine)
```

### Full Example of db module

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import scoped_session, sessionmaker
from sqlalchemy.ext.declarative import declarative_base


engine = create_engine("sqlite:///:memory:", echo=False)
db_session = scoped_session(
    sessionmaker(autocommit=False, autoflush=False, bind=engine)
)


Base = declarative_base()
Base.query = db.session.query_property()


def init_db():
    from app.models import User

    Base.metadata.create_all(bind=engine)
```

### Full Example of a model module

```python
from sqlalchemy import Column, Integer, String, Boolean, DateTime
from db import Base

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String, unique=True)
    email = Column(String, unique=True)
    hashed_password = Column(String, nullable=True)

    def __init__(self, name=None, email=None):
        self.name = name
        self.email = email

    def __repr__(self):
        return f'<User {self.name}>'
```

## Basic CRUD Functions

### Adding and Updating

```python
ed_user = User(name='ed', fullname='Ed Jones', nickname='edsnickname')
session.add(ed_user)
session.commit()
```

### Rolling Back

```python
session.rollback()
```

### Querying

Queries are called on __sessions__.

```python
for instance in session.query(User).order_by(User.id):
    print(instance.name, instance.fullname)
```

#### Filters

| SQL | SQLAlchemy |
|-----|----|
| **equals**| session.query.filter(_Object.fieldname_ == _value_)|
| **not equals** | session.query.filter(_Object.fieldname_ != _value_) |
| **LIKE** | session.query.filter(_Object.fieldname_.like(_value_)) |
| **ILIKE** | session.query.filter(_Object.fieldname_.ilike(_value_)) |
| **IN** | session.query.filter(_Object.fieldname_.in\_([list,of,values])) |
| **NOT IN** | session.query.filter(*~Object.fieldname*.in_([list,of,values])) |
| **IS NULL** | session.query.filter(*Object.fieldname* == None) <br> session.query.filter(_Object.fieldname_.is\_(None)) |
| **IS NOT NULL** | session.query.filter(_Object.fieldname_ != None)<br>session.query.filter(_Object.fieldname_.isnot(None)) |
| **AND** | session.query.filter(_and(*first filter*, *second filter*))<br>session.query.filter(*first term*, *second term*)<br>session.query.filter(*first term*).filter(*second term*)|
| **OR** | session.query.filter(or\_(_Object.fieldname1_, _Object.fieldname2_))|
| **MATCH** | session.query.filter(_Object.fieldname_.match(*value*))|

#### Returning Lists and Scalars

| Query Type | Description|
|---|---|
| **all()** | returns a list |
| **first()** | applies a limit of one and returns the first result as a scalar|
| **one()**| fetches all rows and returns an error if not exactly one row is found|
|**one\_or\_none()**| fetches all rows and returns an error if more than one row is found.<br>  If none found returns none.<br> If one found returns  result as scalar.|
|**scalar()**| invokes the one() method and on success returns the first column of the row found|

#### Textual SQL

Literal strings can be passed to the `text()` method for filter and order_by arguments.

```python
from sqlalchemy import text
for user in session.query(User).filter(text("id<224")).order_by(text("id")).all():
    print(user.name)
```

#### Counting

Returns the number of rows returned from a query

```python
session.query(User).filter(User.name.like('%ed')).count()
```

## Relationships
