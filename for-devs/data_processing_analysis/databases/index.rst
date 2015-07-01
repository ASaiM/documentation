.. _for-devs-databases:

Databases
#########

For the taxonomic and functional assignations, sequence databases are needed. They are downloaded from public repository and loaded into data containers.

RefSeq
======

COG
===

The *Clusters of Orthologous Groups of proteins* (COGs) database is popular tool for functional annotation :cite:`galperin_expanded_2015`. Each COG consists of individual orthologous proteins or orthologous sets of paralogs, which typically have the same function.

The COGs database is downloaded from ftp://ftp.ncbi.nih.gov/pub/COG/COG2014/data and incorporated into a data container. Some treatments are made like extraction of interesting informations into Python dictionary to facilite the query.

KEGG
====

The *Kyoto Encyclopedia of Genes and Genomes* (KEGG) database :cite:`kanehisa_kegg:_2000` is a collection of databases dealing with genomes, biological pathways, diseases, drugs, and chemical substances. According to the developers, KEGG is a "computer representation" of the biological system :cite:`kanehisa_genomics_2006`.

:ref:`HUMAnN <for-devs-functional-assignation-pathway-module-analysis-humann>` uses KEGG database. However, KEGG is now commercial. To get around the use of KEGG but still using HUMAnN, a correspondance between COG gene families and KEGG Orthology is made. 

.. rubric:: References

.. bibliography:: ../../../references.bib
   :cited:
   :style: plain
   :filter: docname in docnames


   

