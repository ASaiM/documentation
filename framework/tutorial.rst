.. _framework-tutorial:

Tutorial
========

To understand a microbiota environment, we need answers to questions as "Who is there?", "What are they doing?" and "How are they doing it?". This can be achieved by analysis of metagenomic and metatranscriptomic sequences sampled from interesting environment.

These analyses often follow the same scheme (with some variation given the sequences, the questions, ...): sequence pretreatments, taxonomic and functional assignations of the sequences.
These analyses are complex and require numerous tools. :ref:`ASaiM framework <framework>` provides a Galaxy environment to help analyses of gut microbiota data with selected tools, databases and workflows.

In this tutorial, we explain how to use ASaiM framework to analyze metagenomic sequences of gut microbiota to obtain taxonomic and functional assignations of sequences. 

Install and configure the framework
###################################

To :ref:`install the framework <framework-installation>`, clone the `GitHub repository <http://github.com:ASaiM/framework>`_:

.. code-block:: bash

    $ git clone git@github.com:ASaiM/framework.git

Move to the corresponding directory:

.. code-block:: bash

    $ cd framework

:ref:`Install the required dependencies <framework-installation-requirements>`:

.. code-block:: bash

    $ ./src/install_dependencies.sh

:ref:`Configure Galaxy environment <framework-use-configure>`:

.. code-block:: bash

    $ ./src/configure.sh

Launch the framework
####################

Once installed and configured, the Galaxy instance on which the framework is based can be :ref:`launched <framework-use-launch>`:

.. code-block:: bash

    $ ./src/launch_galaxy.sh

This task can take some times because it launch a Galaxy instance and populates it with tools, databases, workflows. 

The Galaxy instance can be browsed on `http://127.0.0.1:8080/ <http://127.0.0.1:8080/>`_.

Galaxy is simple to use. You can check these videos for more informations. Some documentation is also available on :ref:`tool usage <framework-tools-usage>` and :ref:`workflow usage <framework-workflow-usage>`.


Get the data
############


To illustrate why and how to use ASaiM framework on microbiota sequences, a dataset of metagenomic sequences from an lean human is used. The data are coming from a study on core gut microbiome in obese and lean twins 

You can also take your own dataset (paired-end or not) of microbiota data. 

The chosen dataset has to be uploaded in Galaxy environment with 'Get Data'->'Upload file' in 'Common tools' section in left bar of Galaxy interface. Several options are proposed

    * direct upload, for files < 2 Gb
    * FTP upload, required for files > 2 Gb



..
    Process and analyze the dataset
    ###############################

    Pretreatments
    *************

    Taxonomic analysis
    ******************

    Functional analysis
    *******************

    Download the outputs
    ####################

    Transform the history of tool execution into a workflow
    #######################################################

Stop Galaxy and clear the environment
#####################################

Galaxy runs as a background process and have to be stopped manually:

.. code-block:: bash

    $ ./src/stop_galaxy.sh

Once stopped, the environment must be cleared with:

.. code-block:: bash

    $ ./src/clean_galaxy.sh

