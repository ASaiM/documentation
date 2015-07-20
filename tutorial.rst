.. _demo:

ASaiM in demo: Analysis of metatranscriptomic sequences
#######################################################

To illustrate why and how to use ASaiM framework, we generated a toy dataset of metatranscriptomic sequences from an healthy human. 

Data
====

The sequences are coming from human feces microbiota which were sequenced with paired-end Miseq Illumina. The original sequence set has undergone the similar treatments to the ones described in this demo. From original sequence set (> 2.9 millions of sequences), were extracted 6196 sequences given the following criteria:

- 748 sequences which match to radomly selected modules (5% of extracted modules after :ref:`HUMAnN analysis <for-devs-functional-assignation-pathway-module-analysis-humann>`)
- 549 sequences which match to radomly selected modules (5% of extracted modules after :ref:`HUMAnN analysis <for-devs-functional-assignation-pathway-module-analysis-humann>`)
- 1433 (0.1%) sequences which were sorted as rRNA sequences after :ref:`SortMeRNA treatment <for-devs-pretreatments-rna-sorting>`
- 1475 (5%) sequences which were sorted as non rRNA sequences after :ref:`SortMeRNA treatment <for-devs-pretreatments-rna-sorting>`
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

   make -f path/to/src/Makefile run_pipeline


Generated outputs
=================

The pipeline execute generates a directory in which all the outputs are grouped per treatments. For the demo, the generated directory is:

.. code-block:: bash

    2015-07-02_19-31/
        report.txt
        quality_estimation/
            FastQC/
                <FastQC output files>
        quality_treatments/
            Prinseq/
                <Prinseq output files>
        paired_end_assembly/
            FastQ_Join/
                <FastQ_Join output files>
        rna_sorting/
            SortMeRNA/
                <SortMeRNA output files>
        non_rRNA_taxonomic_assignation/
            MetaPhlAn/
                <MetaPhlAn output files>
        protein_ncrna_db_search/
            search_against_cog/
                Blast/
                    <Blast output files>

The ``report.txt`` reports executed treatments and tools and some preliminary results.


.. Post-treatments
.. ===============

.. Comparison with similar data
.. ============================
