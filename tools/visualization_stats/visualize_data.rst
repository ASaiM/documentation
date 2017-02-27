.. _framework-tools-visualization-stats-visualization:

==============
Visualize data
==============

.. _framework-tools-visualization-stats-visualization-export2graphlan:

Export2GraPhlAn
================

export2graphlan is a conversion software tool to produce both annotation and tree file for GraPhlAn. It can convert MetaPhlAn, LEfSe, and/or HUMAnN output to GraPhlAn input format

In particular, the annotation file tries to highlight specific sub-trees deriving automatically from input file what nodes are important.

For more information, check the `user manual <https://bitbucket.org/CibioCM/export2graphlan/overview/>`_.

.. _framework-tools-visualization-stats-visualization-graphlan:

GraPhlAn
========

GraPhlAn is a software tool for producing high-quality circular representations of taxonomic and phylogenetic trees.

GraPhlAn focuses on concise, integrative, informative, and publication-ready representations of phylogenetically- and taxonomically-driven investigation.

For more information, check the `user manual <https://bitbucket.org/nsegata/graphlan/overview>`_.

.. _framework-tools-visualization-stats-visualization-graphlan-graphlan:

GraPhlAn to produce graphical output of an input tree
-----------------------------------------------------

This tool produces graphical output of an input tree, generated, personalized, and annotated using the :ref:`dedicated tool <framework-tools-visualization-stats-visualization-graphlan-input>`.

.. _framework-tools-visualization-stats-visualization-graphlan-input:

Generation, personalization and annotation of tree for GraPhlAn
---------------------------------------------------------------

This tool modifies any input tree (in any of the three standard format) adding additional information regarding structural or graphical aspects of the tree (like colors and style of the taxa, labels, shadows, heatmaps, ...). It generates PhyloXML files that can be converted into image using :ref:`GraPhlAn main tool`.

Two inputs are expected: input tree in any of the three most popular format (Newick, PhyloXML, or text format) and an annotation file.

The annotation file is a tab-delimited file listing the graphical options for clades. Usually each line has three fields: the name of the clade, the name of the option, and the value to assign to the option. Lines can however have two fields (typically for "global" option not referred to a specific clade) or four fields when the external rings (a sort of circular heatmap) is specified. This file can be generated using :ref:`Export2GraPhlAn <framework-tools-visualization-stats-visualization-export2graphlan>`. More information about this file is available on `GraPhlAn user manual <https://bitbucket.org/nsegata/graphlan/overview>`_.

.. _framework-tools-visualization-stats-visualization-krona:

KRONA
=====

`KRONA <https://github.com/marbl/Krona/wiki>`_ :cite:`ondov_interactive_2011,cuccuru_orione_2014` allows hierarchical data to be explored with zoomable pie charts. Krona charts can be created using an Excel template or KronaTools, which includes support for several bioinformatics tools and raw data formats. The charts can be viewed with a recent version of any major web browser.

Particularly, this tool renders results of a metagenomic profiling as a zoomable pie chart

.. _framework-tools-visualization-stats-visualization-barplot:

Plot barplot with R
===================

This tool plot a barplot using R's ``barplot`` function.

The input file must be a tabular file with multiple columns: a column with row names (for bar names) and a least a column with data.

The output image is customizable (margin, legend positions, ...) and can be export in different format.

.. _framework-tools-visualization-stats-visualization-gbarplot:

Plot grouped barplot with R
===========================

This tool plot a grouped barplot with multiple data, using R's ``barplot`` function.

The input file must be a tabular file with multiple columns: a column with row names (for bar names) and a least a column with data.

The output image is customizable (margin, legend positions, ...) and can be export in different format.

.. _framework-tools-visualization-stats-visualization-xy:

Plot generic X-Y plot with R
============================

This tool plot a generic X-Y plot using the standard R's ``plot`` function.

The input file must be a tabular file with at least two data columns.

The output image is customizable (margin, legend positions, ...) and can be export in different format.

.. _framework-tools-visualization-stats-visualization-histo:

Histogram of a numeric column
=============================

This tool computes a histogram of the numerical values in a column of a dataset.

All invalid, blank and comment lines in the dataset are skipped. The number of skipped lines is displayed in the resulting history item.

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
