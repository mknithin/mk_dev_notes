##########
Docker
##########

Docker is: a way to implement Linux containers!

Linux containers is a way to isolate an entire operating system .


Local development with docker  
*****************************

Developing apps in a docker container have several advantages.
you can develope apps in same production environment and thus avoid deployment surprises.

Which editor/IDE I can use for containerized development ??

Most modern IDE/editors support this feature now a days , I do development python and the main players are Vscode and Pycharm

Pycharm
=======

Pycharm from Jetbrains is the feature rich and the best editor I've ever used for python development.
I done almost all projects with Pycharm, so the interface feels addictive and more familiar 

Pycharm has an option  for  adding a remote interpreter, we can use this to create a containerized development env using 
a docker file or docker compose file.

But while working with this , I found a irritated issue .

When we add a new python package to the requirement file , there is no option available to rebuild the container.

find issue @ https://youtrack.jetbrains.com/issue/PY-17516


Vscode
======

Vscode is a new player  from tech giant microsoft , and it's well supported and open source.
Vscode is actually a text editor which can be transformed to a well equipped IDE with it's vast list of plugins.

I used vscode for my scripting projects but not for big web projects. the autocompletion and django features available in pycharm not allowed
me to do that .

Other than explicit framework support for python, most of the feature are available in vscode.

and microsoft as build a really good python extension for language support 
(I think they recreated the language server recently and named like Pylance, which is available as  a extension for now.)


So back to the topic docker, 

we have 2 options available in vscode to develope apps with docker

#. debug containerized apps by attaching to the container at launch configuration
#. develope inside a container using remote container extension.

I tried the first option several times , but it lacks the language specific feature like intellisens and code completion.

I'm using the second option, ie using remote container extension.
which I feels really good , because the entire dev environment is isolated including the extensions, which will give an options to completely
orchestrate the environment for a particular project , if we have a team working on project then everyone can work on same environment and 
that will be a productivity boost.

Using git in Vscode remote containers
*************************************

How we use git in remote container, a straightforward question I had while trying the vscode remote containers for the first time.
When I checked that in the doc I understood that remote container extension provide out of box support for local git credentials.

But it was not working for me even though the local credentials are set.

I resolved this problem by adding file permission to ~/.gitconfig file(added the +677)


Docker no space left error
**************************
I got this error firstly when I try to install postgre db from a docker compose file.

This is the complete error text

.. code-block::

    fixing permissions on existing directory /var/lib/postgresql/data ... ok
    initdb: could not create directory "/var/lib/postgresql/data/pg_wal": No space left on device
    initdb: removing contents of data directory "/var/lib/postgresql/data"


The solution is to delete the unused images and stope images .

I followed this page 

    https://www.peterbe.com/plog/no-space-left-on-device-on-osx-docker

and this is the command used here to do that 

.. code-block:: shell

    docker container prune
    docker image prune


To refer source host in docker container
****************************************

when you want to refer the source host(your laptop or the server you're running the docker), from a  docker container
use the host name

.. code-block:: shell
    
    host.docker.internal



Docker compose
**************

when changes in any docker file while running compose , always run

.. code-block:: shell
    
   docker-compose up --build





