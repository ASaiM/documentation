.. _for-devs-pretreatments-paired-end-assembly:

Assembly of paired-end sequences
################################

For sequences sequenced with paired-end, assembly of paired-end sequences reduces the dataset complexity. :ref:`Read more about paired-end assembly <for-users-pretreatments-paired-end-assembly>`.

ASaiM framework offers the possiblity to assemble paired-end sequences with FastQJoin.

FastQJoin
=========

FastQJoin is a command-line tool available in `ea-utils tools <https://code.google.com/p/ea-utils/>`_ :cite:`aronesty_ea-utils_2011`. Similar to audy's stitch program, it uses the squared distance for anchored alignment, which is a good measure of anchored alignment quality, akin to squared-deviation for means.

For assembly, the overlapping bases are treated as:

- When the bases match, the higher quality base is used
- When the bases don't match, if one quality is greater than 50%, then the resulting quality is the difference between the two qualities (reduced quality due to mismatch), or 50%, whichever is greater.

The default values used in ASaiM framework are:

+--------------------------------------------+-----------------------------------------------------------------+
|                                            | Default threshold and variable name in configuration file       | 
+============================================+=================================================================+
|                                            | 6 bp                                                            |
| Min overlap in bp required to join pairs   +-----------------------------------------------------------------+
|                                            | ``paired_end_assembly_with_fastq_join_min_overlap``             |                          
+--------------------------------------------+-----------------------------------------------------------------+
|                                            | 8                                                               |
| Max % differences within region of overlap +-----------------------------------------------------------------+
|                                            | ``paired_end_assembly_with_fastq_join_perc_max_diff``           |
+--------------------------------------------+-----------------------------------------------------------------+
|                                            | False                                                           |
| Smaller insert                             +-----------------------------------------------------------------+
|                                            | ``paired_end_assembly_with_fastq_join_assembly_smaller_insert`` |
+--------------------------------------------+-----------------------------------------------------------------+

.. rubric:: References

.. bibliography:: ../../../references.bib
   :cited:
   :style: plain
   :filter: docname in docnames

       