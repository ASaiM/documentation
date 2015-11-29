.. _framework-use:

Usage
#####

The ASaiM framework is based on a Galaxy instance. Before :ref:`launching the Galaxy instance <framework-use-launch>`, the environment must be configure for Galaxy. Then, the Galaxy instance will run as background task and need a manual intervention to :ref:`stop it<framework-use-stop>` and :ref:`clean Galaxy <framework-use-clean>`.

:ref:`Several tools <framework-tools>` are automatically installed in Galaxy instance using an Ansible playbook. :ref:`Checkout how to add tools and workflows from ToolShed <framework-use-add>`.

.. _framework-use-configure: 

Configure Galaxy environment
============================

PostgreSQL is used to manage databases in Galaxy. It must be launched as a background tasks. PostgreSQL database must be then setup for Galaxy (new database and user creation).
Launch and setup of PostgreSQL is done by running:

.. code-block:: bash

    $ ./src/postgresql/configure_postgres.sh


The FTP server with ``proftpd`` has to be configured and launched, by running:

.. code-block:: bash

    $ ./src/proftpd/configure_proftpd.sh


All the configuration (postgresql and proftpd) can be done by running:

.. code-block:: bash

    $ ./src/configure.sh

.. _framework-use-launch:

Launch ASaiM Galaxy instance
==========================

To launch the Galaxy instance corresponding to ASaiM framework:

.. code-block:: bash

    $ ./src/launch_galaxy.sh

The Galaxy instance can be then browse on `http://127.0.0.1:8080/ <http://127.0.0.1:8080/>`_. 

Galaxy is simple to use. You can check these videos for more informations. Some documentation is also available on :ref:`tool usage <framework-tools-usage>` and :ref:`workflow usage <framework-workflow-usage>`.

``src/launch_galaxy.sh`` script configures a Galaxy instance:

1. Get latest revision of Galaxy from `Github <https://github.com/galaxyproject/galaxy>`_
2. Prepare databases and local tools
3. Configure Galaxy instance with
    - Custom configuration files
    - Wanted tools
    - Wanted databases
4. Launch Galaxy instance
5. Populate Galaxy instance with wanted tools from ToolShed using Ansible playbook

These tasks can take some time, particularly the Galaxy population. After registration with admin account (email: `asaim-admin@asaim.com`), you can 
follow the tool installation in 'Admin' -> 'Manage installed tools' menu.

.. _framework-use-stop:

Stop ASaiM Galaxy instance
========================

Galaxy instance runs as a background task. Stopping it needs a manual intervention:

.. code-block:: bash

    $ ./src/stop_galaxy.sh

This script calls a Galaxy script killing the daemon in which Galaxy has been launched.

.. _framework-use-clean:

Clean Galaxy environment
========================

When Galaxy instance is configure and launched, a database and several directories are created. They can be cleared after usage with:

.. code-block:: bash

    $ ./src/clean_galaxy.sh

This script will:

1. Remove the generated local galaxy directory
2. Remove local directory containing the tools from ToolShed
3. Clear virtual environment
4. Clear PostgreSQL database and user

.. _framework-use-add:

Add tools and workflows to Galaxy instance
==========================================

Tools are installed mainly using an Ansible playbook with wanted tools described in files in ``lib/galaxy_tools_playbook/files/`` directory.

To add new tools, you can modify the files in ``lib/galaxy_tools_playbook/files/`` and launch the script to populate Galaxy:

.. code-block:: bash

    $ ./src/populate_galaxy.sh

You can use the web interface as described here.


