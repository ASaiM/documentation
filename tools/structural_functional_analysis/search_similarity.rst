.. _framework-tools-struct-funct-analysis-search:

=================
Search similarity
=================



.. _framework-tools-struct-funct-analysis-search-blast:

NCBI BLAST+
===========

BLAST+ :cite:`camacho_blast+:_2009` is a sequence similarity search program that can be used to quickly search a sequence database for matches to a query sequence. The command line NCBI BLAST+ tool suite was wrapped for use within Galaxy :cite:`cock_ncbi_2015`.

FASTA file corresponding to database have to be :ref:`turned into a database <framework-tools-struct-funct-analysis-search-makeblastdb>` before searching against.


Because Galaxy focuses on processing tabular data, the default output of most of following tool is tabular. The standard BLAST+ tabular output contains 12 columns:

====== ========= ============================================
Column NCBI name Description
------ --------- --------------------------------------------
     1 qseqid    Query Seq-id (ID of your sequence)
     2 sseqid    Subject Seq-id (ID of the database hit)
     3 pident    Percentage of identical matches
     4 length    Alignment length
     5 mismatch  Number of mismatches
     6 gapopen   Number of gap openings
     7 qstart    Start of alignment in query
     8 qend      End of alignment in query
     9 sstart    Start of alignment in subject (database hit)
    10 send      End of alignment in subject (database hit)
    11 evalue    Expectation value (E-value)
    12 bitscore  Bit score
====== ========= ============================================

The BLAST+ tools can optionally output additional columns of information, but this takes longer to calculate. Many commonly used extra columns are included by selecting the extended tabular output. The extra columns are included *after* the standard 12 columns. This is so that you can write workflow filtering steps that accept either the 12 or 25 column tabular BLAST output. Galaxy now uses this extended 25 column output by default.

====== ============= ===========================================
Column NCBI name     Description
------ ------------- -------------------------------------------
    13 sallseqid     All subject Seq-id(s), separated by a ';'
    14 score         Raw score
    15 nident        Number of identical matches
    16 positive      Number of positive-scoring matches
    17 gaps          Total number of gaps
    18 ppos          Percentage of positive-scoring matches
    19 qframe        Query frame
    20 sframe        Subject frame
    21 qseq          Aligned part of query sequence
    22 sseq          Aligned part of subject sequence
    23 qlen          Query sequence length
    24 slen          Subject sequence length
    25 salltitles    All subject title(s), separated by a '&lt;&gt;'
====== ============= ===========================================

The third option is to customise the tabular output by selecting which columns you want, from the standard set of 12, the default set of 25, or any of the additional columns BLAST+ offers (including species name).

The fourth option is BLAST XML output, which is designed to be parsed by another program, and is understood by some Galaxy tools.

You can also choose several plain text or HTML output formats which are designed to be read by a person (not by another program). The HTML versions use basic webpage formatting and can include links to the hits on the NCBI website. The pairwise output (the default on the NCBI BLAST website) shows each match as a pairwise alignment with the query. The two query anchored outputs show a multiple sequence alignment between the query and all the matches, and differ in how insertions are shown (marked as insertions or with gap characters added to the other sequences).


.. _framework-tools-struct-funct-analysis-search-info:

Show database information
-------------------------

This tool calls the NCBI BLAST+ ``blastdbcmd`` command line tool with the ``-info`` switch to give summary information about a BLAST database, such as the size (number of sequences and total length) and date.

.. _framework-tools-struct-funct-analysis-search-makeblastdb:

Make BLAST database
-------------------

This tool make BLAST database from one or more FASTA files and/or BLAST databases.

This is a wrapper for the NCBI BLAST+ tool ``makeblastdb``, which is the replacement for the ``formatdb`` tool in the NCBI legacy BLAST suite.

.. _framework-tools-struct-funct-analysis-search-blastp:

Search protein database with protein query sequence(s)
------------------------------------------------------

This tool searches a protein database using a protein query, using the NCBI BLAST+ ``blastp`` command line tool.

.. _framework-tools-struct-funct-analysis-search-tblastn:

Search translated nucleotide database with protein query sequence(s)
--------------------------------------------------------------------

This tool searches a translated nucleotide database using a protein query, using the NCBI BLAST+ ``tblastn`` command line tool.

.. _framework-tools-struct-funct-analysis-search-makeprofiledb:

Make profile database
---------------------

This tool takes a protein domain profile database (for use with RPS-BLAST or RSP-TBLASTN) from one or more Position Specific Scoring Matrices (PSSM) files in the NCBI `scoremat` ASN.1 format (usually named `*.smp`).

This is a wrapper for the NCBI BLAST+ tool ``makeprofiledb``.

.. _framework-tools-struct-funct-analysis-search-blastn:

Search nucleotide database with nucleotide query sequence(s)
------------------------------------------------------------

This tool searches a nucleotide database using a nucleotide query, using the NCBI BLAST+ ``blastn`` command line tool. Algorithms include ``blastn``, ``megablast``, and discontiguous ``megablast``.

.. _framework-tools-struct-funct-analysis-search-dustmasker:

Mask low complexity regions
---------------------------

This tool identifies and masks out low complexity regions of a nucleotide database (or sequences in FASTA format) by using the symmetric DUST algorithm.

If you select `maskinfo ASN.1` (binary or text) as output format, the output file can be used as masking data for NCBI BLAST+ ``makeblastdb`` tool.

.. _framework-tools-struct-funct-analysis-search-blastx:

Search protein database with translated nucleotide query sequence(s)
--------------------------------------------------------------------

This tool searches a protein database using a translated nucleotide query, using the NCBI BLAST+ ``blastx`` command line tool.

