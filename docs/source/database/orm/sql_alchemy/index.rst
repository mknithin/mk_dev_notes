***********
SQL Alchemy
***********

The function of a ORM(object relational mapper) is associating user defined python  classes with database tables.
And the SQL Alchemy is doing the exact same thing here.

So here a instance of  python classes (objects) represent rows in their corresponding tables. 

SQL Alchemy ORM, is build on top of the Expression Language.which is the general way to interact with the DB in SQL Alchemy.


Fundamentals
************

*  A collection of Table objects and their associated child objects is referred to as **database metadata**

Connecting to DB
################

To create connection ,we need to create a instance of Alchemy Engine class and it represents the core interface to the database, adapted through a **dialect** (consider it as a db driver) that handles the details of the database and DBAPI in use.


.. code-block:: python

    >>> from sqlalchemy import create_engine
    >>> engine = create_engine('postgresql://nithinmk:@localhost/alembic_trial', echo=True)


The Engine establishes the DBAPI connection when we call method  like **Engine.execute()** or **Engine.connect()**
When using the ORM, we typically don’t use the Engine directly once created; instead, it’s used behind the scenes by the ORM.

Declare a Mapping
#################

When using the ORM, the configurational process starts by describing the database tables we’ll be dealing with, and then by defining our own classes which will be mapped to those tables. 
In modern SQLAlchemy, these two tasks are usually performed together, using a system known as **Declarative** , which allows us to create classes that include directives to describe the actual database table they will be mapped to.


Classes mapped using the Declarative system are defined in terms of a base class which maintains a catalog of classes and tables relative to that base - this is known as the declarative base class. 
Our application will usually have just one instance of this base in a commonly imported module.

.. code-block:: python

    >>> from sqlalchemy.ext.declarative import declarative_base
    >>> Base = declarative_base()



Now that we have a “base”, we can define any number of mapped classes using this base class.

Create a Schema
###############

SQL ALchemy represents information for a specific table using **Table** , and the declarative system will automatically construct this(Table metadata) for us.

The Table object is a member of a larger collection known as **MetaData**. When using Declarative, this object is available using the .metadata attribute of our declarative base class.

The MetaData is a registry which includes the ability to emit a limited set of schema generation commands to the database. 

we can use MetaData to issue CREATE TABLE statements to the database for all tables that don’t yet exist.
we call the **MetaData.create_all()** method, passing in our Engine as a source of database connectivity.


.. code-block:: shell

    >>> Base.metadata.create_all(engine)

Creating a Session
###################

The ORM’s “handle” to the database is the **Session**. 
When we first set up the application, at the same level as our create_engine() statement, we define a Session class which will serve as a factory for new Session objects.

.. code-block:: python

    >>> from sqlalchemy.orm import sessionmaker
    >>> Session = sessionmaker(bind=engine)

By creating a session object won't open a any new connection to DB, When it’s first used, it retrieves a connection from a pool of connections maintained by the Engine, and holds onto it until we commit all changes and/or close the session object.


Adding and Updating Objects
###########################

To persist our User object, we Session.add() it to our Session

.. code-block:: python

    >>> ed_user = User(name='ed', fullname='Ed Jo`nes', nickname='edsnickname')
    >>> session.add(ed_user)

At this point, we say that the instance is pending; no SQL has yet been issued and the object is not yet represented by a row in the database. 
The Session will issue the SQL to persist Ed Jones as soon as is needed, using a process known as a **flush**. 

For example, below we create a new Query object which loads instances of User.

.. code-block:: python

    >>> our_user = session.query(User).filter_by(name='ed').first()

Here In fact, the Session has identified that the row returned is the same row as one already represented within its internal map of objects.

The ORM concept at work here is known as an identity map and ensures that all operations upon a particular row within a Session operate upon the same set of data.

We can add more User objects at once using add_all()

.. code-block:: python

    >>> session.add_all([
        User(name='wendy', fullname='Wendy Williams', nickname='windy'),
        User(name='mary', fullname='Mary Contrary', nickname='mary'),
        User(name='fred', fullname='Fred Flintstone', nickname='freddy')])

we’ve decided Ed’s nickname isn’t that great, so lets change it:

.. code-block:: python
    
    >>> ed_user.nickname = 'eddie'

Here the Session is paying attention. It knows, for example, that Ed Jones has been modified:


.. code-block:: python
    
    >>> session.dirty
    IdentitySet([<User(name='ed', fullname='Ed Jones', nickname='eddie')>])

Now  to issue all remaining changes to the database and commit the transaction, which has been in progress throughout. We do this via **Session.commit()**.


.. code-block:: python
    
    >>> session.commit()