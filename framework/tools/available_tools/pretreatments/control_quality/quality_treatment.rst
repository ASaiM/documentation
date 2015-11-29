.. _framework-tools-available-pretreatments-control-quality-treatment:

Control treatment 
#################

Principle
=========

Based on :ref:`quality estimations <framework-tools-available-pretreatments-control-quality-estimation>`, sequences must be treated. Better quality generated sequences will limit the bias in downstream analysis.

In general, quality treatments are:

- Elimination of sequences having a mean quality score below the defined threshold
- Quality trimming on sequence ends
- Elimination of sequences having a N content higher than the defined threshold
- Reduction of nucleotide frequency bias
- Removal of adapter sequences
- Removal of reads with smaller than a threshold

The following guide is inspired by recommendations found in PRINSEQ manual. It should ensure that the data used for downstream analysis are not compromised of low-quality sequences, sequence artifacts, or sequence contamination that might lead to erroneous conclusions. However, the user must be aware of each step and parameters and must be free to change them.

There are 2 types of quality treatments: filtering and trimming.

.. _framework-tools-available-pretreatments-control-quality-treatment-filter:

Filter treatments
-----------------

The filter treatments eliminate sequences based on some criteria.

.. _framework-tools-available-pretreatments-control-quality-treatment-filter-length:

Length related
**************

Short sequences can cause problems during, for example, database searches to find similar sequences. Short sequences are more likely to match at a random position by chance than longer sequences and may therefore result in false positive functional or taxonomical assignments. Furthermore, short sequences are likely to be quality trimmed during the signal-processing step and of lower quality with possible sequencing errors. A rule of thumb for sequence length thresholds of longer-read datasets is to filter sequences shorter than 60 bp (20 amino acids).

.. _framework-tools-available-pretreatments-control-quality-treatment-filter-quality:

Quality score related
*********************

Huse et al. :cite:`huse_accuracy_2007` found that sequences with an average score below 25 had more errors than those with higher averages.
Low quality sequences can cause problems during downstream analysis and most assemblers do not take into account quality scores when processing the data. The errors in the reads can complicate the assembly process and might cause misassemblies or make an assembly impossible. Most published thresholds for the sequence mean quality score range from 15 to 25.

.. _framework-tools-available-pretreatments-control-quality-treatment-filter-GC:

GC content related
******************

The GC content distribution of most samples should follow a normal distribution. In some cases, a bi-modal distribution can be observed, especially for metagenomic datasets. This filter is rarely used, but proved useful to separate sequences in a bi-modal distribution.

.. _framework-tools-available-pretreatments-control-quality-treatment-filter-ambiguity:

Ambiguity code related
**********************

A high number of Ns can be a sign for a low quality sequence. Ambiguous bases can cause problems during downstream analysis. Filtering out all reads containing Ns is only suggested if the loss can be afforded (e.g. high coverage datasets or low number of sequences with ambiguous bases). Filtering reads containing more than 1% of ambiguous bases is advised.

.. _framework-tools-available-pretreatments-control-quality-treatment-trim:

Trim options
------------

The trim treatments cut the sequences based on some criteria.

.. _framework-tools-available-pretreatments-control-quality-treatment-trim-length-pos:

Trim by length/position
***********************

To eliminate bases at sequence end, sequences can be trimmed to a specific length or a fixed number of nucleotides can be trimmed from either end. This can be used to eliminate adapters.

.. _framework-tools-available-pretreatments-control-quality-treatment-trim-tails:

Trim tails
**********

Poly-A/T tails can be trimmed from either end specifying a minimum tail length. All repeats of As or Ts with at least this length will be trimmed from the sequence ends. Trimming poly-A/T tails can reduce the number of false positives during database searches, as long tails tend to align well to sequences with low complexity or sequences with poly-A tails in the database.

.. _framework-tools-available-pretreatments-control-quality-treatment-trim-ends:

Trim ends by quality scores
***************************

Sequences can be trimmed from either end using different rules applied to a sliding window. To stop at the first base that fails the rule defined, use a window size of 1. A bigger window size can trim sequences that might contain a high quality score in between low quality scores without stopping at the high quality score. To move the sliding window over all quality scores without missing any, the step size should be less or equal to the window size.

The quality trimming during the signal processing step (see Raw data processing PDF file) may not be sufficient. Trimmed sequences can end with low quality bases or even with ambiguous base N (approx. 1%). Reads with RLMIDs (Rapid library multiplex identifiers) may be trimmed in high quality regions as the default behavior will cause the reads to be trimmed at the first position the MID sequence matches, even if it is not the MID but a natural occurring match inside the read.

The parameters should be set to trim positions with a quality score below 20.

Tools
=====

..
    .. note::

        Input: sequence file with quality values for each base

        Output: quality treated sequence file

PRINSEQ :cite:`schmieder_quality_2011` is a tool for easy and rapid quality control and data preprocessing of metagenomic and metatranscriptomic datasets. This tool allow to process the sequences with :ref:`filtering <for-users-pretreatments-quality-control-treatment-filter>` and :ref:`trimming <for-users-pretreatments-quality-control-treatment-trim>`.


Filter treatments
-----------------

By default in ASaiM framework, the values for the filter treatments are:

+----------------------------+----------------+
|                            | Default values |
+============================+================+
| Minimum sequence length    | 60 bp          |
+----------------------------+----------------+
| Maximum sequence length    | No treatment   |
+----------------------------+----------------+
| Minimum quality score      | No treatment   |
+----------------------------+----------------+
| Maximum quality score      | No treatment   |
+----------------------------+----------------+
| Minimum mean quality score | 15             |
+----------------------------+----------------+
| Maximum mean quality score | No treatment   |
+----------------------------+----------------+
| Minimum GC percentage      | No treatment   |
+----------------------------+----------------+
| Maximum GC percentage      | No treatment   |
+----------------------------+----------------+
| N percentage               | 2              |
+----------------------------+----------------+
| N number                   | No treatment   |
+----------------------------+----------------+
| Other base filtering       | False          |
+----------------------------+----------------+

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

+------------------------------+----------------+
|                              | Default values |
+==============================+================+
| Trimming length              | No treatment   |
+------------------------------+----------------+
| Left trimming position       | No treatment   |
+------------------------------+----------------+
| Right trimming position      | No treatment   |
+------------------------------+----------------+
| Left trimming percentage     | No treatment   |
+------------------------------+----------------+
| Right trimming percentage    | No treatment   |
+------------------------------+----------------+
| Left tail trimming           | No treatment   |
+------------------------------+----------------+
| Right tail trimming          | No treatment   |
+------------------------------+----------------+
| Left N base trimming         | No treatment   |
+------------------------------+----------------+
| Right N base trimming        | No treatment   |
+------------------------------+----------------+
| Left quality trimming        | No treatment   |
+------------------------------+----------------+
| Right quality trimming       | 20             |
+------------------------------+----------------+
| Type of quality estimation   | mean           |
+------------------------------+----------------+
| Rule of quality estimation   | lt             |
+------------------------------+----------------+
| Window of quality estimation | 5 bp           |
+------------------------------+----------------+
| Step of quality estimation   | 5 bp           |
+------------------------------+----------------+

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

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames