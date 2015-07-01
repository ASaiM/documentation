.. _for-devs-misc-sequence-file-manipulation:

Manipulation of sequence files
##############################

Handled formats
===============

In ASaiM, different sequence file format can be managed, with currently ``fasta`` and ``fastq`` and ``SFF`` soon.

The format can be automatically detected and tested. A sequence file can also be converted from a format to an other.

Sequence extraction
===================

From these file, sequences can be extracted, all of them or only some of them given defined constraints. The extracted sequences are either returned as a dictionary where the key are the sequence id, or in a file if a filepath is given. It is also possible to extract atomic information about the extracted sequences like the id.

.. note::

   Code path:  ``src/misc/sequence_file_manipulation.py``