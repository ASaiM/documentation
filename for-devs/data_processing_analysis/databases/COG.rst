.. _for-devs-databases-COG:

COG
###

Data container

Change for gene families from KEGG to COG definition
====================================================

Use of KEGG - COG correspondence given in HUMAnN data --> Need to have something more reliable, maybe?

Change in file with correspondence between module/pathway and gene families : use of COG gene family names instead of KEGG one

Ok with pathway

Issue with modules and sub-modules: 

expression: K
          | -K
          | expression ',' expression
          | expression '\t' expression
          | expression '-' expression
          | expression '+' expression
          | ( expression )

normally replacement of K by the corresponding COG
issue when no K > COG correspondence
what to do?

multiple cases : 

- K 
- -K
- expression ',' expression
- expression '\t' expression
- expression '-' expression
- expression '+' expression
- ( expression )