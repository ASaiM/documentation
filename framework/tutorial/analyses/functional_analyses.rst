.. _framework-tutorial-functional-analysis:

Functional analyses
===================

Investigation of sample composition give an insight on "What organisms are present in our sample". We now want to know "What are they doing in that sample ?", with metabolic analyses.

Metabolic analysis
------------------

For this investigation, we need to affiliate sequences to a protein database.
We choose for this task to use `HUMAnN2 <http://huttenhower.sph.harvard.edu/humann2>`_.
HUMAnN profiles the presence/absence and abundance of gene families and microbial 
pathways in a community from metagenomic or metatranscriptomic sequencing data.

HUMAnN2 is available in `Analyze metabolism` (`Functional assignation` section). We execute HUMAnN2 on non rRNA sequences:

.. _humann2_param:

.. figure:: /assets/images/framework/tutorial/humann2_param.png

3 output files are generated:

- A file with abundance of found UniRef50 gene families
- A file with coverage of found Metacyc pathways
- A file with abundance of found Metacyc pathways

These 3 files give detailed insights into gene families and pathways. This is interesting when we want to look to a particular pathway or to check abundance of a given gene families. However, when we want a broad overview of metabolic processes in a community, we need tools to regroup gene families or pathways into global categories.

Broad overview of metabolic analysis
------------------------------------

To get global categories from HUMAnN2 outputs, we decide to use `Gene Ontology <http://geneontology.org/>`_. Gene ontology project is a collaborative project to get a 3 structures ontologies to describe gene products in terms of their associated biological processes, cellular components and molecular functions. 

HUMAnN2 gives opportunity to regroup UniRef50 gene family abundances into GO abundances. However, these GO terms are still too precise to get a good overview of metabolic processes. 

Gene Ontology Consortium proposes `GO slim <http://geneontology.org/page/go-slim-and-subset-guide>`_, which are cut-down versions of the GO ontologies to give a broad overview of the ontology content. In our case, we use metagenomic GO slim terms developed by Jane Lomax and the InterPro group. 

To regroup HUMAnN2 output containing UniRef50 gene family abundances into abundances of metagenomic GO slim term, we use `Group humann2 uniref50 abundances to Gene Ontology (GO) slim terms <https://github.com/ASaiM/group_humann2_uniref_abundances_to_GO>`_ :cite:`batut_group_humann2_uniref_abundances_to_go:_2016`. This tool uses `GoaTools <https://github.com/tanghaibao/goatools>`_ :cite:`tang_goatools:_2016` to map GO terms to GO slim terms, HUMAnN2 to regroup abundances of UniRref50 gene families into abundances of metagenomc GO slim terms and custom Python scripts.

Tool to group HUMAnN2 UniRef50 abundances to Gene Ontology (GO) slim terms is available in `Analyse metabolism` (`Functional assignation` section). We execute it on HUMAnN2 output containing UniRef50 gene family abundance:

.. _group_humann2_uniref_abundances_to_go_param:

.. figure:: /assets/images/framework/tutorial/group_humann2_uniref_abundances_to_go_param.png

This tool generates 3 tabular outputs:

- A file with abundances of GO terms corresponding to molecular functions
- A file with abundances of GO terms corresponding to biological processes
- A file with abundances of GO terms corresponding to cellular components

Visualization of metabolic analysis
-----------------------------------

The 3 previously generated tabular files with relative abundances of Gene Ontology slim terms can be visualised with barplots. A tool `Plot barplot with R` is available in `Visualize data` (`Post treatments` section):

.. _plot_barplot:

.. figure:: /assets/images/framework/tutorial/plot_barplot.png

Several graphical options are available such as margins, labels, bar color, ...

For our dataset, we execute this tool 3 times to obtain the following 3 graphics 

.. _cellular_component_abundance:

.. figure:: /assets/images/framework/tutorial/cellular_component_abundance.png
    :scale: 50 %

    Relative abundance of GO slim terms corresponding to cellular components
    

.. _biological_process_abundance:

.. figure:: /assets/images/framework/tutorial/biological_process_abundance.png
    :scale: 50 %

    Relative abundance of GO slim terms corresponding to biological processes


.. _molecular_function_abundance:

.. figure:: /assets/images/framework/tutorial/molecular_function_abundance.png
    :scale: 50 %

    Relative abundance of GO slim terms corresponding to molecular fonctions


.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames