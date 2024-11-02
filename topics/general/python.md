
- [Python Abstract Classes](https://medium.com/analytics-vidhya/abc-in-python-abstract-base-class-35808a9d6b32)
- [Pydantic]()
  
### What are decorators in Python?

 decorator is a function that takes another function as an argument and extends or modifies its behavior without changing its source code. Decorators are often used to add functionality such as logging, authentication, or memoization to functions or methods.

Differentiate between map(), filter(), and reduce() functions in terms of their purposes and use cases.


### What is the Global Interpreter Lock (GIL) in Python, and how does it impact multithreading?

Global Interpreter Lock (GIL) in Python is a mutex that allows only one thread to execute Python bytecode at a time, even on multi-core processors. This means that in a multi-threaded Python program, only one thread is actively executing Python code at any given moment, while others are waiting for their turn.


### What is yield?



Modules, in general, are simply Python files with a .py extension and can have a set of functions, classes, or variables defined and implemented. They can be imported and initialized once using the import statement. If partial functionality is needed, import the requisite classes or functions using from foo import bar.

Packages allow for hierarchial structuring of the module namespace using dot notation. As, modules help avoid clashes between global variable names, in a similar manner, packages help avoid clashes between module names.
Creating a package is easy since it makes use of the system's inherent file structure. So just stuff the modules into a folder and there you have it, the folder name as the package name. Importing a module or its contents from this package requires the package name as prefix to the module name joined by a dot.


### What are global, protected and private attributes in Python?

    Global variables are public variables that are defined in the global scope. To use the variable in the global scope inside a function, we use the global keyword.
    Protected attributes are attributes defined with an underscore prefixed to their identifier eg. _sara. They can still be accessed and modified from outside the class they are defined in but a responsible developer should refrain from doing so.
    Private attributes are attributes with double underscore prefixed to their identifier eg. __ansh. They cannot be accessed or modified from the outside directly and will result in an AttributeError if such an attempt is made.


### What is the use of self in Python?

Self is used to represent the instance of the class. With this keyword, you can access the attributes and methods of the class in python. It binds the attributes with the given arguments. self is used in different places and often thought to be a keyword. But unlike in C++, self is not a keyword in Python.

What are decorators in Python?

Decorators in Python are essentially functions that add functionality to an existing function in Python without changing the structure of the function itself.

### Pickling:

    Pickling is the name of the serialization process in Python. Any object in Python can be serialized into a byte stream and dumped as a file in the memory. 


### What are Exception Groups in Python?

The latest feature of Python 3.11, Exception Groups. The ExceptionGroup can be handled using a new except* syntax. The * symbol indicates that multiple exceptions can be handled by each except* clause.


### What are some important classes provided by SQLAlchemy to map tables from a database?

The most important classes provided by SQLAlchemy to map tables from a database are the Table, MetaData, and Column classes. The Table class represents a table in a database, the MetaData class represents the schema for a database, and the Column class represents a column in a database table.

Is it possible to convert a list of objects into a dictionary using SQLAlchemy? If yes, then how?

Yes, it is possible to convert a list of objects into a dictionary using SQLAlchemy. This can be done using the `as_dict` function.

What’s the difference between session.commit() and session.flush()?

The main difference between session.commit() and session.flush() is that session.commit() will also commit any changes to the database, whereas session.flush() will only flush the changes to the database.


### difference between a SQLAlchemy Core and SQLAlchemy ORM?

SQLAlchemy Core and ORM are two distinct layers of SQLAlchemy, a SQL toolkit for Python.

The Core is a low-level SQL abstraction layer focused on database schema and SQL expressions. It provides a direct interaction with the database using SQL commands and does not hide the underlying SQL nature of a relational database.

On the other hand, SQLAlchemy ORM (Object Relational Mapper) is a high-level API that allows interaction with databases using Python classes. It abstracts the underlying SQL commands, enabling developers to work with objects rather than tables and SQL queries. This makes it easier to write Pythonic code and reduces the need for repetitive SQL syntax.


### How does SQLAlchemy handle SQL injections and what methods does it use to prevent it?

SQLAlchemy prevents SQL injections primarily through the use of bind parameters. This method ensures that data sent to the database is not directly included in the query string, but instead kept separate and then combined by the DBMS.

### How can you implement one-to-one and one-to-many relationships in SQLAlchemy?

In SQLAlchemy, one-to-one and one-to-many relationships are implemented using the relationship() function. 

lass Parent(Base):
__tablename__ = ‘parent’
id = Column(Integer, primary_key=True)
child = relationship(“Child”, uselist=False, back_populates=”parent”)

class Child(Base):
__tablename__ = ‘child’
id = Column(Integer, primary_key=True)
parent_id = Column(Integer, ForeignKey(‘parent.id’))
parent = relationship(“Parent”, back_populates=”child”)

### What are some advantages of using FastAPI over Flask?

FastAPI is built on top of Starlette, which is a lightweight ASGI framework. This makes it ideal for building high-performance web applications. Additionally, FastAPI comes with built-in support for data validation, authentication, and documentation.

### What is uvicorn? Why should it be used with FastAPI?

Uvicorn is a web server that is specifically designed for use with the FastAPI web framework. 


 Explain the caching strategies of Django. ?

Django has its own inbuilt caching system that allows us to store our dynamic pages. So that we don’t have to request them again when we need them. The advantage of the Django Cache framework is that it allows us to cache data such as templates or the entire site. Django provides four different types of caching options, they are:

    per-site cache – It is the most straightforward to set up and caches your entire website.
    per-view cache – Individual views can be cached using the per-view cache.
    Template fragment caching allows you to cache only a portion of a template.
    low-level cache API – It can manually set, retrieve, and maintain particular objects in the cache using the low-level cache API.

Explain the role of Django middleware and provide some examples

Django middleware is a series of hooks that process requests and responses globally before they reach the view or after they leave the view. Middleware can be used for various purposes, such as authentication, session management, and caching. Some examples of Django middleware include:

    AuthenticationMiddleware: Handles user authentication and associates users with requests.
    SessionMiddleware: Manages sessions for users.
    CsrfViewMiddleware: Protects against cross-site request forgery attacks.
    

https://towardsdatascience.com/build-an-async-python-service-with-fastapi-sqlalchemy-196d8792fa08

## Pydantic

TODO
