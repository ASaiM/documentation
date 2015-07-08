.. _for-devs-pretreatments-quality-control-estimation:

Quality estimation
##################

To estimate sequence quality and treatments to do, many indicators can be checked:

- :ref:`Sequence length <for-users-pretreatments-quality-control-estimation-length>`
- :ref:`Base quality <for-users-pretreatments-quality-control-estimation-quality>`
- :ref:`Base content <for-users-pretreatments-quality-control-estimation-base-content>`
- :ref:`Sequence duplication <for-users-pretreatments-quality-control-estimation-seq-duplication>`
- :ref:`Sequence complexity <for-users-pretreatments-quality-control-estimation-seq-complexity>`
- :ref:`Tag sequence <for-users-pretreatments-quality-control-estimation-tag-sequences>`
- :ref:`Sequence contamination <for-users-pretreatments-quality-control-estimation-seq-contamination>`

Several tools can be used to estimate these indicators. Currently only :ref:`FastQC <for-devs-pretreatments-quality-control-estimation-fastqc>` is available in ASaiM framework.

.. _for-devs-pretreatments-quality-control-estimation-fastqc:
FastQC
======

.. note::

    Input: sequence file with quality values for each base

    Output: report 

`FastQC <http://www.bioinformatics.babraham.ac.uk/projects/fastqc/>`_ is used to generate quality graphics and estimate numerous quality informations and threshold. This tool generates of a report with several graphics. For each studied indicators, FastQC providing a quick overview to tell in which areas there may be problems. 

The thresholds of warning and error raising of each indicators are adjustable. By default in ASaiM framework, the values are:

+------------------------------------------------+-----------------------------------------------------------+
|                                                | Default threshold and variable name in configuration file | 
+======================================+=========+===========================================================+
|                                      | Warning | < 1 bp                                                    |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_sequence_length_warn``   | 
| Sequence length                      +---------+-----------------------------------------------------------+
|                                      | Error   | < 1 bp                                                    |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_sequence_length_error``  |
+--------------------------------------+---------+-----------------------------------------------------------+
| Per sequence quality score           | Warning | < 27                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_sequence_warn``          | 
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | < 20                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_sequence_error``         |
+--------------------------------------+---------+-----------------------------------------------------------+
| Lower per base quality score         | Warning | < 10                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_base_lower_warn``        |
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | < 5                                                       |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_base_lower_error``       |
+--------------------------------------+---------+-----------------------------------------------------------+
| Median per base quality score        | Warning | < 25                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_base_median_warn``       |
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | < 20                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_base_median_error``      |
+--------------------------------------+---------+-----------------------------------------------------------+
| Per tile quality score               | Warning | < 5                                                       |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_tile_warn``              |
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | < 10                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_tile_error``             |
+--------------------------------------+---------+-----------------------------------------------------------+
| Per sequence GC content              | Warning | > 15%                                                     |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_gc_content_warn``        |
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | > 30%                                                     |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_gc_content_error``       |
+--------------------------------------+---------+-----------------------------------------------------------+
| Difference per base sequence content | Warning | > 10%                                                     |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_sequence_content_warn``  |
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | > 20%                                                     |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_sequence_content_error`` |
+--------------------------------------+---------+-----------------------------------------------------------+
| N content                            | Warning | > 5%                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_n_content_warn``         |
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | > 20%                                                     |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_n_content_error``        |
+--------------------------------------+---------+-----------------------------------------------------------+
| Adapter content                      | Warning | > 5%                                                      |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_adapter_warn``           |
|                                      +---------+-----------------------------------------------------------+
|                                      | Error   | > 10%                                                     |
|                                      |         +-----------------------------------------------------------+
|                                      |         | ``quality_estimation_with_fastqc_adapter_error``          |
+--------------------------------------+---------+-----------------------------------------------------------+



Explanation of the generated report
-----------------------------------

Length of sequences
~~~~~~~~~~~~~~~~~~~

FastQC generates a graph showing the distribution of fragment sizes in the file which was analysed. 
In many cases this will produce a simple graph showing a peak only at one size, but for variable length FastQ files this will show the relative amounts of each different size of sequence fragment. 

