.. _framework-tutorial:

Tutorial on metatranscriptomic sequences
########################################

To understand a microbiote, we need answers to questions as "Who is there?", "What are they doing?" and "How are they doing it?". This can be achieved by analysis of metagenomic and metatranscriptomic sequences sampled from interesting environment.

Theses analyses often follow the same scheme (with some variation given the sequences, the questions, ...): sequence pretreatments, taxonomic and functional assignations of the sequences. 

Install the framework
=====================

To :ref:`install the framework <framework-installation>`, clone the `GitHub repository <http://github.com:ASaiM/framework>`_:

.. code-block:: bash

    $ git clone git@github.com:ASaiM/framework.git


Install the required dependencies as described in ``README`` file.

Launch the framework
====================

To :ref:`use the framework <framework-use>`, we recommend to use virtual environment

.. code-block:: bash

    virtualenv --no-site-packages venv
    source venv/bin/activate 

Once the virtual environment is build, the framework can be launched

.. code-block:: bash

    (venv)cd framework
    (venv)./scripts/launch_galaxy.sh

Behind this script, there are Shell scripts which configure the corresponding Galaxy instance. :ref:`Read more about how it works <framework-use-standard>`. 

Once the Galaxy instance is configured, you can browse it on `http://127.0.0.1:8080/ <http://127.0.0.1:8080/>`_. :ref:`Check out how Galaxy is working <framework-galaxy>`.

Get the data
============

Use the toy dataset
-------------------

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
----------------

Upload the choosen dataset on Galaxy
------------------------------------

Process and analyze the dataset
===============================

Pretreatments
-------------

Taxonomic analysis
------------------

Functional analysis
-------------------

Download the outputs
====================

Transform the history of tool execution into a workflow
=======================================================
