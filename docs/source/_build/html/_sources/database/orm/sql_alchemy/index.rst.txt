***********
SQL Alchemy
***********

The function of a ORM(object relational mapper) is associating user defined python  classes with database tables.
And the SQL Alchemy is doing the exact same thing here.

So here a instance of  python classes (objects) represent rows in their corresponding tables. 

SQL Alchemy ORM, is build on top of the Expression Language.which is the general way to interact with the DB in SQL Alchemy.


Fundamentals
############

*  A collection of Table objects and their associated child objects is referred to as **database metadata**

Connecting to DB
################

To create connection ,we need to create a instance of Alchemy Engine class and it represents the core interface to the database, adapted through a **dialect** (consider it as a db driver) that handles the details of the database and DBAPI in use.


.. code-block:: python

    from sqlalchemy import create_engine
    engine = create_engine('postgresql://nithinmk:@localhost/alembic_trial', echo=True)


The Engine establishes the DBAPI connection when we call method  like **Engine.execute()** or **Engine.connect()**
When using the ORM, we typically don’t use the Engine directly once created; instead, it’s used behind the scenes by the ORM.

Declare a Mapping
#################

When using the ORM, the configurational process starts by describing the database tables we’ll be dealing with, and then by defining our own classes which will be mapped to those tables. 
In modern SQLAlchemy, these two tasks are usually performed together, using a system known as **Declarative** , which allows us to create classes that include directives to describe the actual database table they will be mapped to.


Classes mapped using the Declarative system are defined in terms of a base class which maintains a catalog of classes and tables relative to that base - this is known as the declarative base class. 
Our application will usually have just one instance of this base in a commonly imported module.

.. code-block:: python

    from sqlalchemy.ext.declarative import declarative_base
    Base = declarative_base()



Now that we have a “base”, we can define any number of mapped classes using this base class.





