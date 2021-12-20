###
Git
###

Details about git VCS

Git Submodules doc 
*******************

https://git-scm.com/book/en/v2/Git-Tools-Submodules


Git submodule authentication issue 
**********************************

Git sub module is option to include a project repo inside another for various reasons.

When such a repository have more than one submodules and the git username and email is not configured globally

then there is a chance that you'll come across this issue 

.. code-block:: shell

    remote: HTTP Basic: Access denied
    fatal: Authentication failed for 'https://gitlab.com/d7networks/message_dispatcher.git/'
    fatal: clone of 'https://gitlab.com/d7networks/message_dispatcher' into submodule path '/tmp/direct7-platform/message_dispatcher' failed
    Failed to clone 'message_dispatcher'. Retry scheduled
    Username for 'https://gitlab.com': Password for 'https://gitlab.com':
    Cloning into '/tmp/direct7-platform/message_dispatcher'...
    remote: HTTP Basic: Access denied
    fatal: Authentication failed for 'https://gitlab.com/d7networks/message_dispatcher.git/'
    fatal: clone of 'https://gitlab.com/d7networks/message_dispatcher' into submodule path '/tmp/direct7-platform/message_dispatcher' failed
    Failed to clone 'message_dispatcher' a second time, aborting

Solution is to configure global git username and email , just by doing

.. code-block:: shell

    git config --global user.name "your username"
    git config --global user.password "your password"


Add a submodule  to existing repo
**********************************


.. code-block:: shell

    git submodule add https://github.com/chaconinc/DbConnector

once the submodule is added the repo will be downloaded to the current directory



Cloning a Project with Submodules
**********************************


.. code-block:: shell
    
    git clone --recurse-submodules https://github.com/chaconinc/MainProject



Working on a Project with Submodules
************************************


Pulling in Upstream Changes from the Submodule Remote
#####################################################

The simplest model of using submodules in a project would be if you were simply consuming a subproject and wanted to get updates from it from time to time but were not actually modifying anything in your checkout.

If you want to check for new work in a submodule, you can go into the directory and run git fetch and git merge the upstream branch to update the local code.


.. code-block:: shell
    
    > git fetch

    From https://github.com/chaconinc/DbConnector
   c3f01dc..d0354fc  master     -> origin/master
    
    > git merge origin/master
    
    Updating c3f01dc..d0354fc
    Fast-forward
    scripts/connect.sh | 1 +
    src/db.c           | 1 +
    2 files changed, 2 insertions(+)


There is an easier way to do this as well, if you prefer to not manually fetch and merge in the subdirectory.

.. code-block:: shell
    
    > git submodule update --remote DbConnector
    
    remote: Counting objects: 4, done.
    remote: Compressing objects: 100% (2/2), done.
    remote: Total 4 (delta 2), reused 4 (delta 2)
    Unpacking objects: 100% (4/4), done.
    From https://github.com/chaconinc/DbConnector
    3f19983..d0354fc  master     -> origin/master
    Submodule path 'DbConnector': checked out 'd0354fc054692d3906c85c3af05ddce39a1c0644'


If you set the configuration setting status.submodulesummary, Git will also show you a short summary of changes to your submodules:


.. code-block:: shell
    
    > git config status.submodulesummary 1



Pulling Upstream Changes from the Project Remote
################################################


Simply executing git pull to get your newly committed changes is not enough:

.. code-block:: shell
    
    > $ git pull

    From https://github.com/chaconinc/MainProject
    fb9093c..0a24cfc  master     -> origin/master
    Fetching submodule DbConnector
    From https://github.com/chaconinc/DbConnector
    c3f01dc..c87d55d  stable     -> origin/stable
    Updating fb9093c..0a24cfc
    Fast-forward
    .gitmodules         | 2 +-
    DbConnector         | 2 +-
    2 files changed, 2 insertions(+), 2 deletions(-)

    > git status

    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   DbConnector (new commits)

    Submodules changed but not updated:

    * DbConnector c87d55d...c3f01dc (4):
    < catch non-null terminated lines
    < more robust error handling
    < more efficient db routine
    < better connection routine

    no changes added to commit (use "git add" and/or "git commit -a")


By default, the git pull command recursively fetches submodules changes, as we can see in the output of the first command above. However, it does not update the submodules.

To finalize the update, you need to run git submodule update:


.. code-block:: shell
    
    $ git submodule update --init --recursive
    
    Submodule path 'vendor/plugins/demo': checked out '48679c6302815f6c76f1fe30625d795d9e55fc56'

    $ git status
    
    On branch master
    Your branch is up-to-date with 'origin/master'.
    nothing to commit, working tree clean   


easy way to do this, in one step

.. code-block:: shell
    
    $ git pull --recurse-submodules

