.. _framework-tutorial-functional-analysis:

Functional analyses
===================

Investigation of sample composition give an insight on "What organisms are present
in our sample". We know what to know "What are they doing in that sample ?".

For this investigation, we need to affiliate sequences to a protein database.
We choose for this task to use `HUMAnN2 <http://huttenhower.sph.harvard.edu/humann2>`_.
HUMAnN profiles the presence/absence and abundance of gene families and microbial 
pathways in a community from metagenomic or metatranscriptomic sequencing data.

HUMAnN2 is available in `Analyze metabolism` (`Functional assignation` section). 
We execute HUMAnN2 on non rRNA sequences:

.. _humann2_param:

.. figure:: /assets/images/framework/tutorial/humann2_param.png

3 output files are generated:

- A file with abundance of found UniRef50 gene families
- A file with coverage of found Metacyc pathways
- A file with abundance of found Metacyc pathways


.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames