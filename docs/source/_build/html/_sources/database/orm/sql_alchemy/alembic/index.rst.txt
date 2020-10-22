***********
Alembic
***********

Database migration using alembic
################################

used for?
**********

Alembic provides for the creation, management, and invocation of change management scripts for a relational database, using SQLAlchemy as the underlying engine.

How to use
**********

Usage of Alembic starts with creation of the Migration Environment. This is a directory of scripts that is specific to a particular application. The migration environment is created just once, and is then maintained along with the application’s source code itself. The environment is created using the init command of Alembic, and is then customizable to suit the specific needs of the application.


.. code-block:: shell

   alembic init alembic

This will generate something like ;


.. code-block:: shell

   yourproject/
    alembic/
        env.py
        README
        script.py.mako
        versions/
            3512b954651e_add_account.py
            2b1ae634e5cd_add_order_id.py
            3adcc9a56557_rename_username_field.py


alembic.ini
***********

Alembic placed a file alembic.ini into the current directory. This is a file that the alembic script looks for when invoked. This file can be anywhere, either in the same directory from which the alembic script will normally be invoked, or if in a different directory, can be specified by using the --config option to the alembic runner.


Create a Migration Script
*************************

With the environment in place we can create a new revision, using alembic revision:

.. code-block:: shell

    $ alembic revision -m "create account table"
    Generating /path/to/yourproject/alembic/versions/1975ea83b712_create_accoun
    t_table.py...done


Auto Generating Migrations
**************************

Alembic can view the status of the database and compare against the table metadata in the application, generating the “obvious” migrations based on a comparison. This is achieved using the --autogenerate option to the alembic revision command, which places so-called candidate migrations into our new migrations file. We review and modify these by hand as needed, then proceed normally.


To use autogenerate, we first need to modify our env.py so that it gets access to a table metadata object that contains the target. Suppose our application has a declarative base in myapp.mymodel. This base contains a MetaData object which contains Table objects defining our database. We make sure this is loaded in env.py and then passed to EnvironmentContext.configure() via the target_metadata argument. The env.py sample script used in the generic template already has a variable declaration near the top for our convenience, where we replace None with our MetaData. Starting with:

.. code-block:: shell

    # add your model's MetaData object here
    # for 'autogenerate' support
    # from myapp import mymodel
    # target_metadata = mymodel.Base.metadata
    target_metadata = None

we change to:


.. code-block:: shell

    from myapp.mymodel import Base
    target_metadata = Base.metadata


Note: The best approach is to import all the model classes to the base file location, thus this module have all the models available before imported by alembic. Otherwise there is chance for alembic generate a empty migration file.
