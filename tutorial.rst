.. _demo:

ASaiM in demo: Analysis of metatranscriptomic sequences
#######################################################

To illustrate why and how to use ASaiM framework, we generated a toy dataset of metatranscriptomic sequences from an healthy human. 

Data
====

The sequences are coming from human feces microbiota which were sequenced with paired-end Miseq Illumina. From original sequence set, were extracted ... % sequences given the following criteria:

- sequences which match to a module or pathway after :ref:`HUMAnN analysis <for-devs-functional-assignation-pathway-module-analysis-humann>`, with conservation of 10% of the extracted modules/pathways from original dataset analysis
- 0.5% of other sequences

The dataset can be downloaded :ref:`here <>`. It consists in a repository with:

- two sequence files (``R1_sequences.fastq`` and ``R2_sequences.fastq``) which correspond to sequences files from paired-end sequencing
- a configuration file (``config_file.json``). Check out :ref:`the configuration file description <for-devs-configuration-file>` for more information

Pipeline construction
=====================

In the configuration file, is defined the pipeline to execute, which correspond to:

.. image:: images/metatranscriptomic_chart.*

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