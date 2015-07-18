.. _for-devs-pretreatments-rna-sorting:
RNA sorting
###########

RNA sorting treatment is used to extract rRNA sequences from all sequences and then facilitae further functional assignation. :ref:`Read more about RNA sorting... <for-users-pretreatments-rna-sorting>`. This treatment is available in ASaiM with SortMeRNA

SortMeRNA
=========

.. note::

    Input: sequence file and rRNA database

    Output: aligned and rejected sequence files

SortMeRNA :cite:`kopylova_sortmerna:_2012` is a tool for RNA filtering based on local sequence alignment against rRNA databases. By default, ASaiM framework uses the parameters:

+-------------------------------------+---------------------------------------------------------------+
|                                     | Default threshold and variable name in configuration file     | 
+=====================================+===============================================================+
|                                     | All available                                                 |
| rRNA databases                      +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_db``                           |                          
+-------------------------------------+---------------------------------------------------------------+
|                                     | fasta                                                         |
| Database format                     +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_db_format``                    |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 18                                                            |
| Database seed length for clustering +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_seed_length``                  |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 10000                                                         | 
| Database seed length for clustering +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_max_nb_position``              |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 0                                                             |
| Alignment number                    +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_num_alignments``               |
+-------------------------------------+---------------------------------------------------------------+
|                                     | -1                                                            |
| Best                                +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_best``                         |
+-------------------------------------+---------------------------------------------------------------+
|                                     | -1                                                            |
| Min Longest Increasing Subsequence  +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_min_lis``                      |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 1                                                             |
| E-value threshold                   +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_e_value_threshold``            |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 0.97                                                          |
| % identity threshold                +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_id``                           |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 0.97                                                          |
| % coverage threshold                +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_coverage``                     |
+-------------------------------------+---------------------------------------------------------------+
|                                     | L, L/2, L/3 with L = seed length                              |
| Passes                              +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_passes``                       |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 4                                                             |
| Edge number                         +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_edges``                        |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 2                                                             |
| Seed number                         +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_num_seeds``                    |
+-------------------------------------+---------------------------------------------------------------+
|                                     | False                                                         |
| Full search                         +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_full_search``                  | 
+-------------------------------------+---------------------------------------------------------------+
|                                     | True                                                          |
| Output fasta/fastq file             +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_fastx``                        |
+-------------------------------------+---------------------------------------------------------------+ 
|                                     | False                                                         |
| Output SAM file                     +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_sam``                          |
+-------------------------------------+---------------------------------------------------------------+ 
|                                     | 18                                                            |
| Addition of SQ tags in SAM file     +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_sq``                           |   
+-------------------------------------+---------------------------------------------------------------+ 
|                                     | 1                                                             |
| Blast output format                 +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_blast``                        |
+-------------------------------------+---------------------------------------------------------------+
|                                     | True                                                          |
| Log file                            +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_log``                          |  
+-------------------------------------+---------------------------------------------------------------+
|                                     | False                                                         |
| Print all reads                     +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_print_all_reads``              |
+-------------------------------------+---------------------------------------------------------------+
|                                     | False                                                         |
| Paired-end in                       +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_paired_in``                    |
+-------------------------------------+---------------------------------------------------------------+
|                                     | False                                                         |
| Paired-end out                      +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_paired_out``                   |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 2                                                             |
| Matching score                      +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_match_score``                  |
+-------------------------------------+---------------------------------------------------------------+
|                                     | -3                                                            |
| Mismatch penalty                    +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_mismatch_penalty``             |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 5                                                             |
| Gap-open penalty                    +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_gap_open_penalty``             |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 2                                                             |
| Gap extension penalty               +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_gap_ext_penalty``              |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 2                                                             |
| N addition penalty                  +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_n_penalty``                    |
+-------------------------------------+---------------------------------------------------------------+
|                                     | False                                                         |
| Search on forward strand            +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_forward_strand_search``        |
+-------------------------------------+---------------------------------------------------------------+
|                                     | False                                                         |
| Search on reverse complementary     +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_reverse_complementary_search`` |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 1                                                             |
| Thread number to use                +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_thread_number``                |
+-------------------------------------+---------------------------------------------------------------+
|                                     | 1024                                                          |
| Memory to use for loading reads     +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_memory``                       |
+-------------------------------------+---------------------------------------------------------------+
|                                     | False                                                         |
| Add pid to output file names        +---------------------------------------------------------------+
|                                     | ``rna_sorting_with_sort_me_rna_pid``                          |
+-------------------------------------+---------------------------------------------------------------+


(à revérifier)





Parameters
----------

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
---------
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

.. rubric:: References

.. bibliography:: ../../../references.bib
   :cited:
   :style: plain
   :filter: docname in docnames

       