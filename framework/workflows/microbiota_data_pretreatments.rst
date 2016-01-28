.. _framework-workflows-microbiota-sequences-pretreatments:

Pretreatments
=============

Before any analyses (taxonomic or functional), raw sequences have to be pre-processed 
(quality control, sequence sorting and construction of long sequences).

Steps depend on type of input sequences (paired-end or single):

.. _microbiota_data_analysis_pretreatment_workflow:

.. figure:: /assets/images/framework/workflows/pretreatment_workflow.png

   Workflows to pre-process microbiota data from raw sequences

In Galaxy, two workflows manage steps of data pretreatment given the type of
input sequences

.. _microbiota_pretreatment_paired_end_workflow:

.. figure:: /assets/images/framework/workflows/microbiota_pretreatment_paired_end_workflow.svg

   Workflow to pre-process microbiota data from raw sequences in Galaxy (paired-end sequences)

.. _microbiota_pretreatment_single_workflow:

.. figure:: /assets/images/framework/workflows/microbiota_pretreatment_single_workflow.svg

   Workflow to pre-process microbiota data from raw sequences in Galaxy (single sequences)

The workflows output 3 sequence files:

- non rRNA sequences
- rRNA sequences

.. _framework-workflows-microbiota-sequences-pretreatments-quality:
Quality control and treatment
#############################

As described in :ref:`description of quality estimation <framework-tools-available-pretreatments-control-quality-estimation>`,
several sequence parameters must be checked to ensure that the raw data looks
good and reduce bias in data.

In this workflow, quality control and treatments are made using PRINSEQ, as 
described in :ref:`quality treatments <framework-tools-available-pretreatments-control-quality-treatment>`:

- Elimination of sequences:
    - with length inferior to 60 bp
    - with a mean quality score inferior to 15
    - with more than 2% of N bases
- Trimming of sequences on right end when the mean quality score over a window of 5 bp is inferior to 20

Quality treatment is applied on raw sequences (before paired-end assembly or any
other step). Indeed paired-end quality treated sequences are needed for 
:ref:`16S sequence reconstruction <framework-workflows-microbiota-sequences-pretreatments-reconstruction>`.

For paired-end sequences, both sequence files are quality treated 
together to limit issue on paired-end assembly.

.. _framework-workflows-microbiota-sequences-pretreatments-assembly:
Paired-end sequences assembly (for paired-end sequences only)
#############################################################

For downstream tools such as SortMeRNA for :ref:`rRNA sorting <framework-workflows-microbiota-sequences-pretreatments-sorting>`,
one sequence file is expected. Paired-end sequences have then to be 
:ref:`assembled <framework-tools-available-pretreatments-assemble>`. 

In the workflow, we use FastQJoin with default parameters:

- Minimum of 6 bp overlap is required to join pairs
- Maximam 8% differences within region of overlap

.. _framework-workflows-microbiota-sequences-pretreatments-sorting:
rRNA (rDNA) sorting
###################

Metagenomic and metatranscriptomic data are constitued of different types of
sequences: sequences corresponding to CDS, sequences corresponding to ribosomal
sequences (rDNA or rRNA), ... 

Useful functional information are present in sequences corresponding to CDS. 
However, in most microbiota sequences, rRNA (or rDNA) sequences are much more 
abundant than other sequences. This overabundance of rRNA can complexify extraction
of functional information. 

To :ref:`sort RNA sequences into rRNA and non rRNA <framework-tools-available-pretreatments-manipulate-rna>`, 
we use SortMeRNA. This tool filter RNA sequences based on local sequence alignment
(BLAST) against rRNA databases (SILVA and RFAM). 
:ref:`Default parameters <framework-tools-available-pretreatments-manipulate-rna-sortmerna>` 
are used, with all available databases.

We could also use :ref:`16S reconstruction <framework-tools-available-pretreatments-manipulate-rna>` 
to get long 16S sequences for better taxonomic assignation. However, Reago requires 
a fixed sequence length. And this can be standard in our worlklow. 


