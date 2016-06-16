.. _framework-tools-manipulation-manipulate-bam-sam:

========================
Manipulate BAM/SAM files
========================

These tools are based on `SAMTools <https://github.com/samtools/samtools>`_ :cite:`li_sequence_2009,li_statistical_2011,li_improving_2011`.

.. _framework-tools-available-common-manipulate-bam-sam-reheader:

Copy SAM/BAM header between datasets
####################################

This tool copies header from ``source`` dataset into ``target`` dataset using ``samtools reheader`` command.

.. _framework-tools-manipulation-manipulate-bam-sam-rmdup:

Remove PCR duplicates
#####################

This tool removes potential PCR duplicates. If multiple read pairs have identical external coordinates, it only retains the pair with highest mapping quality. In the paired-end mode, this command only works with FR orientation and requires ISIZE is correctly set. It does not work for unpaired reads (e.g. two ends mapped to different chromosomes or orphan reads)

.. _framework-tools-manipulation-manipulate-bam-sam-slice:

Slice BAM by genomic regions
############################

This tool allows to restrict (slice) input BAM dataset to a list of intervals defined in a BED file, individual chromosomes, or manually set list of coordinates. This tool is based on ``samtools view`` command.

.. _framework-tools-manipulation-manipulate-bam-sam-calmd:

Recalculate MD/NM tags
######################

This tool generates the MD tag using ``samtools calmd`` command. If the MD tag is already present, this command will give a warning if the MD tag generated is different from the existing tag. The output is a BAM file.

From SAM format specification, MD tag is a string for mismatching positions (Regex : ``[0-9]+(([A-Z]|\^[A-Z]+)[0-9]+)*7``) and NM tag an integer which edit distance to the reference, including ambiguous bases but excluding clipping.


.. _framework-tools-manipulation-manipulate-bam-sam-stats:

Generate statistics for BAM dataset
###################################

This tool runs the ``samtools stats`` command

.. _framework-tools-manipulation-manipulate-bam-sam-sam-to-bam:

Convert SAM to BAM
##################

This tool converts SAM dataset into its binary, BAM, representation using ``samtools sort`` and ``samtools view`` commands:

.. code-block:: none

   samtools sort -O bam -o sorted_input.bam [INPUT SAM]
   samtools view -b -h -o -T [REFERENCE GENOME] [OUTPUT BAM] sorted_input.bam


.. _framework-tools-manipulation-manipulate-bam-sam-bedcov:

Calculate read depth for a set of genomic intervals
###################################################

This tool calculates read depth for regions listed in a BED dataset using ``samtools bedcov`` command.

.. _framework-tools-manipulation-manipulate-bam-sam-sort:

Sort BAM dataset
################

This tool uses ``samtools sort`` command to sort BAM datasets in coordinate or read name order.

.. _framework-tools-manipulation-manipulate-bam-sam-flagstat:

Tabulate descriptive stats for BAM dataset
##########################################

This tool uses ``samtools flagstat`` command to print descriptive information for a BAM dataset. Here is an example of such information:

.. code-block:: none

    200 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 secondary
    0 + 0 supplementary
    0 + 0 duplicates
    25 + 0 mapped (12.50%:nan%)
    200 + 0 paired in sequencing
    100 + 0 read1
    100 + 0 read2
    0 + 0 properly paired (0.00%:nan%)
    0 + 0 with itself and mate mapped
    25 + 0 singletons (12.50%:nan%)
    0 + 0 with mate mapped to a different chr
    0 + 0 with mate mapped to a different chr (mapQ>=5)

.. _framework-tools-manipulation-manipulate-bam-sam-bam-to-sam:

Convert BAM to SAM
##################

This tools converts BAM dataset to SAM using ``samtools view`` command:

.. _framework-tools-manipulation-manipulate-bam-sam-split:

Split BAM dataset on readgroups
###############################

This tool splits BAM files on readgroups. It is based on ``samtools split`` command and generates multiple output datasets for each redagroup from the input dataset.

.. _framework-tools-manipulation-manipulate-bam-sam-idxstats:

Tabulate mapping statistics for BAM dataset
###########################################

This tool runs the ``samtools idxstats`` command. It retrieves and prints stats in the index file.

Input is a sorted and indexed BAM file, the output is tabular with four columns (one row per reference sequence plus a final line for unmapped reads):

.. code-block:: none

    Column Description
    ------ -----------------------------
         1 Reference sequence identifier
         2 Reference sequence length
         3 Number of mapped reads
         4 Number of placed but unmapped reads
              (typically unmapped partners of mapped reads)

.. _framework-tools-manipulation-manipulate-bam-sam-mpileup:

Call variants
#############

This tool report variants for one or multiple BAM files. Alignment records are grouped by sample identifiers in ``@RG`` header lines. If sample identifiers are absent, each input file is regarded as one sample.


.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
