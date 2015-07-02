.. _demo:

ASaiM in demo: Analysis of metatranscriptomic sequences
#######################################################

To illustrate why and how to use ASaiM framework, we generated a toy dataset of metatranscriptomic sequences from an healthy human. 

Data
====

The sequences are coming from human feces microbiota which were sequenced with paired-end Miseq Illumina. The original sequence set has undergone the similar treatments to the ones described in this demo. From original sequence set (> 2.9 millions of sequences), were extracted 6196 sequences given the following criteria:

- 748 sequences which match to radomly selected modules (5% of extracted modules after :ref:`HUMAnN analysis <for-devs-functional-assignation-pathway-module-analysis-humann>`)
- 116 sequences which match to radomly selected modules (5% of extracted modules after :ref:`HUMAnN analysis <for-devs-functional-assignation-pathway-module-analysis-humann>`)
- 1433 (0.1%) sequences which were sorted as rRNA sequences after :ref:`SortMeRNA treatment <for-devs-pretreatments-rna-sorting>`
- 1470 (5%) sequences which were sorted as non rRNA sequences after :ref:`SortMeRNA treatment <for-devs-pretreatments-rna-sorting>`
- 1400 (0.1%) sequences which were not joined by :ref:`FastQJoin <for-devs-pretreatments-paired-end-assembly>`
- 1029 (1%) sequences which were discarded by quality treatment with :ref:`PRINSEQ <for-devs-pretreatments-quality-control-treatment-prinseq>`

The dataset is included in code sources in ``demo`` repository, which cis constitued of:

- two sequence files (``R1_sequences.fastq`` and ``R2_sequences.fastq``) which correspond to sequences files from paired-end sequencing
- a configuration file (``config_file.json``). Check out :ref:`the configuration file description <for-devs-configuration-file>` for more information

Pipeline construction
=====================

In the configuration file, is defined the pipeline to execute, which correspond to:

.. image:: images/demo_pipeline.*

The generated pipeline follows :ref:`our recommendations <pipeline-construction-metatranscriptomic>` to process metatranscriptomic sequences from raw sequences to taxonomic and functional assignation.

Pipeline execution
==================

The execution of the generated pipeline on this dataset follows :ref:`the previously described rules<installation-running-pipeline-execution>`. From the data repository, in a terminal:

.. code-block:: bash

   make -f path/to/src/makefile run_pipeline


Generated outputs
=================

Post-treatments
===============

Comparison with similar data
============================