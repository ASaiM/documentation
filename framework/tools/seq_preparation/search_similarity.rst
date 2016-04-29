.. _framework-tools-available-seq-prep-search_similarity:

=================
Search similarity
=================

Principle
#########

Tools
#####

Blast
*****

Show BLAST database information from blastdbcmd with NCBI BLAST+ database info 
==============================================================================


Make BLAST database with NCBI BLAST+ makeblastdb 
================================================

Search protein database with protein query sequence(s) with NCBI BLAST+ blastp
==============================================================================

Search translated nucleotide database with protein query sequence(s) with NCBI BLAST+ tblastn 
=============================================================================================

Make profile database with NCBI BLAST+ makeprofiledb 
====================================================

Search nucleotide database with nucleotide query sequence(s) with NCBI BLAST+ blastn 
====================================================================================

Masks low complexity regions with NCBI BLAST+ dustmasker 
========================================================

Search protein database with translated nucleotide query sequence(s) with NCBI BLAST+ blastx  
============================================================================================

Mask low-complexity regions in protein sequences with NCBI BLAST+ segmasker 
===========================================================================

Search translated nucleotide database with translated nucleotide query sequence(s) with NCBI BLAST+ tblastx 
===========================================================================================================

Search protein domain database (PSSMs) with protein query sequence(s) with NCBI BLAST+ rpsblast 
===============================================================================================

Extract sequence(s) from BLAST database with NCBI BLAST+ blastdbcmd entry(s) 
============================================================================

Search protein domain database (PSSMs) with translated nucleotide query sequence(s) with NCBI BLAST+ rpstblastn 
===============================================================================================================

Convert BLAST XML output to tabular with BLAST XML to tabular 
=============================================================

Convert masking information in lower-case masked FASTA input to file formats suitable for makeblastdb with NCBI BLAST+ convert2blastmask 
========================================================================================================================================


Diamond
*******

DIAMOND :cite:`buchfink_fast_2015` is a new alignment tool for aligning short DNA sequencing reads to a protein reference database such as NCBI-NR. On Illumina reads of length 100-150bp, in fast mode, DIAMOND is about 20,000 times faster than BLASTX, while reporting about 80-90% of all matches that BLASTX finds, with an e-value of at most 1e-5. In sensitive mode, DIAMOND ist about 2,500 times faster than BLASTX, finding more than 94% of all matches.

Build database from a FASTA file
================================

Similarity search
=================

Supported values for gap open and gap extend parameters depending on the selected scoring matrix.


Matrix  Supported values for (gap open)/(gap extend)
BLOSUM45    (10-13)/3; (12-16)/2; (16-19)/1
BLOSUM50    (9-13)/3; (12-16)/2; (15-19)/1
BLOSUM62    (6-11)/2; (9-13)/1
BLOSUM80    (6-9)/2; 13/2; 25/2; (9-11)/1
BLOSUM90    (6-9)/2; (9-11)/1
PAM250  (11-15)/3; (13-17)/2; (17-21)/1
PAM70   (6-8)/2; (9-11)/1
PAM30   (5-7)/2; (8-10)/1

Search of Vsearch
*****************

Sequence search based on vsearch.

Parameters: 

