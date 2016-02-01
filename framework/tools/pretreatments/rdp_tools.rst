.. _framework-tools-available-pretreatments-frameshift:

================================================
Correct frameshift and classify nearest neighbor
================================================

Principle
#########

Tool
####

Framebot of RDPTools
********************

RDP Tools

RDP FrameBot :cite:`wang_ecological_2013` is a frameshift correction and nearest neighbor classification tool for use with high-throughput amplicon sequencing. It uses a dynamic programming algorithm to align each query DNA sequence against a set of target protein sequences, produces frameshift-corrected protein and DNA sequences and an optimal global or local protein alignment. More information on Github repository.

Input
=====

One protein reference fasta file or index file, and one DNA query fasta file are required.

Several reference sets for a list of genes are available. But personal own set of reference sequences can be provide as representative of the gene of interest (http://fungene.cme.msu.edu is a good resource). The reference set must contain protein or DNA representative sequences of the gene target and should be compiled to have a good coverage of diversity of the gene family. FrameBot is significantly more accurate when the nearest target protein sequence (from the reference set) is at least 50% identical to the query read. Running FrameBot is computationally intensive in no-metric-search mode because it performs all-against-all comparisons between query DNA and the target protein sequences. Therefore we recommend limiting your reference set to 200 protein sequences for no-metric-search mode. The index metic-search mode gains more than 10-fold speedup by reducing the number of comparisons (see FrameBot citation). A larger DNA reference set can be used.

Parameters
==========

The parameters are numerous in Framebot

The alignment mode: glocal, local or global
The minimum abundance for de-novo mode
The maxmimum aa identity cutoff for de-novo mode
The Percent identity cutoff
The top k closest protein targets
Length cutoff in number of amino acids
Disable metric search (provide fasta file of seeds instead of index file)
Result file name stem
Disable the pre-filtering step for non-metric search
Sequence quality data
Protein translation table to use
The word size used to find closest protein targets


Output
=======

The framebot step produces five output files:

the alignment to the nearest match satisfying the minimum length and protein identity cutoff.
the frameshift-corrected nucleotide and protein sequences satisfying the minimum length and protein identity cutoff.
the alignment to the nearest match that failed the minimum length and protein identity cutoff.
a fasta file containing the nucleotide sequences that failed the minimum length and protein identity cutoff.

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames