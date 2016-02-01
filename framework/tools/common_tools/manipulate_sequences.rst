.. _framework=tools=available=common=manipulate=sequences:

=========================
Manipulate sequence files
=========================

Filter sequences by ID from a tabular file
##########################################

By default it divides a FASTA, FASTQ or Standard Flowgram Format (SFF) file in two, those sequences with or without an ID present in the tabular file column(s) specified. You can opt to have a single output file of just the matching records, or just the non=matching ones.

Instead of providing the identifiers in a tabular file, you can alternatively provide them as a parameter (type or paste them into the text box). This is a useful shortcut for extracting a few sequences of interest without first having to prepare a tabular file.

Note that the order of sequences in the original sequence file is preserved, as is any Roche XML Manifest in an SFF file. Also, if any sequences share an identifier (which would be very unusual in SFF files), duplicates are not removed.

This tool was developed for Peter J.A. Cock, Björn A. Grüning, Konrad Paszkiewicz and Leighton Pritchard (2013). Galaxy tools and workflows for sequence analysis with applications in molecular plant pathology. PeerJ 1:e167 http://dx.doi.org/10.7717/peerj.167 and rely on :cite:`cock_ncbi_2015`.

Example Usage
*************

You may have performed some kind of contamination search, for example running BLASTN against a database of cloning vectors or bacteria, giving you a tabular file containing read identifiers. You could use this tool to extract only the reads without BLAST matches (i.e. those which do not match your contaminant database).

You may have a file of FASTA sequences which has been used with some analysis tool giving tabular output, which has then been filtered on some criteria. You can then use this tool to divide the original FASTA file into those entries matching or not matching your criteria (those with or without their identifier in the filtered tabular file).

Rename sequences with ID mapping from a tabular file
####################################################

Takes a FASTA, QUAL, FASTQ or Standard Flowgram Format (SFF) file and produces a new sequence file (of the same format) where the sequence identifiers have been renamed according to the specified columns in your tabular file.

WARNING: If you have any duplicates in the input sequence file, you will still have duplicate sequences in the output.

WARNING: If the tabular file has more than one new name for any old ID, the last one is used.

This tool was developed for Peter J.A. Cock, Björn A. Grüning, Konrad Paszkiewicz and Leighton Pritchard (2013). Galaxy tools and workflows for sequence analysis with applications in molecular plant pathology. PeerJ 1:e167 http://dx.doi.org/10.7717/peerj.167 and rely on :cite:`cock_ncbi_2015`.

Select sequences by ID from a tabular file
##########################################

Takes a FASTA, QUAL, FASTQ or Standard Flowgram Format (SFF) file and produces a new sequence file (of the same format) containing only the records with identifiers in the tabular file (in the order from the tabular file).

WARNING: If you have any duplicates in the tabular file identifiers, you will get duplicate sequences in the output.

This tool was developed for Peter J.A. Cock, Björn A. Grüning, Konrad Paszkiewicz and Leighton Pritchard (2013). Galaxy tools and workflows for sequence analysis with applications in molecular plant pathology. PeerJ 1:e167 http://dx.doi.org/10.7717/peerj.167 and rely on :cite:`cock_ncbi_2015`.

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

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames