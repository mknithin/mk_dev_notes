##################
vscode editor
##################

Everyone knows vscode , a popluar editor from microsoft, I love vscode because of the customization possible with this


Preferred Vscode extension for python development
*************************************************

#. Python extension by microsoft : https://marketplace.visualstudio.com/items?itemName=ms-python.python
#. Visual Studio IntelliCode : https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode
#. Python Docstring Generator : https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring
#. Code bookmarks : https://marketplace.visualstudio.com/items?itemName=alefragnani.Bookmarks
#. Error Lens : https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens


Unresolved import warnings
**************************

If you're getting a warning about an unresolved import, first ensure that the
package is installed into your environment if it is a library (`pip`, `pipenv`, etc).
If the warning is about importing your own code (and not a library), continue reading.

The language server treats the workspace root (i.e. folder you have opened) as
the main root of user module imports. This means that if your imports are not relative
to this path, the language server will not be able to find them. This is common
for users who have a `src` directory which contains their code, a directory for
an installable package, etc. Note that the `src` scenario is automatically detected
by the language server, so no configuration is necessary in that particular case.

These extra roots must be specified to the language server. The easiest way to
do this (with the VS Code Python extension) is to create a workspace configuration
which sets `python.analysis.extraPaths`. For example, if a project uses a
`sources` directory, then create a file `.vscode/settings.json` in the workspace
with the contents:


.. code-block::

    {

        "python.analysis.extraPaths": ["./sources"] 

    }
    


This list can be extended to other paths within the workspace (or even with
code outside the workspace in more complicated setups). Relative paths will
be taken as relative to the workspace root.

Note that if you are coming to Pylance from using the Microsoft Python Language Server, this setting has changed from `python.autoComplete.extraPaths` to `python.analysis.extraPaths`.


To use custom modules in interactive python window
**************************************************

Say when arrange all your custom source code inside a directory call app. and your are trying to access the modules(of course, the python files)from  Python interactive window(Jupyter notebook)

Most probably you'll get a ModuleNotFound Error

When I came across this, I tried many solutions like;

* Adding PYTHONPATH={absolute_path_to_app_dir} in .env file in Work Directory
* Adding PYTHONPATH={absolute_path_to_app_dir} in **terminal.integrated.env.osx** settings

But nothing worked , and the solution that worked is;

changing

.. code-block:: javascript 

    "python.dataScience.notebookFileRoot": "${fileDirname}"

to

.. code-block:: javascript 

    "python.dataScience.notebookFileRoot": "${workspaceFolder}"
