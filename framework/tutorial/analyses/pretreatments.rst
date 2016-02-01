.. _framework-tutorial-pretreatments:

Pretreatments to prepare raw sequences
======================================

Before any analyses (taxonomic or functional), raw sequences have to be pre-processed 
with quality control and sequence sorting. 

In this tutorial, we will only focus on steps for single-end input sequences. But 
several notes will teach how to do with paired-end sequences.

Four main files are created during pretreatments:

- Non rRNA sequences
- 16S rRNA sequences
- 18S rRNA sequences
- Other rRNA sequences

Quality control and treatment
#############################

As described in :ref:`description of quality estimation <framework-tools-available-pretreatments-control-quality-estimation>`,
several sequence parameters must be checked to ensure that raw data looks good 
and then reduce bias in data analysis.

In this tutorial, quality control and treatments are made using PRINSEQ, as 
described in :ref:`quality treatments <framework-tools-available-pretreatments-control-quality-treatment>`:

- Elimination of sequences:
    - with length inferior to 60 bp (to eliminate sequences with too few information)
    - with a mean quality score inferior to 15 (to eliminate bad sequences)
    - with more than 2% of N bases (to eliminate sequences with too few usefull information)
- Trimming of sequences on right end when the mean quality score over a window of 5 bp is inferior to 20 (to improve conserved part of sequences)

To apply quality treatment with PRINSEQ on raw sequences, you click on `Control
quality` on `Pretreatment` section on left pannel. Two tools will be proposed and
you choose `PRINSEQ`. The central panel will be then filled with possible 
options to execute PRINSEQ

.. _prinseq:

.. figure:: /assets/images/framework/tutorial/prinseq.png

In central panel, you choose:

- The type of library (single-end, here)
- The FastQ file (input sequence file, it will be automatically proposed the downloaded file) 
- Parameters
    - Filtering
        - Filtering of sequences based on their length
            - Filtering of too smal sequences with a minimum length of 60 bp
            - No filtering of too big sequences
        - Filtering of sequences based on quality score
            - No filtering of sequences based on their minimum score
            - No filtering of sequences based on their maximum score
            - Filtering of sequences based on their mean score
                - Filtering of sequences with too small mean score with a minimum mean score of 15
                - No filtering of sequences with too high mean score
        - Filtering of sequences based on their base content
            - No filtering of sequences based on their GC percentage
            - No filtering of sequences based on their number of N bases
            - Filtering of sequences based on their percentage of N bases with a maximal N percentage of 2%
            - No filtering of sequences with characters other than A, T, C, G and N
        - Filtering of sequences based on their complexity with a maximum DUST score of 7
    - Trimming
        - No trimming from 3'-end
        - No trimming from the ends
        - No tail trimming
        - Trimming by quality score
            - No trimming by quality score from the 5'-end
            - Trimming by quality score from the 3'-end with a minimum mean quality threshold of 20, computed on a sliding window of 5bp moving by 5bp

.. note::

    For paired-end sequences, both sequence files are quality treated together 
    to limit issue during paired-end assembly. This is done by selected `paired-end`
    in library type

After parameter selection, you click on `Execute`. 3 orange boxes with expected
outputs (good sequences, rejected sequences and a summary).

.. _prinseq_execution:

.. figure:: /assets/images/framework/tutorial/prinseq_execution.png

Once the boxes are green, quality treatments are done. With chosen parameters on 
our datasets (217,386 input sequences with a mean length of bp ), we expect 
conservation of 215,444 (99.09%) sequences with a mean length of 239.29 bp. 
Sequences are filtered mainly because of length.

In quality control of EBI metagenomic workflow, 88.43% of sequences (192,248) 
are conserved. 

.. note::

    For downstream tools such as SortMeRNA for :ref:`rRNA sorting <framework-workflows-microbiota-sequences-pretreatments-sorting>`,
    one sequence file is expected. Paired-end sequences have then to be 
    :ref:`assembled <framework-tools-available-pretreatments-assemble>`. 

    You can use FastQJoin with default parameters:

    - Minimum of 6 bp overlap is required to join pairs
    - Maximum 8% differences within region of overlap

Dereplication
#############

Dereplication corresponds to identification of unique sequences in a dataset to 
conserve only one copy of each sequence in the dataset and then reduce the dataset
size without loosing information.

