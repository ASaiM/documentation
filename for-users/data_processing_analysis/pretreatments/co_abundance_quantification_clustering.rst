.. _for-users-pretreatments-coabundance-quantification-clustering:

Co-abundance quantification and clustering of similar reads
###########################################################

.. warning::
    Not available

Reduction of the complexity (size of each dataset)

Pool of reads with identical sequences into unique reads and estimation of transcript expression
Normalization of each sample transcript expression to account for expression bias due to transcript length --> values of Reads Per Kilobase of transcript per Million reads mapped (RPKM - Mortazavi et al 2008), with formula : 10^9C/NL where C = number of reads that could be mapped in that sample to the specific bacterial transcript, L = the length of the transcript and N = total number of reads that could be mapped to bacterial transcripts in that sample.

Assignation of each transcript to gene family

All-vs-all BLAST search of the unique transcripts identified from all samples (E-value inferior to 10:sup:`-5`
Placement of each transcript into gene family using the Markov clustering algorithm (MCL - van Dongen 2000) with an inflation parameter of 2.6 to place each transcript into one of 13,278 gene families
Computation of the relative expression of each gene family derived from the sum of RPKM values for each transcript associated with that gene family
Co-abundance quantification and clustering of reads with similar abundance
Conservation of abundance informations

Normalization of each sample transcript expression to account for expression bias due to transcript length --> values of Reads Per Kilobase of transcript per Million reads mapped (RPKM - Mortazavi et al 2008).
Formula : 10^9C/NL where C = number of reads that could be mapped in that sample to the specific bacterial transcript, L = the length of the transcript and N = total number of reads that could be mapped to bacterial transcripts in that sample.
