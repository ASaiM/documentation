.. _framework-tools-available-seq-prep-vsearch:

=============
Vsearch tools 
=============

VSearch :cite:`rognes_vsearch:_2015` is an open-source alternative to `USEARCH <http://www.drive5.com/usearch/>`_. :cite:`edgar_search_2010`.

Alignment
=========

Pairwise alignments of all sequences.

Dereplication
=============

Merge strictly identical sequences contained in filename. Identical sequences are defined as having the same length and the same string of nucleotides (case insensitive, T and U are considered the same).

Sorting
=======

Fasta entries are sorted by decreasing abundance or sequence length . To obtain a stable sorting order, ties are sorted by decreasing abundance and label increasing alpha-numerical order, or just by label increasing alpha-numerical order. Label sorting assumes that all sequences have unique labels. The same applies to the automatic sorting performed during chimera checking, derepli- cation, and clustering.

Masking
=======

An input sequence can be composed of lower- or uppercase nucleotides. Lowercase nucleotides are silently set to uppercase before masking, unless the −−qmask soft option is used. Here are the results of combined masking options −−qmask (or −−dbmask for database sequences) and −−hardmask, assuming each input sequences contains both lower and uppercase nucleotides:

===== ======== ================================================
qmask hardmask action
===== ======== ================================================
none  off      no masking, all symbols uppercased
none  on       no masking, all symbols uppercased
dust  off      masked symbols lowercased, others uppercased
dust  on       masked symbols changed to Ns, others uppercased
soft  off      lowercase symbols masked, no case changes
soft  on       lowercase symbols masked and changed to Ns
===== ======== ================================================

Search
======

Sequence search based on vsearch.


========= ================
Key       Description
========= ================
aln       Print a string of M (match), D (delete, i.e. a gap in the query) and I (insert, i.e. a gap in the target) representing the pairwise alignment. Empty field if there is no alignment.
alnlen    Print the length of the query-target alignment (number of columns). The field is set to 0 if there is no alignment.
bits      Bit score (not computed for nucleotide alignments). Always set to 0.
caln      Compact representation of the pairwise alignment using the CIGAR format (Compact Idiosyncratic Gapped Alignment Report): M (match), D (deletion) and I (insertion). Empty field if there is no alignment.
evalue    E-value (not computed for nucleotide alignments). Always set to -1.
exts      Number of columns containing a gap extension (zero or positive integer value).
gaps      Number of columns containing a gap (zero or positive integer value).
id        Percentage of identity (real value ranging from 0.0 to 100.0). The percentage identity is defined as 100 * (matching columns) / (alignment length - terminal gaps).
id0       CD-HIT definition of the percentage of identity (real value ranging from 0.0 to 100.0) using the length of the shortest sequence in the pairwise alignment as denominator: 100 * (matching columns) / (shortest sequence length).
id1       The percentage of identity (real value ranging from 0.0 to 100.0) is defined as the edit distance: 100 * (matching columns) / (alignment length).
id2       The percentage of identity (real value ranging from 0.0 to 100.0) is defined as the edit distance, excluding terminal gaps. The field id2 is an alias for the field id.
id3       Marine Biological Lab definition of the percentage of identity (real value ranging from 0.0 to 100.0), counting each extended gap (internal or terminal) as a single difference and using the length of the longest sequence in the pairwise alignment as denominator: 100 * (1.0 - [(mismatches + gaps) / (longest sequence length)]).
id4       BLAST definition of the percentage of identity (real value ranging from 0.0 to 100.0), equivalent to −−iddef 2 in a context of global pairwise alignment.
ids       Number of matches in the alignment (zero or positive integer value).
mism      Number of mismatches in the alignment (zero or positive integer value).
opens     Number of columns containing a gap opening (zero or positive integer value).
pairs     Number of columns containing only nucleotides. That value corresponds to the length of the alignment minus the gap-containing columns (zero or positive integer value).
pctgaps   Number of columns containing gaps expressed as a percentage of the alignment length (real value ranging from 0.0 to 100.0).
pctpv     Percentage of positive columns. When working with nucleotide sequences, this is equivalent to the percentage of matches (real value ranging from 0.0 to 100.0).
pv        Number of positive columns. When working with nucleotide sequences, this is equivalent to the number of matches (zero or positive integer value).
qcov      Fraction of the query sequence that is aligned with the target sequence (real value ranging from 0.0 to 100.0). The query coverage is computed as 100.0 * (matches + mismatches) / query sequence length. Internal or terminal gaps are not taken into account. The field is set to 0.0 if there is no alignment.
qframe    Query frame (-3 to +3). That field only concerns coding sequences and is not computed by vsearch. Always set to +0.
qhi       Last nucleotide of the query aligned with the target. Always equal to the length of the pairwise alignment. The field is set to 0 if there is no alignment.
qihi      Last nucleotide of the query aligned with the target (ignoring terminal gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
qilo      First nucleotide of the query aligned with the target (ignoring initial gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
ql        Query sequence length (positive integer value). The field is set to 0 if there is no alignment.
qlo       First nucleotide of the query aligned with the target. Always equal to 1 if there is an alignment, 0 otherwise.
qrow      Print the sequence of the query segment as seen in the pairwise alignment (i.e. with gap insertions if need be). Empty field if there is no alignment.
qs        Query segment length. Always equal to query sequence length.
qstrand   Query strand orientation (+ or - for nucleotide sequences). Empty field if there is no alignment.
query     Query label.
raw       Raw alignment score (negative, null or positive integer value). The score is the sum of match rewards minus mismatch penalties, gap openings and gap extensions. The field is set to 0 if there is no alignment.
target    Target label. The field is set to "*" if there is no alignment.
tcov      Fraction of the target sequence that is aligned with the query sequence (real value rang-ing from 0.0 to 100.0). The target coverage is computed as 100.0 * (matches + mis-matches) / target sequence length. Internal or terminal gaps are not taken into account. The field is set to 0.0 if there is no alignment.
tframe    Target frame (-3 to +3). That field only concerns coding sequences and is not computed by vsearch. Always set to +0.
thi       Last nucleotide of the target aligned with the query. Always equal to the length of the pairwise alignment. The field is set to 0 if there is no alignment.
tihi      Last nucleotide of the target aligned with the query (ignoring terminal gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
tilo      First nucleotide of the target aligned with the query (ignoring initial gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
tl        Target sequence length (positive integer value). The field is set to 0 if there is no alignment.
tlo       First nucleotide of the target aligned with the query. Always equal to 1 if there is an alignment, 0 otherwise.
trow      Print the sequence of the target segment as seen in the pairwise alignment (i.e. with gap insertions if need be). Empty field if there is no alignment.
ts        Target segment length. Always equal to target sequence length. The field is set to 0 if there is no alignment.
tstrand   Target strand orientation (+ or - for nucleotide sequences). Always set to "+", so reverse strand matches have tstrand "+" and qstrand "-". Empty field if there is no alignment.
========= ================


Shuffling
=========

Sequence shuffling to obtain new random sequences.

Chimera detection
=================

Sequence chimera detection based on a different scoring functions.

Clustering
==========

vsearch implements a single-pass, greedy star-clustering algorithm, similar to the algorithms implemented in usearch, DNAclust and sumaclust for example.


.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