This module will raise a warning if all sequences are not the same length. This module will raise an error if any of the sequences have zero length. 

For some sequencing platforms it is entirely normal to have different read lengths so warnings here can be ignored.

Base qualities
~~~~~~~~~~~~~~

In the report, there is 3 graphs to check on base qualities:

    Per sequence quality score
        The per sequence quality score report shows the distribution of sequence mean quality score of the dataset. Warning and error are raised if the most frequently observed mean quality is below defined thresholds. Errors here usually indicate a general loss of quality within a run. For long runs this may be alleviated through quality trimming. If a bi-modal, or complex distribution is seen then the results should be evaluated in concert with the per-tile qualities (if available) since this might indicate the reason for the loss in quality of a subset of sequences. 

    Per base sequence quality
        This plot shows an overview of the range of quality values across all bases at each position in the file. For each position, a BoxWhisker type plot is drawn. The elements of the plot are as follows:

            - The central red line is the median value 
            - The yellow box represents the inter-quartile range (25-75%)
            - The upper and lower whiskers represent the 10% and 90% points
            - The blue line represents the mean quality

        The y-axis on the graph shows the quality scores. The higher the score the better the base call. The background of the graph divides the y axis into very good quality calls (green), calls of reasonable quality (orange), and calls of poor quality (red). The quality of calls on most platforms will degrade as the run progresses, so it is common to see base calls falling into the orange area towards the end of a read. 

        Warning and error are issued if the lower quartile for any base is less than a defined threshold, or if the median for any base is less than a defined threshold.


    Per tile sequence quality
        This graph will only appear with Illumina library which retains its original sequence identifiers. The graph allows to look at the quality scores from each tile across all bases to see if there was a loss in quality associated with only one part of the flowcell. 
        The plot shows the deviation from the average quality for each tile. The colours are on a cold to hot scale, with cold colours being positions where the quality was at or below the average for that base in the run, and hotter colours indicate that a tile had worse qualities than other tiles for that base. In the example below you can see that certain tiles show consistently poor quality. A good plot should be blue all over. 
         
        Reasons for seeing warnings or errors on this plot could be transient problems such as bubbles going through the flowcell, or they could be more permanent problems such as smudges on the flowcell or debris inside the flowcell lane. 

        Warning and error are issued if any tile shows a mean Phred score more than certain value less than the mean for that base across all tiles.


Base content
~~~~~~~~~~~~

To check at base content, 3 graphs must be studied:

    Per sequence GC content
        The GC content is mesured across the whole length of each sequence in a file and compared to a modelled normal distribution of GC content. 
        In a normal random library you would expect to see a roughly normal distribution of GC content where the central peak corresponds to the overall GC content of the underlying genome. Since GC content is unknown, the modal GC content is calculated from the observed data and used to build a reference distribution. 
    
        Warning and error are raised if the sum of the deviations from the normal distribution represents more than a defined percentage.

    Per base sequence content
        In per Base Sequence Content plot, FastQC plots out the proportion of each base position in a file for which each of the four normal DNA bases has been called.  Warning and error are issued if the difference between A and T, or G and C is greater than a defined percentage.

    Ambiguous bases or Per base N content
        A high number of Ns can be a sign for a low quality sequence or even dataset. FastQC plots out the percentage of base calls at each position for which an N was called. Warning and error are raised if any position shows an N content of (>5%, by default). This module will raise an error if any position shows an N content of (>20%, by default).

Sequence duplication
~~~~~~~~~~~~~~~~~~~~

As :ref:`mentioned previously <for-users-pretreatments-quality-control-estimation-seq-duplication>`, investigating sequence duplication in metagenomic and metatranscriptomic datasets is a delicate step. So, the corresponding reports are ignored.

Tag sequences
~~~~~~~~~~~~~

To investigate tag or adapter content, FastQC generates a plot showing a cumulative percentage count of the proportion of the library which has seen each of the adapter sequences at each position. Once a sequence has been seen in a read it is counted as being present right through to the end of the read so the percentages you see will only increase as the read length goes on. 

Warning and error are issued if any sequence is present in more than a defined percentage of all reads.
