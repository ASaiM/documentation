.. _framework-tools-available-pretreatments-manipulate-rna:

Manipulate RNA sequences 
########################

Principle
=========

Metatranscriptomic data are constituted of rRNA and other RNA type sequences. rRNA sequences are useful for taxonomic assignation but do not include any useful information for functional assignation. This information is included in other RNA type like mRNA. However, rRNA sequences are much more present in metatranscriptomic sequences than other RNA sequences. Functional information can be then difficult to extract.

Sorting RNA sequences into rRNA and non rRNA sequences facilitates functional and/or taxonomic assignation by reducing sequence complexity. This treatment relies on search against rRNA sequence databases to identify and extract rRNA sequences from all sequences.

Tools
=====

SortMeRNA
---------

..
    .. note::

        Input: sequence file and rRNA database

        Output: aligned and rejected sequence files

SortMeRNA :cite:`kopylova_sortmerna:_2012` is a tool for RNA filtering based on local sequence alignment against rRNA databases. By default, ASaiM framework uses the parameters:

+-------------------------------------+----------------------------------+
|                                     | Default values                   |
+=====================================+==================================+
| rRNA databases                      | All available                    |                          
+-------------------------------------+----------------------------------+
| Database format                     | fasta                            |
+-------------------------------------+----------------------------------+
| Database seed length for clustering | 18                               |
+-------------------------------------+----------------------------------+
| Database seed length for clustering | 10000                            |
+-------------------------------------+----------------------------------+
| Alignment number                    | 0                                |
+-------------------------------------+----------------------------------+
| Best                                | -1                               |
+-------------------------------------+----------------------------------+
| Min Longest Increasing Subsequence  | -1                               |
+-------------------------------------+----------------------------------+
| E-value threshold                   | 1                                |
+-------------------------------------+----------------------------------+
| % identity threshold                | 0.97                             |
+-------------------------------------+----------------------------------+
| % coverage threshold                | 0.97                             |
+-------------------------------------+----------------------------------+
| Passes                              | L, L/2, L/3 with L = seed length |
+-------------------------------------+----------------------------------+
| Edge number                         | 4                                |
+-------------------------------------+----------------------------------+
| Seed number                         | 2                                |
+-------------------------------------+----------------------------------+
| Full search                         | False                            | 
+-------------------------------------+----------------------------------+
| Output fasta/fastq file             | True                             |
+-------------------------------------+----------------------------------+ 
| Output SAM file                     | False                            |
+-------------------------------------+----------------------------------+ 
| Addition of SQ tags in SAM file     | 18                               |  
+-------------------------------------+----------------------------------+ 
| Blast output format                 | 1                                |
+-------------------------------------+----------------------------------+
| Log file                            | True                             |  
+-------------------------------------+----------------------------------+
| Print all reads                     | False                            |
+-------------------------------------+----------------------------------+
| Paired-end in                       | False                            |
+-------------------------------------+----------------------------------+
| Paired-end out                      | False                            |
+-------------------------------------+----------------------------------+
| Matching score                      | 2                                |
+-------------------------------------+----------------------------------+
| Mismatch penalty                    | -3                               |
+-------------------------------------+----------------------------------+
| Gap-open penalty                    | 5                                |
+-------------------------------------+----------------------------------+
| Gap extension penalty               | 2                                |
+-------------------------------------+----------------------------------+
| N addition penalty                  | 2                                |
+-------------------------------------+----------------------------------+
| Search on forward strand            | False                            |
+-------------------------------------+----------------------------------+
| Search on reverse complementary     | False                            |
+-------------------------------------+----------------------------------+
| Thread number to use                | 1                                |
+-------------------------------------+----------------------------------+
| Memory to use for loading reads     | 1024                             |
+-------------------------------------+----------------------------------+
| Add pid to output file names        | False                            |
+-------------------------------------+----------------------------------+


(à revérifier)

Parameters
**********

Several options are "particular":

- number of alignments:
    
    - 1: output the first alignment passing E-value threshold. It is the best choice if only filtering is needed, very fast.
    - higher int for more alignment made and output, speed decrease
    - 0: all alignments reaching the E-value threshold are reported, very slow. This option is not suggested for high similarity rRNA databases, due to many possible alignments per read causing a very large file output

- best:

    - 1: only one high-candidate reference sequence will be searched for alignments (determined heuristically using a longest increasing sub-sequence of seed matches. The single best alignment of those will be reported. Very fast
    - higher int for more alignments, though only the best one will be reported; speed decrease
    - 0: all high-candidate reference sequences will be searched for alignments, though only the best one will be reported; very slow

- output alignments in various Blast-like formats: 0 for pairwise, 1 for tabular (Blast -m 8 format), 2 for tabular + column for CIGAR, 3 for tabular + columns for CIGAR and query coverage (à revoir !!)

- print all reads: output null alignment strings for non-aligned reads off to SAM and/or BLAST tabular files
- paired-end in: both paired-end reads go in aligned sequence file
- paired-end out: both paired-end reads go in non-aligned sequence file
- passes: three intervals at which to place the seed on the read
- edge number: number (or percent if INT followed by % sign) of nucleotides to add to each edge of the read prior to SW local alignment 
- seed number: number of seeds matched before searching for candidate LIS (2, by default)
- full search: search for all 0-error and 1-error seed matches in the index rather than stopping after finding a 0-error match (<1% gain in sensitivity with up four-fold decrease in speed) 
    

Databases
*********

Several rRNA databases are available by default in SortMeRNA:

- silva-bac-16s-id90 from SILVA SSU Ref NR v.119 with 12,798 sequences
- silva-arc-16s-id95 from SILVA SSU Ref NR v.119 origin with 3,193 sequences
- silva-euk-18s-id95 from SILVA SSU Ref NR v.119 with 7,348 sequences
- silva-bac-23s-id98 from SILVA LSU Ref v.119 with 4,488 sequences
- silva-arc-23s-id98 from SILVA LSU Ref v.119 with 251 sequences
- silva-euk-28s-id98 from SILVA LSU Ref v.119 with 4,935 sequences
- rfam-5s-id98 from RFAM with 59,513 seqeunces
- rfam-5.8s-id98 from RFAM with 13,034 sequences

Other databases can be added.

..
    Reago
    -----

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames