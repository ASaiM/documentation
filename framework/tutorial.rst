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

The Galaxy instance can be browsed on `http://0.0.0.0:8080/ <http://0.0.0.0:8080/>`_.

Galaxy is simple to use. You can check these videos for more informations. Some documentation is also available on :ref:`tool usage <framework-tools-usage>` and :ref:`workflow usage <framework-workflow-usage>`.


Get the data
############

To illustrate why and how to use ASaiM framework on microbiota sequences, a 
dataset of metagenomic sequences from an lean human is used. The data are coming 
from a study on core gut microbiome in obese and lean twins :cite:`turnbaugh_core_2009`, 
available on `EBI metagenomic <https://www.ebi.ac.uk/metagenomics/projects/SRP000319>`_. 
We chosed data from 
`Patient TS1 <https://www.ebi.ac.uk/metagenomics/projects/SRP000319/samples/SRS000998/runs/SRR029687/results/versions/1.0>`_ 
(lean woman). Raw data are available 
`here <ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR029/SRR029687/SRR029687.fastq.gz>`_. 

These data were also analyzed with `EBI metagenomic <https://www.ebi.ac.uk/metagenomics/about>`_. 
Our quality control, taxonomic and functional analyses results can be compared to 
the `one obtained by EBI metagenomic workflow <https://www.ebi.ac.uk/metagenomics/projects/SRP000319/samples/SRS000998/runs/SRR029687/results/versions/1.0>`_.

You can also take your own dataset (paired-end or not) of microbiota data. 

The chosen dataset has to be uploaded in Galaxy environment with `Get Data` -> `Upload 
file` in `Common tools` section in left panel of Galaxy interface. 

.. _get_data:

.. figure:: /assets/images/framework/tutorial/get_data.png

Several download options are proposed

    * direct upload, for files < 2 Gb
    * FTP upload, required for files > 2 Gb

The downloaded file will then be visible inside right panel (`History`)

.. _upload_data:

.. figure:: /assets/images/framework/tutorial/upload_data.png

This right panel will concentrate all files (input files, output files and any
intermediary files). In this panel, you can also "follow" execution of a task.
When a task is launched, the expected output files will be visible on the right
panel, in orange boxes. When the task is done, the output file
boxes will become green or red in case of execution error.

Process and analyze the dataset
###############################

Extraction of useful information from raw microbiota sequences is a complex process 
with numerous steps:

.. _data_processing:

.. figure:: /assets/images/framework/workflows/simplified_workflow.png

These steps can be get together in 3 main steps:

- :ref:`Pretreatments <framework-tutorial-pretreatments>` to prepare raw sequences
- :ref:`Taxonomic analysis <framework-tutorial-taxonomic-analysis>` to extract microbiota structure
- :ref:`Functional analysis <framework-tutorial-functional-analysis>` to extract microbiota metabolism

In this tutorial, we will execute each step of the workflow to extract useful
information from 

.. _framework-tutorial-pretreatments:

Pretreatments
*************

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
-----------------------------

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
-------------

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
-------------------

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

.. _framework-tutorial-taxonomic-analysis:

Taxonomic analysis
******************

To identify micro-organisms populating a sample and their proportion, we use 
:ref:`taxonomic and phylogenetic approaches <framework-tools-available-taxonomic-assignation>`. 
Indeed, in these approaches, each reads or sequences are assigned to the most 
plausible microbial lineage. 

Most tools used to estimate sample composition use 16S rRNA genes as marker for
bacteria and archea and 18S rRNA genes for eukarya. It is the approache used by
QIIME :cite:`caporaso_qiime_2010` and 
:ref:`taxonomic analysis of rRNA sequences <framework-tutorial-taxonomic-analysis-nonrRNA>`.

Other tools, such as MetaPhlAn :cite:`segata_metagenomic_2012,truong_metaphlan2_2015`,
propose alternatives based on more general clade-specific marker genes. We can
use such approaches to :ref:`analyze taxonomy of non rRNA sequences <framework-tutorial-taxonomic-analysis-rRNA>`.

.. _framework-tutorial-taxonomic-analysis-nonrRNA:

Taxonomic analysis on rRNA sequences
------------------------------------


.. _framework-tutorial-taxonomic-analysis-rRNA:

Taxonomic analysis on non rRNA sequences
----------------------------------------

To estimate sample composition, we can also use MetaPhlAn2 :cite:`truong_metaphlan2_2015`
on non rRNA sequences. This tool infer the presence and read coverage of 
clade-specific markers to detect taxonomic clades and their relative abundance.

This tool is available on left panel in `Assign taxonomy on non rRNA sequences` 
(`Taxonomic assignation`). In this tutorial, you execute it on non rRNA sequences
from first :ref:`SortMeRNA execution <framework-tutorial-pretreatments-rna-sorting>`.

.. _metaphlan_2_parameters:

.. figure:: /assets/images/framework/tutorial/metaphlan_2.png

In the dataset, we obtain a text file with 59 lines, each line corresponding to
a taxonomic assignation (represented at different taxonomic level) with its
relative abundance.

.. _metaphlan_2_output:

.. figure:: /assets/images/framework/tutorial/metaphlan_2_output.png

To get a graphical visualisation of MetaPhlAn 2 output, you can use GraPhlAn after
applying `Export to GraPhlAn`.



.. _framework-tutorial-functional-analysis:

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

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames

