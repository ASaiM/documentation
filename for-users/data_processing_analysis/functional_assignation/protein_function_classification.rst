.. _for-users-functional-assignation-protein-function-classification:

Classification of protein function
##################################

COG : BLAST searches against COG database (high e-value, identify the closest matching sequence in "empty" database)

Enzyme Classification (EC) : BLASTP against a database of 127,478 enzyme proteins annotated by SwissProt (use of a more stringent E-value to reduce the number of false positives that arise when sequence similarity is used for enzyme classification purposes : Hung et al 2010)

KEGG : KEGG Automatic Annotation Server (default gene-set derived from 25 genomes with 15 additional bacterial genomes?) based on a bi-directional best assignment method

Relative expression levels

- Counting the number of reads that were assigned to a particular protein-encoding gene
- Normalisation : dividing each gene count by the total mRNA read count of each dataset and multiplied by the average of the total mRNA read count across all dataset (Dillies et al 2013)

Relative abundance of each COG category, EC number, ... derived from the sum of RPKM values for each transcript that maps to the specific category, number, ...

Tools
#####

HUMAnN
------



   