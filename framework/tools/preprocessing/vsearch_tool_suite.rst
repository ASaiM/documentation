.. _framework-tools-preprocessing-vsearch:

=============
Vsearch tools
=============

VSearch :cite:`rognes_vsearch:_2015` is an open-source alternative to `USEARCH <http://www.drive5.com/usearch/>`_. :cite:`edgar_search_2010`. Most of following documentation comes from `VSEARCH GitHub repository <https://github.com/torognes/vsearch>`_.


.. _framework-tools-preprocessing-vsearch-alignment:

Alignment
=========

This tool performs pairwise alignments of all sequences.

It uses a 8-way 16-bit SIMD vectorized implementation of the full dynamic programming algorithm (Needleman-Wunsch) for global sequence alignment. It is an adaptation of the method described by Rognes (2011) :cite:`rognes_faster_2011`. Due to the extreme memory requirements of this method when aligning two long sequences (e.g. more than 5000bp long), an alternative algorithm described by Hirschberg (1975) :cite:`` and Myers and Miller (1988) :cite:`myers_optimal_1988` is used when aligning a pair of long sequences. This alternative algorithm uses only a linear amount of memory but is much slower. USEARCH by default uses a heuristic procedure involving seeding, extension and banded dynamic programming. If the ``--fulldp`` option is specified to USEARCH it will also use a full dynamic programming approach, but USEARCH is then considerably slower.

.. _framework-tools-preprocessing-vsearch-dereplication:

Dereplication
=============

This tool merges strictly identical sequences contained in filename. Identical sequences are defined as having the same length and the same string of nucleotides (case insensitive, T and U are considered the same).

.. _framework-tools-preprocessing-vsearch-sorting:

Sorting
=======

With this tool, FastA entries are sorted by decreasing abundance or sequence length. To obtain a stable sorting order, ties are sorted by decreasing abundance and label increasing alpha-numerical order, or just by label increasing alpha-numerical order. Label sorting assumes that all sequences have unique labels. The same applies to the automatic sorting performed during chimera checking, derepli- cation, and clustering.

.. _framework-tools-preprocessing-vsearch-masking:

Masking
=======

This tool masks simple repeats and low-complexity regions in the sequences

By default, it uses an optimized multithreaded re-implementation of the well-known DUST algorithm by Tatusov and Lipman (`source <ftp://ftp.ncbi.nlm.nih.gov/pub/tatusov/dust/version1/src/>`_) to mask simple repeats and low-complexity regions in the sequences before searching and clustering. USEARCH by default uses an undocumented rapid masking method called "fastnucleo" that seems to mask fewer and smaller regions than dust. USEARCH may also be run with the DUST masking method, but the masking then takes something like 30 times longer.

An input sequence can be composed of lower- or uppercase nucleotides. Lowercase nucleotides are silently set to uppercase before masking, unless the ``−−qmask`` soft option is used.

.. _framework-tools-preprocessing-vsearch-search:

Search
======

This tool performs sequence search.

VSearch search algorithm indexes the unique kmers in the database in a way similar to USEARCH, but is currently limited to continuous words (non-spaced seeds) of length 7-15 (the length can be specified with the --wordlength option, default 8). It samples every unique kmer from each query sequence and identifies the number of matching kmers in each database sequence. It then examines the database sequences in order of decreasing number of kmer matches. A full global alignment is computed and those target sequences that satisfy all accept options are retained while the others are rejected. The ``--maxrejects`` and ``--maxaccepts`` options are supported in this process, indicating the maximum number of non-matching and matching target sequences considered, respectively.

The accuracy of VSEARCH searches has been assessed and compared to USEARCH version 7.0.1090. The Rfam 11.0 database was used for the assessment, as described on the USEARCH website. A similar procedure was described in the USEARCH paper using the Rfam 9.1 database.

The database was initially shuffled. Then the first sequence from each of the 2085 Rfam families with at least two members was selected as queries while the rest was used as the database. The ability of VSEARCH and USEARCH to identify another member of the same family as the top hit was measured, and then recall and precision was calculated.

When USEARCH was run without the ``--fulldp`` option, VSEARCH had much better recall than USEARCH, but the precision was lower. The F1-score was considerably higher for VSEARCH. When USEARCH was run with --fulldp, VSEARCH had slightly better recall, precision and F-score than USEARCH.

The recall of VSEARCH was usually about 92.3-93.5% and the precision was usually 93.0-94.1%. When run without the ``--fulldp`` option the recall of USEARCH was usually about 83.0-85.3% while precision was 98.5-99.0%. When run with the ``--fulldp`` option the recall of USEARCH was usually about 92.0-92.8% and the precision was about 92.2-93.0%.

The speed of VSEARCH searches appears to be somewhat faster than USEARCH when USEARCH is run without the ``--fulldp`` option. When USEARCH is run with the ``--fulldp`` option, VSEARCH may be considerable faster, but it depends on the options and sequences used.

For the accuracy assessment searches in Rfam 11.0 with 100 replicates of the query sequences, VSEARCH needed 46 seconds, whereas USEARCH needed 60 seconds without the --fulldp option and 70 seconds with ``--fulldp``. This includes time for loading, masking and indexing the database (about 2 seconds for VSEARCH, 5 seconds for USEARCH). The measurements were made on a Apple MacBook Pro Retina 2013 with four 2.3GHz Intel Core i7 cores (8 virtual cores) using the default number of threads (8).

.. _framework-tools-preprocessing-vsearch-shuffling:

Shuffling
=========

This tool shuffles sequences to obtain new random sequences, in a pseudo-random order.

.. _framework-tools-preprocessing-vsearch-chimera-detection:

Chimera detection
=================

This tool detects sequence chimera using the algorithm described by Edgar et al. (2011) :cite:`edgar_uchime_2011`.

VSEARCH is about 40% faster than USEARCH on de novo chimera detection and about 30% faster on detection against a reference database. In VSEARCH ``uchime_ref`` is multithreaded, while ``uchime_denovo`` is not.

.. _framework-tools-preprocessing-vsearch-clustering:

Clustering
==========

vsearch implements a single-pass, greedy star-clustering algorithm, similar to the algorithms implemented in usearch, DNAclust and sumaclust for example.

The speed of clustering with VSEARCH relative to USEARCH depends on how many threads are used. Running with a single thread VSEARCH currently seems to be 2-4 times slower than with USEARCH, depending on parameters. Clustering has been parallelized with threads in VSEARCH, but clustering does not seem to be parallelized in USEARCH (despite what the name and documentation for ``--cluster_fast`` seems to indicate). Clustering with VSEARCH using 4-8 threads is often faster than USEARCH. The speed of VSEARCH might be further improved with an intra-sequence SIMD-vectorized aligner. Speed also depends on sequence length, and vsearch is relatively slower with longer sequences compared to usearch.


.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
