.. _framework-installation:

Installation and use
====================

The ASaiM framework is using the `Galaxy Docker <http://bgruening.github.io/docker-galaxy-stable/>`_ to ease the deployment and customization of the Galaxy instance. 

If you do not want to use Docker, we also provide :ref:`documentation to setup and run the framework<framework-installation-source>` without using Docker.

.. _framework-installation-docker:
Installation with Docker
########################

Requirements
************

To use the ASaiM framework, `Docker <https://www.docker.com/products/overview#h_installation>`_ is required. 

For Linux users and people familiar with the command line, please follow the `very good instructions <https://docs.docker.com/installation/>`_ from the Docker project. Non-Linux users are encouraged to use `Kitematic <https://kitematic.com>`_, a graphical User-Interface for managing Docker containers.

Launching ASaiM
***************

Starting the ASaiM Docker container is analogous to starting the generic Galaxy Docker image: 

.. code-block:: bash

    $ docker run -d -p 8080:80 quay.io/bebatut/asaim-framework

Nevertheless, here is a quick rundown: 

- ``docker run`` starts the Image/Container

    In case the Container is not already stored locally, Docker downloads it automatically
   
- The argument ``-p 8080:80`` makes the port 80 (inside of the container) available on port 8080 on your host

    Inside the container a Apache web server is running on port 80 and that port can be bound to a local port on your host computer. 
    With this parameter you can access your Galaxy instance via `http://localhost:8080` immediately after executing the command above
    
- ``quay.io/bebatut/asaim-framework`` is the Image/Container name, that directs Docker to the correct path in the Docker index
- ``-d`` will start the Docker container in Daemon mode. 

> A detailed discussion of Docker's parameters is given in the `Docker manual <http://docs.docker.io/>`_. It is really worth reading.

For an interactive session, you can execute:

.. code-block:: bash

    $ docker run -i -t -p 8080:80 bebatut/asaim-framework /bin/bash


and manually invokes the ``startup`` script to start PostgreSQL, Apache and Galaxy.

For a more specific configuration, you can have a look at the `documentation of the Galaxy Docker Image <http://bgruening.github.io/docker-galaxy-stable/>`_.

Data
****

Docker images are "read-only". All changes during one session are lost after restart. This mode is useful to present ASaiM to your colleagues or to run workshops with it. 

To install Tool Shed repositories or to save your data, you need to export the computed data to the host computer. Fortunately, this is as easy as:

.. code-block:: bash

    $ docker run -d -p 8080:80 -v /home/user/galaxy_storage/:/export/ bebatut/asaim-framework


Given the additional ``-v /home/user/galaxy_storage/:/export/`` parameter, Docker will mount the folder ``/home/user/galaxy_storage`` into the Container under ``/export/``. A ``startup.sh`` script, that is usually starting Apache, PostgreSQL and Galaxy, will recognize the export directory with one of the following outcomes:

- In case of an empty ``/export/`` directory, it will move the `PostgreSQL <http://www.postgresql.org/>_` database, the Galaxy database directory, Shed Tools and Tool Dependencies and various configure scripts to /export/ and symlink back to the original location.
- In case of a non-empty ``/export/``, for example if you continue a previous session within the same folder, nothing will be moved, but the symlinks will be created.

This enables you to have different export folders for different sessions - meaning real separation of your different projects.

Usage of ASaiM
**************

The previous commands will start the ASaiM framework with the configuration and launch of a Galaxy instance and its population with the needed tools, workflows and databases. The instance will be accessible at `http://localhost:8080 <http://localhost:8080>`_.

Users & Passwords
*****************

The Galaxy Admin User has the username `admin@galaxy.org` and the password `admin`.

The PostgreSQL username is `galaxy`, the password `galaxy` and the database name `galaxy`.
If you want to create new users, please make sure to use the ``/export/`` volume. Otherwise your user will be removed after your Docker session is finished.


.. _framework-installation-source:
Installation from source
########################

Before :ref:`deploying the custom Galaxy instance <framework-use-launch>`, the environment must be :ref:`configure <framework-use-configure>` for Galaxy. And, after deployment, the custom Galaxy instance will run as background task and need a manual intervention to :ref:`stop it<framework-use-stop>` and :ref:`clean Galaxy <framework-use-clean>`.

.. _framework_use_virtual_circle:

.. figure:: /assets/images/framework/usage/virtual_circle.png
    :align: center

    Virtual circle to get ASaiM framework correctly running