- ``aln``: Print a string of M (match), D (delete, i.e. a gap in the query) and I (insert, i.e. a gap in the target) representing the pairwise alignment. Empty field if there is no alignment.
- ``alnlen``: Print the length of the query-target alignment (number of columns). The field is set to 0 if there is no alignment.
- ``bits``: Bit score (not computed for nucleotide alignments). Always set to 0.
- ``caln``: Compact representation of the pairwise alignment using the CIGAR format (Compact Idiosyncratic Gapped Alignment Report): M (match), D (deletion) and I (insertion). Empty field if there is no alignment.
- ``evalue``: E-value (not computed for nucleotide alignments). Always set to -1.
- ``exts``: Number of columns containing a gap extension (zero or positive integer value).
- ``gaps``: Number of columns containing a gap (zero or positive integer value).
- ``id``: Percentage of identity (real value ranging from 0.0 to 100.0). The percentage identity is defined as 100 * (matching columns) / (alignment length - terminal gaps).
- ``id0``: CD-HIT definition of the percentage of identity (real value ranging from 0.0 to 100.0) using the length of the shortest sequence in the pairwise alignment as denominator: 100 * (matching columns) / (shortest sequence length).
- ``id1``: The percentage of identity (real value ranging from 0.0 to 100.0) is defined as the edit distance: 100 * (matching columns) / (alignment length).
- ``id2``: The percentage of identity (real value ranging from 0.0 to 100.0) is defined as the edit distance, excluding terminal gaps. The field id2 is an alias for the field id.
- ``id3``: Marine Biological Lab definition of the percentage of identity (real value ranging from 0.0 to 100.0), counting each extended gap (internal or terminal) as a single difference and using the length of the longest sequence in the pairwise alignment as denominator: 100 * (1.0 - [(mismatches + gaps) / (longest sequence length)]).
- ``id4``: BLAST definition of the percentage of identity (real value ranging from 0.0 to 100.0), equivalent to −−iddef 2 in a context of global pairwise alignment.
- ``ids``: Number of matches in the alignment (zero or positive integer value).
- ``mism``: Number of mismatches in the alignment (zero or positive integer value).
- ``opens``: Number of columns containing a gap opening (zero or positive integer value).
- ``pairs``: Number of columns containing only nucleotides. That value corresponds to the length of the alignment minus the gap-containing columns (zero or positive integer value).
- ``pctgaps``: Number of columns containing gaps expressed as a percentage of the alignment length (real value ranging from 0.0 to 100.0).
- ``pctpv``: Percentage of positive columns. When working with nucleotide sequences, this is equivalent to the percentage of matches (real value ranging from 0.0 to 100.0).
- ``pv``: Number of positive columns. When working with nucleotide sequences, this is equivalent to the number of matches (zero or positive integer value).
- ``qcov``: Fraction of the query sequence that is aligned with the target sequence (real value ranging from 0.0 to 100.0). The query coverage is computed as 100.0 * (matches + mismatches) / query sequence length. Internal or terminal gaps are not taken into account. The field is set to 0.0 if there is no alignment.
- ``qframe``: Query frame (-3 to +3). That field only concerns coding sequences and is not computed by vsearch. Always set to +0.
- ``qhi``: Last nucleotide of the query aligned with the target. Always equal to the length of the pairwise alignment. The field is set to 0 if there is no alignment.
- ``qihi``: Last nucleotide of the query aligned with the target (ignoring terminal gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
- ``qilo``: First nucleotide of the query aligned with the target (ignoring initial gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
- ``ql``: Query sequence length (positive integer value). The field is set to 0 if there is no alignment.
- ``qlo``: First nucleotide of the query aligned with the target. Always equal to 1 if there is an alignment, 0 otherwise.
- ``qrow``: Print the sequence of the query segment as seen in the pairwise alignment (i.e. with gap insertions if need be). Empty field if there is no alignment.
- ``qs``:  Query segment length. Always equal to query sequence length.
- ``qstrand``: Query strand orientation (+ or - for nucleotide sequences). Empty field if there is no alignment.
- ``query``: Query label.
- ``raw``: Raw alignment score (negative, null or positive integer value). The score is the sum of match rewards minus mismatch penalties, gap openings and gap extensions. The field is set to 0 if there is no alignment.
- ``target``: Target label. The field is set to "*" if there is no alignment.
- ``tcov``: Fraction of the target sequence that is aligned with the query sequence (real value rang-ing from 0.0 to 100.0). The target coverage is computed as 100.0 * (matches + mis-matches) / target sequence length. Internal or terminal gaps are not taken into account. The field is set to 0.0 if there is no alignment.
- ``tframe``: Target frame (-3 to +3). That field only concerns coding sequences and is not computed by vsearch. Always set to +0.
- ``thi``: Last nucleotide of the target aligned with the query. Always equal to the length of the pairwise alignment. The field is set to 0 if there is no alignment.
- ``tihi``: Last nucleotide of the target aligned with the query (ignoring terminal gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
- ``tilo``: First nucleotide of the target aligned with the query (ignoring initial gaps). Nucleotide numbering starts from 1. The field is set to 0 if there is no alignment.
- ``tl``: Target sequence length (positive integer value). The field is set to 0 if there is no alignment.
- ``tlo``: First nucleotide of the target aligned with the query. Always equal to 1 if there is an alignment, 0 otherwise.
- ``trow``: Print the sequence of the target segment as seen in the pairwise alignment (i.e. with gap insertions if need be). Empty field if there is no alignment.
- ``ts``: Target segment length. Always equal to target sequence length. The field is set to 0 if there is no alignment.
- ``tstrand``: Target strand orientation (+ or - for nucleotide sequences). Always set to "+", so reverse strand matches have tstrand "+" and qstrand "-". Empty field if there is no alignment.

Searching options
--alnout FILENAME
    filename for human-readable alignment output
--blast6out FILENAME
    filename for blast-like tab-separated output
--db FILENAME   filename for FASTA formatted database for search
--dbmask    mask db with "dust", "soft" or "none" method (dust)
--dbmatched FILENAME
    FASTA file for matching database sequences
--dbnotmatched FILENAME
    FASTA file for non-matching database sequences
--fastapairs FILENAME
    FASTA file with pairs of query and target
--fulldp    full dynamic programming alignment (always on)
--gapext STRING
    penalties for gap extension (2I/1E)
--gapopen STRING
    penalties for gap opening (20I/2E)
--hardmask  mask by replacing with N instead of lower case
--id REAL   reject if identity lower
--iddef INT id definition, 0-4=CD-HIT,all,int,MBL,BLAST (2)
--idprefix INT  reject if first n nucleotides do not match
--idsuffix INT  reject if last n nucleotides do not match
--leftjust  reject if terminal gaps at alignment left end
--match INT score for match (2)
--matched FILENAME
    FASTA file for matching query sequences
--maxaccepts INT
    number of hits to accept and show per strand (1)
--maxdiffs INT  reject if more substitutions or indels
--maxgaps INT   reject if more indels
--maxhits INT   maximum number of hits to show (unlimited)
--maxid REAL    reject if identity higher
--maxqsize INT  reject if query abundance larger
--maxqt REAL    reject if query/target length ratio higher
--maxrejects INT
    number of non-matching hits to consider (32)
--maxsizeratio REAL
    reject if query/target abundance ratio higher
--maxsl REAL    reject if shorter/longer length ratio higher
--maxsubs INT   reject if more substitutions
--mid REAL  reject if percent identity lower, ignoring gaps
--mincols INT   reject if alignment length shorter
--minqt REAL    reject if query/target length ratio lower
--minsizeratio REAL
    reject if query/target abundance ratio lower
--minsl REAL    reject if shorter/longer length ratio lower
--mintsize INT  reject if target abundance lower
--mismatch INT  score for mismatch (-4)
--notmatched FILENAME
    FASTA file for non-matching query sequences
--output_no_hits
    output non-matching queries to output files
--qmask mask query with "dust", "soft" or "none" method (dust)
--query_cov REAL
    reject if fraction of query seq. aligned lower
--rightjust reject if terminal gaps at alignment right end
--rowlen INT    width of alignment lines in alnout output (64)
--self  reject if labels identical
--selfid    reject if sequences identical
--sizeout   write abundance annotation to output
--strand    search "plus" or "both" strands (plus)
--target_cov REAL
    reject if fraction of target seq. aligned lower
--top_hits_only
    output only hits with identity equal to the best
--uc FILENAME   filename for UCLUST-like output
--uc_allhits    show all, not just top hit with uc output
--usearch_global FILENAME
    filename of queries for global alignment search
--userfields STRING
    fields to output in userout file
--userout FILENAME
    filename for user-defined tab-separated output
--weak_id REAL  include aligned hits with >= id; continue search
--wordlength INT
    length of words for database index 3-15 (8)