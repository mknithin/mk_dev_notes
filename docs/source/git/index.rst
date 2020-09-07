##################
Version control using
##################

Details about git VCS


Git submodule authentication issue 
**********************************

Git sub module is option to include a project repo inside another for various reasons.

When such a repository have more than one submodules and the git username and email is not configured globally

then there is a chance that you'll come across this issue 

.. code-block::

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

.. code-block::

    git config --global user.name "your username"
    git config --global user.password "your password"