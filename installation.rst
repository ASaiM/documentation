.. _installation-running:

Installing and running ASaiM framework
######################################

In a further version, ASaiM framework (pipeline execution, database interrogation, ...) will be used through a web interface. However, currently, the execution of ASaiM framework has to be local.

Requirements
============

To avoid the installation of all proposed tools and to facilitate ASaiM deployment, a pipeline in ASaiM is running through `Docker <https://www.docker.com/>`_ containers (read more about :ref:`the choice of Docker <for-devs-docker>`). Then, `Docker <https://www.docker.com/>`_  and `Docker Compose <https://docs.docker.com/compose/>`_ need to be installed: check out `Docker documentation <https://docs.docker.com>`_  and `Docker Compose installation <https://docs.docker.com/compose/install/>`_.

.. warning:: 
   Docker can not be run on Windows.

   For Mac OS user, a lightweight Linux distribution as `boot2docker <http://boot2docker.io/>`_ is required to run ``Docker``. However, there may be some issues due to limited virtual memory

A pipeline is launched by invocation of :ref:`make <for-devs-workflow-manager>`. Check out `make <https://www.gnu.org/software/make/>`_ for installation.

Download code sources
=====================

The code sources can be directly downloaded:

* Last version of ASaiM as ZIP file
* Last version of ASaiM as TAR.GZ file

or cloned from the `GitHub organization <https://github.com/ASaiM/>`_:

.. code-block:: bash

   git clone git://github.com/ASaiM/


Pipeline generation
===================

A pipeline definition (tools and parameters to use) is saved in :ref:`a configuration file <for-devs-configuration-file>`. This file can be manually or automatically generated via the web interface of `configuration file generator <http://g2im.u-clermont1.fr/asaim/>`_.

Pipeline execution
==================
.. _installation-running-pipeline-execution:

Currently a pipeline can only be executed locally. Code sources have to be downloaded and save in a repository (``path/to/code/src/`` in the following description).

A repository for pipeline execution must be created (``path/to/data/`` in the following description). It will contain all the generated output files. Before pipeline execution, this repository must contain:

- the generated configuration file, which must be named ``config_file.json``
- the sequence file(s) which must be named:
  
  - ``sequences.*`` if the sequences are coming from single-end sequencing
  - ``R1_sequences.*`` and ``R2_sequences.*`` if the sequences are coming from paired-end sequencing
  The sequence file names and path can be modified but these changes have to be also made in the configuration file.

To execute the pipeline, open a terminal and execute the following commands:

.. code-block:: bash

   cd path/to/data
   PATH_TO_SRC = path/to/code/src
   make -f $(PATH_TO_SRC)/Makefile run_pipeline

It's magic (or not, check out :ref:`the workflow manager <for-devs-workflow-manager>`): it's running...


