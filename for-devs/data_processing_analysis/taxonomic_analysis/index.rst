.. _for-devs-taxonomic-assignation:

Taxonomic assignation
#####################

Estimation of the threshold
===========================

Simulation for estimating the minimum bit score threshold given the taxonomic level (see Leimena et al 2013)

- phylogenetic and functional assignments at genus level given a confidence level (>80%)
- phylogenetic and functional assignments at family level given a confidence level (>80%)
- reliable function (COG) assignment given a confidence level (>95%)

Classification/bining
=====================

Blast? MegaBLAST? MetaPhIAN ? KRAKEN (taxonomic sequence classification system, faster but accurate?)?

2 iterative steps for BLASTN searches to reduce the computational workload

- MegaBLAST (default word size? 28?) for an initial exact match
- BLASTN (more sensitive but slower) of unaligned reads and reads with a bit scores below a threshold (74??) for an initial exact match (word size? 11?)

Classification  

- Gene assigned reads : Reads with at least 50% of the alignment length located within the predicted ORF of a gene
- Intergenic reads : others

Significant gene expression identification was determined by ranking the genes based on the number of reads that were assigned to the gene, followed by selecting the top ranking genes that captures 95% of the assigned mRNA reads

Databases?

Numerous matches that require some heuristic post-processing analysis to assign the sequence read to a species

MetaPhlAn
---------

MetaPhlAn is a computational tool for profiling the composition of microbial communities from metagenomic shotgun sequencing data. MetaPhlAn relies on unique clade-specific marker genes identified from 3,000 reference genomes, allowing:

- orders of magnitude speedups compared to existing methods;
- unambiguous taxonomic assignments;
- accurate estimation of organismal relative abundance;
- species-level resolution for bacterial and archaeal organisms.

Options:

- Type of analysis to perform (relative abundance, by default)

  - profiling a metagenomes in terms of relative abundances
  - mapping from reads to clades (only reads hitting a marker)
  - normalized marker counts for clades with at least a non-null marker
  - normalized marker counts (only when > 0.0 and normalized by metagenome size if --nreads is specified)
  - list of markers present in the sample (threshold at 1.0 if not differently specified with --pres_th)

- Taxonomic level for the relative abundance output (all, by default)
  
  - all taxonomic levels
  - kingdoms (Bacteria and Archaea) only
  - phyla only
  - classes only
  - orders only
  - families only
  - genera only
  - species only

-Total number of reads in the original metagenome. It is used only with normalized marker counts analysis type for normalizing the length-normalized counts with the metagenome size as well. No normalization applied if number of reads is not specified
- Threshold for calling a marker present. It is used only with  list of markers present in the sample analysis type
- Database
- Evalue (1e-16, by default)
- Word size for the blasting (NCBI BlastN value (11), by default)
- Minimum total nucleotide length for the markers in a clade for estimating the abundance without considering sub-clade abundances (10000, by default)
- Quantile value for the robust average (0.1, by default)


.. toctree::
   :maxdepth: 2

   