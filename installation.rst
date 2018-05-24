.. _framework-installation:

Installation and use
====================

The ASaiM framework is using the `Galaxy Docker <http://bgruening.github.io/docker-galaxy-stable/>`_ to ease the deployment and customization of the Galaxy instance.

Requirements
************

To use the ASaiM framework, `Docker <https://www.docker.com/products/overview#h_installation>`_ is required.

For Linux users and people familiar with the command line, please follow the `very good instructions <https://docs.docker.com/installation/>`_ from the Docker project.

Non-Linux users are encouraged to use `Kitematic <https://kitematic.com>`_, a graphical User-Interface for managing Docker containers.

    .. raw:: html

        <iframe width="560" height="315" src="https://www.youtube.com/embed/fYer4Xdw_h4" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

    How to use Kitematic for Galaxy Docker, a video realized for the `Galaxy RNA workbench <http://bgruening.github.io/galaxy-rna-workbench>`_.

The databases used by HUMAnN2 are quite big, we recommend to have at least 100 Gb of disk space

Launching ASaiM
***************

1. Starting the ASaiM Docker container: analogous to starting the generic Galaxy Docker image:

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

        A detailed discussion of Docker's parameters is given in the `Docker manual <http://docs.docker.io/>`_. It is really worth reading

    The Docker container is run: Galaxy will be launched!

        Setting up Galaxy and its components can take several minutes. You can inspect the state of the starting using:

        .. code-block:: bash

            $ docker ps # to obtain the id of the container
            $ docker logs <container_id>


    The previous commands will start the ASaiM framework with the configuration and launch of a Galaxy instance and its population with the needed tools, workflows and databases. The instance will be accessible at `http://localhost:8080 <http://localhost:8080>`_

2. Installation of the databases once Galaxy is running

    .. code-block:: bash

        $ docker exec <container_id> ./run_data_managers


Workflows
*********

To access to the workflows, you need to connect with the admin user (username: `admin@galaxy.org`, password: ``admin``). And you will have access to the workflows in the 'Workflow' section (Top panel)

Databases
*********

Databases are automatically added to the Galaxy instance for MetaPhlAn2, HUMAnN2 and QIIME.

Sometimes the databases are not correctly seen by the tools. If it is the case, you need to force the connection between the tool and the database:

- Connect with the admin user:
    - username ``admin@galaxy.org``
    - password ``admin``
- Go to the 'Admin' section (Top panel)
- Go to 'Local data' section (Left panel)
- Click on ``humann2_nucleotide_database``, ``humann2_protein_database`` or ``metaphlan2_database`` (depending on the database)
- Click on the 'Reload button' on the top

    The table must be filled

If you want other databases for HUMAnN2 or QIIME, you can install them "manually":

- Connect with the admin user:
    - username ``admin@galaxy.org``
    - password ``admin``
- Go to the 'Admin' section (Top panel)
- Go to 'Local data' section (Left panel)
- Choose the database you want to import

Interactive session
*******************

For an interactive session, you can execute:

.. code-block:: bash

    $ docker run -i -t -p 8080:80 quay.io/bebatut/asaim-framework /bin/bash

and manually invokes the ``startup`` script to start PostgreSQL, Apache and Galaxy and download the need databases.


For a more specific configuration, you can have a look at the `documentation of the Galaxy Docker Image <http://bgruening.github.io/docker-galaxy-stable/>`_.

Data
****

Docker images are "read-only". All changes during one session are lost after restart. This mode is useful to present ASaiM to your colleagues or to run workshops with it.

To install Tool Shed repositories or to save your data, you need to export the computed data to the host computer. Fortunately, this is as easy as:

.. code-block:: bash

    $ docker run -d -p 8080:80 -v /home/user/galaxy_storage/:/export/ quay.io/bebatut/asaim-framework


Given the additional ``-v /home/user/galaxy_storage/:/export/`` parameter, Docker will mount the folder ``/home/user/galaxy_storage`` into the Container under ``/export/``. A ``startup.sh`` script, that is usually starting Apache, PostgreSQL and Galaxy, will recognize the export directory with one of the following outcomes:

- In case of an empty ``/export/`` directory, it will move the `PostgreSQL <http://www.postgresql.org/>`_ database, the Galaxy database directory, Shed Tools and Tool Dependencies and various configure scripts to /export/ and symlink back to the original location.
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


Stoping ASaiM
*************

Once you are done with the ASaiM framework, you can kill the container:

.. code-block:: bash
    $ docker ps # to obtain the id of the container
    $ docker kill <container_id>

The image corresponding to the container will stay in memory. If you want to clean fully your Docker engine, you can follow the `Docker Cleanup Commands <https://www.calazan.com/docker-cleanup-commands/>`_.


Installation of the tools, workflows and tours on an existing Galaxy instance
*****************************************************************************

The tools, workflows and tours available for ASaiM can be easily installed on any existing Galaxy instance.

The first step is to nstall `Ephemeris <https://ephemeris.readthedocs.io/en/latest/>`_: `conda install ephemeris`

Tools
-----

1. Download the YAML files
    - `asaim_tools_1.yaml <https://raw.githubusercontent.com/ASaiM/framework/master/config/asaim_tools_1.yaml>`_
    - `asaim_tools_2.yaml <https://raw.githubusercontent.com/ASaiM/framework/master/config/asaim_tools_2.yaml>`_
    - `asaim_tools_3.yaml <https://raw.githubusercontent.com/ASaiM/framework/master/config/asaim_tools_3.yaml>`_
2. Install the tools (for each of the three files)

    .. code-block:: bash

        $ shed-install -t <YAML file path> -a <your API key> --galaxy <URL of the Galaxy instance>

Workflows
---------

1. Download the workflow files
    - `Shotgun data analysis <https://raw.githubusercontent.com/ASaiM/framework/master/config/workflows/shotgun_workflow.ga>`_
    - `QIIME Illumina overview <https://raw.githubusercontent.com/ASaiM/framework/master/config/workflows/qiime_illumina_overview_tutorial.ga>`_
    - `EBI Metagenomics V3.0 <https://raw.githubusercontent.com/ASaiM/framework/master/config/workflows/EBI_Metagenomics_workflow_3.0.ga>`_
2. Install the workflows (one by one)

    .. code-block:: bash

        $ workflow-install --workflow_path <GA file path> -a <your API key> --galaxy <URL of the Galaxy instance>

Tours
-----

1. Download the tours
    - `Amplicon data analysis <https://raw.githubusercontent.com/galaxyproject/training-material/master/topics/metagenomics/tutorials/general-tutorial/tours/metagenomics-general-tutorial-amplicon.yml>`_
    - `Shotgun data analysis <https://raw.githubusercontent.com/galaxyproject/training-material/master/topics/metagenomics/tutorials/general-tutorial/tours/metagenomics-general-tutorial-shotgun.yml>`_
2. Put the files on `config/plugins/tours/` of the Galaxy folder
3. Restart the Galaxy instance
