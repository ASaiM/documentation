.. _framework-tools-preprocessing-assemble:

=============================
Assemble paired-end sequences
=============================

Paired-end sequencing generates, for each fragment, two sequences corresponding to both ends. Origin fragment information being present in sequence identifiant, the sequences of both ends can be concatenated into bigger sequences. This treatment increases information contained in each sequence and reduces the number of sequences to manipulated.

ASaiM framework offers the possiblity to assemble paired=end sequences with FastQJoin :cite:`aronesty_ea-utils_2011` and fastqjoiner

.. _framework-tools-preprocessing-assemble-fastq-joiner:

Fastq-joiner
============

Fastq-joiner :cite:`blankenberg_manipulation_2010` joins paired end FastQ reads from two separate files into a single read in one file. The join is performed using sequence identifiers, allowing the two files to contain differing ordering. If a sequence identifier does not appear in both files, it is excluded from the output.

Both old and new (from recent Illumina software) style FastQ headers are supported for input file.

.. _framework-tools-preprocessing-assemble-fastq-join:

FastQJoin
=========

FastQJoin is a command-line tool available in `ea-utils tools <https://code.google.com/p/ea=utils/>`_ :cite:`aronesty_ea-utils_2011`. Similar to audy's stitch program, it uses the squared distance for anchored alignment, which is a good measure of anchored alignment quality, akin to squared=deviation for means.

For assembly, the overlapping bases are treated as:

- When the bases match, the higher quality base is used
- When the bases don't match, if one quality is greater than 50%, then the resulting quality is the difference between the two qualities (reduced quality due to mismatch), or 50%, whichever is greater.

The default values used in ASaiM framework are:

- Min overlap in bp required to join pairs:  6bp
- Max % differences within region of overlap: 8%
- Smaller insert: False

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