In ASaiM, this task can be done with `VSearch dereplication` of `VSEARCH` suite 
:cite:`rognes_vsearch:_2015`. 

Sequence file with good quality sequences (PRINSEQ) are in FASTQ format. `VSearch`
tools require FASTA file. So, the file has to be formatted using `Extract` in 
`Manipulate sequence files` section (`Common tools`):

.. _extract_sequence:

.. figure:: /assets/images/framework/tutorial/extract_sequence_file.png

3 files are generated:

- A file with sequences in FASTA format
- A file with quality sequences
- A file with a report

To dereplicate, you execute `Vsearch dereplication` on the sequence file:

.. _vsearch_dereplicate:

.. figure:: /assets/images/framework/tutorial/vsearch_dereplicate.png

In the dataset, 3 sequences (<1%) are removed using dereplication. In EBI 
metagenomic workflow, ~ 4.74% of sequences are removed during this step of 
dereplication.

.. _framework-tutorial-pretreatments-rna-sorting:

rRNA (rDNA) sorting
###################

Metagenomic and metatranscriptomic data are constitued of different types of
sequences: sequences corresponding to CDS, sequences corresponding to ribosomal
sequences (rDNA or rRNA), ... 

Useful functional information are present in sequences corresponding to CDS, and
taxonomic information in sequences corresponding to ribosomomal sequences. To 
enhance downstream analysis such as extraction of functional or taxonomic information, 
it is important to :ref:`sort sequences into rRNA and non rRNA <framework-tools-available-pretreatments-manipulate-rna>`.

For this task, we use SortMeRNA :cite:`kopylova_sortmerna:_2012`. This tool filter 
RNA sequences based on local sequence alignment (BLAST) against rRNA databases. 
With SortMeRNA, 8 rRNA databases are proposed:

- A Rfam database for 5.8S eukarya sequences
- A Rfam database for 5S archea/bacteria sequences
- A SILVA database for 16S archea sequences
- A SILVA database for 16S bacteria sequences
- A SILVA database for 18S eukarya sequences
- A SILVA database for 23S archea sequences
- A SILVA database for 23S bacteria sequences
- A SILVA database for 28S eukarya sequences

16S and 18S sequences are mainly used in taxonomic analyses. So to limitate bias
due to numerous sequences, it is interesting to extract these sequences from
the other rRNA sequences.

So, the step of sequence sorting is split into 3 sub-step:

.. _sequence_sorting_workflow:

.. figure:: /assets/images/framework/tutorial/sequence_sorting.png

SortMeRNA has to be executed 3 times, with different databases. 

For this sequence sorting, you click on `Manipulate RNA` in `Pretreatment` 
section on left pannel. You click then on `Filter with SortMeRNA`. Such as for 
PRINSEQ, parameters for SortMeRNA can be chosed in central panel:

.. _sortmerna_parameters:

.. figure:: /assets/images/framework/tutorial/sortmerna_parameters.png

2 output files are generated:

- A sequence file with `aligned reads` (sequences similar to rRNA databases)
- A sequence file with `rejected reads` (sequences non similar to rRNA databases)

.. note::

    To help file management (numerous files with similar names), we recommend to
    change file names of SortMeRNA outputs

    In left panel, you click on the pencil icon of the file for which
    you want to change name. Several attributes will appear on central panel.
    You can then edit name and save.

In this tutorial, SortMeRNA has to be executed 3 times:

1. First execution of SortMeRNA to split sequences between rRNA and non rRNA sequences
    - Query sequences: output of dereplication
    - rRNA databases: All
2. Second execution of SortMeRNA to split rRNA sequences between 16S rRNA and non 16S rRNA sequences
    - Query sequences: `Aligned reads` of first SortMeRNA execution (rRNA sequences)
    - rRNA databases: SILVA 16S archea and SILVA 16S bacteria
3. Third execution of SortMeRNA to split non 16S rRNA sequences between 18S rRNA and other rRNA sequences
    - Query sequences: `Rejected reads` of second SortMeRNA execution (non 16S rRNA sequences)
    - rRNA databases: SILVA 18S eukarya

For the dataset, we obtain

.. _expected_sequence_sorting:

.. figure:: /assets/images/framework/tutorial/expected_sequence_sorting.png

1,550 sequences (0.72%) are predicted as rRNA sequences. In EBI metagenomics, 
the percentage is similar with 0.50%.


.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames