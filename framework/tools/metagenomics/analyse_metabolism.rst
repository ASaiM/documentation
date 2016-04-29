.. _framework-tools-available-functional-assignation-metabolism:

==================
Analyse metabolism
==================

Principle
#########

Classification of protein function
**********************************

.. 
    COG : BLAST searches against COG database (high e-value, identify the closest matching sequence in "empty" database)

    Enzyme Classification (EC) : BLASTP against a database of 127,478 enzyme proteins annotated by SwissProt (use of a more stringent E-value to reduce the number of false positives that arise when sequence similarity is used for enzyme classification purposes : Hung et al 2010)

    KEGG : KEGG Automatic Annotation Server (default gene-set derived from 25 genomes with 15 additional bacterial genomes?) based on a bi-directional best assignment method

    Relative expression levels

    - Counting the number of reads that were assigned to a particular protein-encoding gene
    - Normalisation : dividing each gene count by the total mRNA read count of each dataset and multiplied by the average of the total mRNA read count across all dataset (Dillies et al 2013)

    Relative abundance of each COG category, EC number, ... derived from the sum of RPKM values for each transcript that maps to the specific category, number, ...

Analysis of pathways and modules
********************************

..
    Construction of metabolic networks as described by Peregrín-Alvarez et al 2009: enzymes (EC numbers) represented as nodes, substrates connecting two enzymes represented as edges in the network et enzyme-substrate relationships inferred from KEGG

    iPath pathway mapping system : mapping the KEGG annotation of the identified protein sequences onto metabolic pathway maps

    Indication of the gene expression levels of the metabolic pathways : log 2 values of the read count of KEGG annotated proteins

    Creation of a global metabolic activity maps and other functional interpretations using reads with alignment bit-scores >= 74

Tools
#####

HUMAnN
******

..
    Alternative approach to infer the functional and metabolic potential of a microbial community metagenome. 
    Determination of the gene families and pathways present or absent within a community, as well as their relative abundances, directly from short sequence reads.

    No need from assembly of metagenomic reads: direct profiling of the metabolic potential of microbial communities as represented by orthologous gene family and pathway abundances.
    The computational methodology incorporates a series of gene- and pathway-level quantification, noise reduction, and smoothing steps in order A) to identify which pathways are present or absent within a metagenomically sequenced community and B) to determine their relative abundances.

    # For each metagenomic sample, HUMAnN recovers the abundances of individual orthologous gene families by counting its reads’ BLAST hits in a weighted manner, normalized by each gene family’s average sequence length.
    # Genes are assigned to pathways using MinPath [22], a maximum parsimony approach to explaining observed genes with available pathways.
    # Pathways unlikely to be present based on the BLAST hits’ approximate organismal profiles are removed in a taxonomic limitation step, which also allows normalization for genes’ average copy number.
    # A biological smoothing or gap filling step is performed, preventing small numbers of apparently absent genes in an otherwise abundant pathway from diminishing its presence due to noise.
    # Finally, HUMAnN assigns each pathway a coverage (presence/absence) score in each sample based on the detection of all of its constituent genes, as well as an abundance score indicating its relative abundance in the sample’s metagenome.

    HUMAnN calibrate to use KEGG. but KEGG has gone commercial --> use of COG : [[Change for gene families from KEGG to COG definition|Change for gene families from KEGG to COG definition...]]

    The process of using HUMAnN with a database other than KEGG (e.g. COG, NOG, etc.) requires:

    - A FASTA file of nucleotide sequences against which the meta'ome is searched, each labeled with a gene ID
    - A file of nucleotide sequence lengths, each labeled with a gene ID 
    - A file of gene-to-OG mappings, generated using protein information in COG database
    - A file of OG-to-pathway mappings, generated using KEGG'K-to-COG mapping found in HUMAnN files. However, with this mapping, 5225 / 8104 KEGG categories were not assigned to COG. Need a more accurate mapping????

    Problem of MinPath used by HUMAnN on MacOSX

    Normalization of COG abundance

    Pathways: unordered sets of orthologous gene families
    Modules: combination of required, optional, or complementary genes

HUMAnN 2
********