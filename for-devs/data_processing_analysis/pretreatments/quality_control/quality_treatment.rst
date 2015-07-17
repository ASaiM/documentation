.. _for-devs-pretreatments-quality-control-treatment:

Quality treatment
#################

To improve the sequence quality and limit the bias in downstream analyses, :ref:`the sequences must be treated with (generally) <for-users-pretreatments-quality-control-treatment>`:

- Elimination of sequences having a mean quality score below the defined threshold
- Quality trimming on sequence ends
- Elimination of sequences having a N content higher than the defined threshold
- Reduction of nucleotide frequency bias
- Removal of adapter sequences
- Removal of reads with smaller than a threshold

These treatments can be made with 2 types of sequence quality treatments (:ref:`filtering <for-users-pretreatments-quality-control-treatment-filter>` and :ref:`trimming <for-users-pretreatments-quality-control-treatment-trim>`) and several tools. Currently only :ref:`PRINSEQ <for-devs-pretreatments-quality-control-treatment-prinseq>` is available in ASaiM framework.


.. _for-devs-pretreatments-quality-control-treatment-prinseq:
PRINSEQ
=======

.. note::

    Input: sequence file with quality values for each base

    Output: quality treated sequence file

PRINSEQ :cite:`schmieder_quality_2011` is a tool for easy and rapid quality control and data preprocessing of metagenomic and metatranscriptomic datasets. This tool allow to process the sequences with :ref:`filtering <for-users-pretreatments-quality-control-treatment-filter>` and :ref:`trimming <for-users-pretreatments-quality-control-treatment-trim>`.


Filter treatments
-----------------

By default in ASaiM framework, the values for the filter treatments are:

+----------------------------+-----------------------------------------------------------+
|                            | Default threshold and variable name in configuration file | 
+============================+===========================================================+
|                            | 60 bp                                                     |
| Minimum sequence length    +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_length_max``             |
+----------------------------+-----------------------------------------------------------+
|                            | Null (No treatment)                                       |
| Maximum sequence length    +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_length_max``             |
+----------------------------+-----------------------------------------------------------+
|                            | Null (No treatment)                                       |
| Minimum quality score      +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_score_min``              |
+----------------------------+-----------------------------------------------------------+
|                            | Null (No treatment)                                       |
| Maximum quality score      +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_score_max``              |
+----------------------------+-----------------------------------------------------------+
|                            | 15                                                        |
| Minimum mean quality score +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_score_mean_min``         |
+----------------------------+-----------------------------------------------------------+
|                            | Null (No treatment)                                       |
| Maximum mean quality score +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_length_max``             |
+----------------------------+-----------------------------------------------------------+
|                            | Null (No treatment)                                       |
| Minimum GC percentage      +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_gc_min``                 |
+----------------------------+-----------------------------------------------------------+
|                            | Null (No treatment)                                       |
| Maximum GC percentage      +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_score_mean_max``         |
+----------------------------+-----------------------------------------------------------+
|                            | 2                                                         |
| N percentage               +-----------------------------------------------------------+
|                            | ``quality_treatment_with_prinseq_n_percentage``           |
+----------------------------+-----------------------------------------------------------+
|                            | Null (No treatment)                                       |
| N number                   +-----------------------------------------------------------+ 
|                            | ``quality_treatment_with_prinseq_n_number``               |
+----------------------------+-----------------------------------------------------------+
|                            | False                                                     |
| Other base filtering       +-----------------------------------------------------------+ 
|                            | ``quality_treatment_with_prinseq_other_base_filter``      |
+----------------------------+-----------------------------------------------------------+


Length related filter treatments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sequences may be eliminated because they are too short or too long. :ref:`More information about why filter sequences by length <for-users-pretreatments-quality-control-treatment-filter>` 


Quality score related filter treatments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`Sequences with low quality must be eliminated <for-users-pretreatments-quality-control-treatment-filter-quality>`. PRINSEQ offers several possibilities for sequence filter based on quality:

- Filter sequences in which at least one base has a quality below/above a threshold
- Filter sequences in which the mean quality score of the sequence is below/above a threshold

GC content related filter treatments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`When the GC content distribution is not bi-modal, it may be interesting to remove sequences based on their GC content <for-users-pretreatments-quality-control-treatment-filter-GC>`. To do that in PRINSEQ, sequences may be filtered if their GC content is below/above a given threshold.

Ambiguity code related filter treatments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`To limite bias in downstream analysis <for-users-pretreatments-quality-control-treatment-filter-ambiguity>`, PRINSEQ allow to eliminate sequences with a high percentage/number of N bases and/or other bases. 

Trimming treatments
-------------------

By default in ASaiM framework, the values for the trimming treatments are:

+------------------------------+-----------------------------------------------------------+
|                              | Default threshold and variable name in configuration file | 
+==============================+===========================================================+
|                              | Null (No treatment)                                       |
| Trimming length              +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_to_length``         |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Left trimming position       +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_left``              |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Right trimming position      +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_right``             |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Left trimming percentage     +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_left_percentage``   |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Right trimming percentage    +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_right_percentage``  |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Left tail trimming           +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_tail_left``         |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Right tail trimming          +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_tail_right``        |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Left N base trimming         +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_ns_left``           |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Right N base trimming        +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_ns_right``          |
+------------------------------+-----------------------------------------------------------+
|                              | Null (No treatment)                                       |
| Left quality trimming        +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_qual_left``         |
+------------------------------+-----------------------------------------------------------+
|                              | 20                                                        |
| Right quality trimming       +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_qual_right``        |
+------------------------------+-----------------------------------------------------------+
|                              | mean                                                      |
| Type of quality estimation   +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_qual_type``         |
+------------------------------+-----------------------------------------------------------+
|                              | lt                                                        |
| Rule of quality estimation   +-----------------------------------------------------------+
|                              | ``quality_treatment_with_prinseq_trim_qual_rule``         |
+------------------------------+-----------------------------------------------------------+
|                              | 5 bp                                                      |
| Window of quality estimation +-----------------------------------------------------------+ 
|                              | ``quality_treatment_with_prinseq_trim_qual_window``       |
+------------------------------+-----------------------------------------------------------+
|                              | 5 bp                                                      |
| Step of quality estimation   +-----------------------------------------------------------+ 
|                              | ``quality_treatment_with_prinseq_trim_qual_step``         |
+------------------------------+-----------------------------------------------------------+

Trim by length/position
~~~~~~~~~~~~~~~~~~~~~~~

:ref:`To eliminate bases at sequence end <for-users-pretreatments-quality-control-treatment-trim-length-pos>`, PRINSEQ offer the possibility to trim sequences to a specific length or a fixed number of nucleotidesfrom either end. 

Trim tails
~~~~~~~~~~

:ref:`Another possibility of trimming is to trim tails (poly A/T or N) <for-users-pretreatments-quality-control-treatment-trim-tails>`. In PRINSEQ, this is specified by giving the minimum tail length to trim. 

Trim ends by quality scores
~~~~~~~~~~~~~~~~~~~~~~~~~~~ 

:ref:`As the quality sequence decrease the sequence length, the sequence quality may be improved by trimming the ends <for-users-pretreatments-quality-control-treatment-trim-ends>`. For this trimming in PRINSEQ, different rules must be specified:

- The quality threshold on the left and right of the sequences
- The type of quality estimation (mean, min, max, ...)
- The rule (lower, greater, ...)
- The window or base number on which the quality is estimated
- The step of window sliding

.. rubric:: References

.. bibliography:: ../../../../references.bib
   :cited:
   :style: plain
   :filter: docname in docnames

       