:ref:`Selected tools <framework-tools>` are automatically installed in Galaxy instance using an Ansible playbook. If you want to add more, :ref:`checkout how to add tools and workflows from ToolShed <framework-use-add-tools>`.

Download code sources
*********************

Source code of ASaiM framework are available on a `GitHub repository <https://github.com/ASaiM/framework/>`_.

Git
---

To get ASaiM framework, ``git`` clone the project:

.. code-block:: bash

    $ git clone http://github.com/ASaiM/framework.git

Releases
--------

All releases of ASaiM framework can be found at `https://github.com/ASaiM/framework/releases <https://github.com/ASaiM/framework/releases>`_.

.. _framework-installation-requirements:

Requirements
************

Some tools must be installed:

- ``git``
- ``python``
- ``pip``
- ``perl``
- ``scons``
- ``mercurial``
- ``openssl``
- ``java``
- ``wget``
- ``openssl``
- ``proftpd``
- ``postgresql``

It can be automatically done by running:

.. code-block:: bash

    $ ./src/install_dependencies.sh

.. note::

    ``apt-get`` is required for Debian, ``yum`` for RHEL and ``homebrew`` for MacOSX.

.. _framework-use-configure:

Configure Galaxy environment
****************************

PostgreSQL is used to manage databases in Galaxy. It must be launched as a background task and setup for Galaxy (new database and user creation).

On the other hand, a FTP server with ``proftpd`` has to be configured and launched.

All the configuration tasks (postgresql and proftpd) can be done by running:

.. code-block:: bash

    $ ./src/configure.sh


.. _framework-use-launch:

Launch ASaiM framework
**********************

To launch the custom Galaxy instance and populate it with dedicated tools and databases :

.. code-block:: bash

    $ ./src/launch_asaim.sh

This task, particularly tool population, can take several hours.

However, once tool population starts, the Galaxy instance can be then browse on `http://127.0.0.1:8080/ <http://127.0.0.1:8080/>`_. And after registration with admin account (email: `asaim-admin@asaim.com`), you can follow tool installation in `Admin` -> `Manage installed tools`.

After installation of the tools, HUMAnN2 databases have to be downloaded (once). It can be done using the dedicated tool available in `STRUCTURAL AND FUNCTIONAL ANALYSIS TOOLS` -> `Analyze metabolism` -> `Download HUMAnN2 databases`. This tool have to be executed twice: once for nucleotide (ChocoPhlAn) database and once for protein (UniRef50) database.

.. _framework-use-add-workflows:

Add workflows
*************

Workflows are not automatically added to the Galaxy instance.

To add them (after tool population):

- Go to `Workflow` menu (top panel)
- Click on `Upload or import workflows` (on top right)
    - Paste the following URL (one at a time) in "Galaxy workflow URL" field
        - Main workflow: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_main_workflow.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_main_workflow.ga>`_
        - Comparative analysis workflows:
            - For taxonomic results: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomic_result_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomic_result_comparative_analysis.ga>`_
            - For functional results (gene families or pathways): `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_functional_result_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_functional_result_comparative_analysis.ga>`_
            - For GO slim terms: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_go_slim_terms_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_go_slim_terms_comparative_analysis.ga>`_
            - For taxonomically-related functional results: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomically_related_functional_result_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomically_related_functional_result_comparative_analysis.ga>`_
    - Click on `Import`
- Do it again with other workflows


.. _framework-use-add-tools:

Add tools from ToolShed to the custom Galaxy instance
*****************************************************

To add tools from ToolShed, you can also add reference to this tool in files in `data/chosen_tools` and then launch:

.. code-block:: bash

    $ ./src/prepare_asaim/populate_galaxy.sh

Alternatively, you can use the web interface and add other tools via ToolShed.
Once register, you go in `Admin` (tool panel) and then `Search Tool Shed` (left panel). You choose which ToolShed to browse, search the wanted tool on the ToolShed, click on it to get `Preview and install` and then on `Install to Galaxy` (on top), choose in which tool section adding it and then click on `Install`.

.. _framework-use-stop:

Stop ASaiM framework
********************

The custom Galaxy instance runs as a background task. Stopping it needs a manual intervention:

.. code-block:: bash

    $ ./src/stop_galaxy.sh


.. _framework-use-clean:

Clean Galaxy environment
************************

When Galaxy instance is configure and launched, a database and several directories are created. They can be cleared after usage with:

.. code-block:: bash

    $ ./src/clean_asaim.sh

