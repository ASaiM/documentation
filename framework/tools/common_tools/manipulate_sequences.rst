.. _framework-tools-available-common-manipulate-sequences:

=========================
Manipulate sequence files
=========================

.. _framework-tools-common-tools-manipulate-sequences-filter:

Filter sequences by ID from a tabular file
##########################################

By default it divides a FASTA, FASTQ or Standard Flowgram Format (SFF) file in two, those sequences with or without an ID present in the tabular file column(s) specified. You can opt to have a single output file of just the matching records, or just the non=matching ones.

Instead of providing the identifiers in a tabular file, you can alternatively provide them as a parameter (type or paste them into the text box). This is a useful shortcut for extracting a few sequences of interest without first having to prepare a tabular file.

Note that the order of sequences in the original sequence file is preserved, as is any Roche XML Manifest in an SFF file. Also, if any sequences share an identifier (which would be very unusual in SFF files), duplicates are not removed.

This tool was developed for :cite:`cock_galaxy_2013`.

You may have performed some kind of contamination search, for example running BLASTN against a database of cloning vectors or bacteria, giving you a tabular file containing read identifiers. You could use this tool to extract only the reads without BLAST matches (i.e. those which do not match your contaminant database).

You may have a file of FASTA sequences which has been used with some analysis tool giving tabular output, which has then been filtered on some criteria. You can then use this tool to divide the original FASTA file into those entries matching or not matching your criteria (those with or without their identifier in the filtered tabular file).

.. _framework-tools-common-tools-manipulate-sequences-rename:

Rename sequences with ID mapping from a tabular file
####################################################

Takes a FASTA, QUAL, FASTQ or Standard Flowgram Format (SFF) file and produces a new sequence file (of the same format) where the sequence identifiers have been renamed according to the specified columns in your tabular file.

.. warning::
  If you have any duplicates in the input sequence file, you will still have duplicate sequences in the output.
  
  If the tabular file has more than one new name for any old ID, the last one is used.

This tool was developed for :cite:`cock_galaxy_2013`.

.. _framework-tools-common-tools-manipulate-sequences-select:

Select sequences by ID from a tabular file
##########################################

Takes a FASTA, QUAL, FASTQ or Standard Flowgram Format (SFF) file and produces a new sequence file (of the same format) containing only the records with identifiers in the tabular file (in the order from the tabular file).

.. warning::
  If you have any duplicates in the tabular file identifiers, you will get duplicate sequences in the output.

This tool was developed for :cite:`cock_galaxy_2013`.

.. _framework-tools-common-tools-manipulate-sequences-fastq-fasta-convert:

FASTQ to FASTA converter
########################

This tool converts data from Solexa format to FASTA format (scroll down for format description).

Example
*******

The following data in Solexa=FASTQ format::

    @CSHL_4_FC042GAMMII_2_1_517_596
    GGTCAATGATGAGTTGGCACTGTAGGCACCATCAAT
    +CSHL_4_FC042GAMMII_2_1_517_596
    40 40 40 40 40 40 40 40 40 40 38 40 40 40 40 40 14 40 40 40 40 40 36 40 13 14 24 24 9 24 9 40 10 10 15 40

Will be converted to FASTA (with 'rename sequence names' # NO)::

    >CSHL_4_FC042GAMMII_2_1_517_596
    GGTCAATGATGAGTTGGCACTGTAGGCACCATCAAT

Will be converted to FASTA (with 'rename sequence names' # YES)::

    >1
    GGTCAATGATGAGTTGGCACTGTAGGCACCATCAAT
    
This tool is based on FASTX=toolkit by Assaf Gordon.

.. _framework-tools-common-tools-manipulate-sequences-fasta-tab-convert:

FASTA-to-Tabular converter
##########################

This tool converts FASTA formatted sequences to TAB-delimited format.

Many tools consider the first word of the FASTA ">" title line to be an identifier, and any remaining text to be a free form description. It is therefore useful to split this text into two columns in Galaxy (identifier and any description) by setting How many columns to divide title string into? to 2. In some cases the description can be usefully broken up into more columns.

The option How many characters to keep? allows to select a specified number of letters from the beginning of each FASTA entry. With the introduction of the How many columns to divide title string into? option this setting is of limited use, but does still allow you to truncate the identifier.

.. _framework-tools-common-tools-manipulate-sequences-split:

Split paired end reads
######################

Splits a single fastq dataset representing paired-end run into two datasets (one for each end). This tool works only for datasets where both ends have the same length.

.. _framework-tools-common-tools-manipulate-sequences-convert:

Convert/ Extract information from a sequence file, with possible constraints
############################################################################

This tool extracts information (sequences, id, length, ...) from sequence files or convert a FastQ file to Fasta file.

Some constraints could be added to extraction/conversion. For example, only sequences with more than 30 bp could be extracted. Or, a sequences whose the identifiant is in a list.

The input is a sequence file in fasta or fastq format. The tool generates different outputs given the chosen parameters.

.. _framework-tools-common-tools-manipulate-sequences-barcodes:

Add barcodes to Fasta sequences
###############################

This tool takes a FASTA file and add at the beginning of each sequence a barcode.

The barcode of each sequence is determined given its sequence identifier. The mapping between sequence identifier and corresponding barcode is defined inside the mapping file. This file must be a tabular delimited file with two columns: the first with sequence identifiers and the second the corresponding barcode.


.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames