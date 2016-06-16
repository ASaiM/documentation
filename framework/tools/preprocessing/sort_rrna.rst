.. _framework-tools-preprocessing-sort-rrna:

==============
Sort rRNA/rDNA
==============


Metagenomic and metatranscriptomic data are constitued of different types of
sequences: sequences corresponding to CDS, sequences corresponding to ribosomal
sequences (rDNA or rRNA), ...

Sequences corresponding to ribosomal sequences (rDNA or rRNA) are useful for
taxonomic assignation. Indeed 16S rRNA is a phylogenetic marker gene, usually
required to analyze the composition of the microbiota data. However, these
sequences do not include any useful information for functional assignation

This information is included in other RNA type like sequences coding for CDS.
However, rRNA sequences are much more present in metatranscriptomic
sequences than other RNA sequences. Functional information can be then difficult
to extract.

Sorting RNA sequences into rRNA and non rRNA sequences facilitates functional
and/or taxonomic assignation by reducing sequence complexity. This treatment
relies on search against rRNA sequence databases to identify and extract rRNA
sequences from all sequences (with
:ref:`SortMeRNA <framework-tools-preprocessing-sort-rrna-sortmerna>`).

.. _framework-tools-preprocessing-sort-rrna-sortmerna:

SortMeRNA
#########

SortMeRNA :cite:`kopylova_sortmerna:_2012` is a software designed to rapidly filter ribosomal RNA fragments
from metatransriptomic data produced by next-generation sequencers.

It is capable of handling large RNA databases and sorting out all fragments
matching to the database with high accuracy and specificity.

The input is one file of reads in FastA or FastQ format and any number of rRNA databases to search against.
If the user has two foward-reverse paired-sequencing reads files, they may use
the script "merge_paired_reads.sh" to interleave the reads into one file, preserving their order.
If the sequencing type for the reads is paired-ended, the user has two options under
"Sequencing type" to filter the reads and preserve their order in the file.
For a further example of each option, please refer to Section 4.2.3 in the `SortMeRNA User Manual <http://bioinfo.lifl.fr/RNA/sortmerna/code/SortMeRNA-user-manual-v1.7.pdf>`_.

The output will follow the same format (FASTA or FASTQ) as the reads. Optionally, a statistic file for the rRNA content of reads, as well as rRNA subunit distribution can be generated.

SortMeRNA is distributed with 8 representative rRNA databases, which were all constructed from the SILVA SSU,LSU (version 111) and the RFAM 5/5.8S (version 11.0) databases using the tool UCLUST.

+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| Representative database  | id % | average id% | # seq (clustered) | Origin                 |  # seq (original) |
+==========================+======+=============+===================+========================+===================+
| SILVA 16S bacteria       |   85 |        91.6 |              8174 | SILVA SSU Ref NR v.111 |            244077 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| SILVA 16S archaea        |   95 |        96.7 |              3845 | SILVA SSU Ref NR v.111 |             10919 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| SILVA 18S eukarya        |   95 |        96.7 |              4512 | SILVA SSU Ref NR v.111 |             31862 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| SILVA 23S bacteria       |   98 |        99.4 |              3055 | SILVA LSU Ref v.111    |             19580 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| SILVA 23s archaea        |   98 |        99.5 |               164 | SILVA LSU Ref v.111    |               405 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| SILVA 28S eukarya        |   98 |        99.1 |              4578 | SILVA LSU Ref v.111    |              9321 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| Rfam 5S archaea/bacteria |   98 |        99.2 |             59513 | RFAM                   |            116760 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+
| Rfam 5.8S eukarya        |   98 |        98.9 |             13034 | RFAM                   |            225185 |
+--------------------------+------+-------------+-------------------+------------------------+-------------------+

id %: members of the cluster must have identity at least 'id %' identity with the representative sequence
average id %: average identity of a cluster member to the representative sequence

The user may also choose to use their own rRNA databases, which are indexed each time. The public ribosomal
databases are indexed when added, but they can be re-indexed with non-default indexing parameters. The indexing may take some time depending on the size of the given database.

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
