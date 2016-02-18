.. _framework-use:

Usage
=====

The ASaiM framework is based on a Galaxy instance. Before :ref:`launching the Galaxy instance <framework-use-launch>`, the environment must be configure for Galaxy. Then, the Galaxy instance will run as background task and need a manual intervention to :ref:`stop it<framework-use-stop>` and :ref:`clean Galaxy <framework-use-clean>`.

.. _framework_use_virtual_circle:

.. figure:: /assets/images/framework/usage/virtual_circle.png
    :align: center

    Virtual circle to get ASaiM framework correctly running

:ref:`Chosen tools <framework-tools>` are automatically installed in Galaxy instance using an Ansible playbook. If you want to add more, :ref:`checkout how to add tools and workflows from ToolShed <framework-use-add-tools>`.

.. _framework-use-configure: 

Configure Galaxy environment
############################

All the configuration (PostgreSQL to manage user and tool databases and proftpd for FTP server) can be done by running:

.. code-block:: bash

    $ ./src/configure.sh

Behind this script, two scripts are launched.

PostgreSQL, used to manage databases in Galaxy, must be launched as a background tasks and setup for Galaxy (new database and user creation). It is done by running:

.. code-block:: bash

    $ ./src/postgresql/configure_postgres.sh


The FTP server with ``proftpd`` is configured and launched with:

.. code-block:: bash

    $ ./src/proftpd/configure_proftpd.sh


.. _framework-use-launch:

Launch ASaiM Galaxy instance
############################

To launch the Galaxy instance corresponding to ASaiM framework:

.. code-block:: bash

    $ ./src/launch_galaxy.sh

The Galaxy instance can be then browsed on `http://0.0.0.0:8080/ <http://0.0.0.0:8080/>`_. 

Galaxy is simple to use. Some documentation is available on :ref:`tool usage <framework-tools-usage>` and :ref:`workflow usage <framework-workflow-usage>`.

``src/launch_galaxy.sh`` script configures a Galaxy instance:

1. Get latest revision of Galaxy from `Github <https://github.com/galaxyproject/galaxy>`_
2. Prepare databases and local tools
3. Configure Galaxy instance with
    - Custom configuration files
    - Wanted tools
    - Wanted databases
4. Launch Galaxy instance on `http://0.0.0.0:8080/ <http://0.0.0.0:8080/>`_
5. :ref:`Populate Galaxy instance with wanted tools from ToolShed using Ansible playbook <framework-use-add-tools>`
6. :ref:`Populate Galaxy instance with needed databases <framework-use-add-db>`

These tasks can take several hours. Main time-consumer task is Galaxy population with tools. However, during this task, you already have access to Galaxy instance on `http://0.0.0.0:8080/ <http://0.0.0.0:8080/>`_. 

You can also follow correct installation of tools `Admin` (tool panel) -> `Manage installed tools` (left panel), after registration with admin account (email: `asaim-admin@asaim.com`, any password). 

.. _framework-use-add-tools:

Add tools and workflows to Galaxy instance
------------------------------------------

Tools are installed mainly using an Ansible playbook with wanted tools described in files in ``lib/galaxy_tools_playbook/files/`` directory.

To add new tools, you can modify the files in ``lib/galaxy_tools_playbook/files/`` and launch the script to populate Galaxy:

.. code-block:: bash

    $ ./src/populate_galaxy.sh

Alternatively, you can use the web interface and add other tools via ToolShed.
Once register, you go in `Admin` (tool panel) and then `Search Tool Shed` (left panel). You choose which ToolShed to browse, search the wanted tool on the ToolShed, click on it to get `Preview and install`, click on `Install to Galaxy` (on top), choose in which tool section adding it and then click on `Install`. 

.. _framework-use-add-db:

Add databases to Galaxy instance
--------------------------------

Needed databases are downloaded and linked to Galaxy tools using bash script:

.. code-block:: bash

    $ ./src/prepare_databases.sh

.. _framework-use-stop:

Stop ASaiM Galaxy instance
##########################

Galaxy instance runs as a background task. Stopping it needs a manual intervention:

.. code-block:: bash

    $ ./src/stop_galaxy.sh

This script calls a Galaxy script killing the daemon in which Galaxy has been launched.

.. _framework-use-clean:

Clean Galaxy environment
########################

When Galaxy instance is configure and launched, a database and several directories are created. They can be cleared after usage with:

.. code-block:: bash

    $ ./src/clean_galaxy.sh

This script will:

1. Remove the generated local galaxy directory
2. Remove local directory containing the tools from ToolShed
3. Clear virtual environment
4. Clear PostgreSQL database and user