.. _framework-tools-struct-funct-analysis-search-segmasker:

Mask low-complexity regions in protein sequences
------------------------------------------------

This tool identifies and masks out low complexity regions of a protein database (or proteins in FASTA format) by using the SEG algorithm.

If you select `maskinfo ASN.1` (binary or text) as output format, the output file can be used as masking data for NCBI BLAST+ ``makeblastdb`` tool.


.. _framework-tools-struct-funct-analysis-search-tblastx:

Search translated nucleotide database with translated nucleotide query sequence(s)
----------------------------------------------------------------------------------

This tool searches a translated nucleotide database using a translated nucleotide query, using the NCBI BLAST+ ``tblastx`` command line tool.

.. _framework-tools-struct-funct-analysis-search-rpsblast:

Search protein domain database (PSSMs) with protein query sequence(s)
---------------------------------------------------------------------

This tool searches a protein domain database using a protein query, using the NCBI BLAST+ ``rpsblast`` command line tool.

The protein domain databases use position-specific scoring matrices (PSSMs). The exact list of domain databases offered will depend on how your local Galaxy has been configured.

.. _framework-tools-struct-funct-analysis-search-blastdbcmd:

Extract sequence(s) from BLAST database
---------------------------------------

This tool extracts FASTA formatted sequences from a BLAST database using the NCBI BLAST+ ``blastdbcmd`` command line tool.

When a BLAST database is constructed from a FASTA file, the original identifiers can be replaced with BLAST assigned identifiers, partly to ensure uniqueness. e.g. Sometimes a prefix of `lcl|` is added (lcl is short for local), or an arbitrary name starting `gnl|BL_ORD_ID|` is created.

If you are using the tabular output from BLAST, it will contain the original identifiers - not the BLAST assigned identifiers suitable for use with the ``blastdbcmd`` tool.

If you are using the XML or plain text output, this will also contain the BLAST assigned identifiers. However, this means getting a list of BLAST assigned identifiers isn't straightforward.

.. _framework-tools-struct-funct-analysis-search-rpstblastn:

Search protein domain database (PSSMs) with translated nucleotide query sequence(s)
-----------------------------------------------------------------------------------

This tool searches a protein domain database using a nucleotide query, using the NCBI BLAST+ ``rpstblastn`` command line tool.

The protein domain databases use position-specific scoring matrices (PSSMs). The exact list of domain databases offered will depend on how your local Galaxy has been configured.

.. _framework-tools-struct-funct-analysis-search-xml:

Convert BLAST XML output to tabular
-----------------------------------

This tool takes the BLAST XML output and can convert it into the
standard 12 column tabular equivalent:

====== ========= ============================================
Column NCBI name Description
------ --------- --------------------------------------------
     1 qseqid    Query Seq-id (ID of your sequence)
     2 sseqid    Subject Seq-id (ID of the database hit)
     3 pident    Percentage of identical matches
     4 length    Alignment length
     5 mismatch  Number of mismatches
     6 gapopen   Number of gap openings
     7 qstart    Start of alignment in query
     8 qend      End of alignment in query
     9 sstart    Start of alignment in subject (database hit)
    10 send      End of alignment in subject (database hit)
    11 evalue    Expectation value (E-value)
    12 bitscore  Bit score
====== ========= ============================================

The BLAST+ tools can optionally output additional columns of information,
but this takes longer to calculate. Most (but not all) of these columns are
included by selecting the extended tabular output. The extra columns are
included *after* the standard 12 columns. This is so that you can write
workflow filtering steps that accept either the 12 or 25 column tabular
BLAST output. This tool now uses this extended 25 column output by default.

====== ============= ===========================================
Column NCBI name     Description
------ ------------- -------------------------------------------
    13 sallseqid     All subject Seq-id(s), separated by a ';'
    14 score         Raw score
    15 nident        Number of identical matches
    16 positive      Number of positive-scoring matches
    17 gaps          Total number of gaps
    18 ppos          Percentage of positive-scoring matches
    19 qframe        Query frame
    20 sframe        Subject frame
    21 qseq          Aligned part of query sequence
    22 sseq          Aligned part of subject sequence
    23 qlen          Query sequence length
    24 slen          Subject sequence length
    25 salltitles    All subject title(s), separated by a '&lt;&gt;'
====== ============= ===========================================

Beware that the XML file (and thus the conversion) and the tabular output
direct from BLAST+ may differ in the presence of XXXX masking on regions
low complexity (columns 21 and 22), and thus also calculated figures like
the percentage identity (column 3).

.. _framework-tools-struct-funct-analysis-search-convert2blastmask:

Convert masking information to file formats suitable for makeblastdb
--------------------------------------------------------------------

This tool converts masking information in lower-case masked FASTA input to file formats suitable for `makeblastdb`.

.. _framework-tools-struct-funct-analysis-search-diamond:

Diamond
=======

Diamond :cite:`buchfink_fast_2015` is a new alignment tool for aligning short DNA sequencing reads to a protein reference database such as NCBI-NR.

On Illumina reads of length 100-150bp, in fast mode, DIAMOND is about 20,000 times faster than BLASTX, while reporting about 80-90% of all matches that BLASTX finds, with an e-value of at most 1e-5. In sensitive mode, DIAMOND is about 2,500 times faster than BLASTX, finding more than 94% of all matches.

.. _framework-tools-struct-funct-analysis-search-makedb>:

Build database from a FASTA file
--------------------------------

This tool builds Diamond database from a FASTA file.

.. _framework-tools-struct-funct-analysis-search-diamond-alignment:

Alignment tool for short sequences against a protein database
-------------------------------------------------------------

This tool aligns short sequences against a protein database using Diamond algorithm.

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
