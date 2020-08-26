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

Vscode is a new payer from tech giant microsoft , and it's well supported and open source.
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


Setup a docker dev environment in Vscode
****************************************

