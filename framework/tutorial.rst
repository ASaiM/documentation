.. _framework-tutorial:

========
Tutorial
========

To understand a microbiota environment, we need answers to questions as "Who is there?", "What are they doing?" and "How are they doing it?". This can be achieved by analysis of metagenomic and metatranscriptomic sequences sampled from interesting environment.

These analyses often follow the same scheme (with some variation given the sequences, the questions, ...): sequence pretreatments, taxonomic and functional assignations of the sequences.
These analyses are complex and require numerous tools. :ref:`ASaiM framework <framework>` provides a Galaxy environment to help analyses of gut microbiota data with selected tools, databases and workflows.

In this tutorial, we explain how to use ASaiM framework to analyze metatranscriptomic sequences of gut microbiota to obtain taxonomic and functional assignations of sequences.

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

    ./src/launch_galaxy.sh

This task can take some times because it launch a Galaxy instance and populates it with tools, databases, workflows. 

The Galaxy instance can be browsed on `http://127.0.0.1:8080/ <http://127.0.0.1:8080/>`_.

Galaxy is simple to use. You can check these videos for more informations. Some documentation is also available on :ref:`tool usage <framework-tools-usage>` and :ref:`workflow usage <framework-workflow-usage>`.

..
    Get the data
    ############

    Use the toy dataset
    *******************

    To illustrate why and how to use ASaiM framework on microbiota sequences, a toy dataset of metatranscriptomic sequences from an healthy human is used. 

    The dataset is generated with the sequences coming from human feces microbiota which were sequenced with paired-end Miseq Illumina. The original sequence set has undergone the similar treatments to the ones described in this demo. From original sequence set (> 2.9 millions of sequences), were extracted 6196 sequences given the following criteria:

    - 748 sequences which match to radomly selected modules (5% of extracted modules after :ref:`HUMAnN analysis <for-devs-functional-assignation-pathway-module-analysis-humann>`)
    - 549 sequences which match to radomly selected modules (5% of extracted modules after :ref:`HUMAnN analysis <for-devs-functional-assignation-pathway-module-analysis-humann>`)
    - 1433 (0.1%) sequences which were sorted as rRNA sequences after :ref:`SortMeRNA treatment <for-devs-pretreatments-rna-sorting>`
    - 1475 (5%) sequences which were sorted as non rRNA sequences after :ref:`SortMeRNA treatment <for-devs-pretreatments-rna-sorting>`
    - 1400 (0.1%) sequences which were not joined by :ref:`FastQJoin <for-devs-pretreatments-paired-end-assembly>`
    - 1029 (1%) sequences which were discarded by quality treatment with :ref:`PRINSEQ <for-devs-pretreatments-quality-control-treatment-prinseq>`

    The dataset is included in code sources in ``data/demo`` repository, which is constitued of two sequence files (``R1_sequences.fastq`` and ``R2_sequences.fastq``) which correspond to sequences files from paired-end sequencing.

    Use your dataset
    ****************

    Upload the choosen dataset on Galaxy
    ************************************

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

