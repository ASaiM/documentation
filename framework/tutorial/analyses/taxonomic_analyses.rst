.. _framework-tutorial-taxonomic-analysis:

Taxonomic analysis
==================

To identify micro-organisms populating a sample and their proportion, we use 
:ref:`taxonomic and phylogenetic approaches <framework-tools-available-taxonomic-assignation>`. 
Indeed, in these approaches, each reads or sequences are assigned to the most 
plausible microbial lineage. 

Most tools used to estimate sample composition use 16S rRNA genes as marker for
bacteria and archea and 18S rRNA genes for eukarya. It is the approache used by
QIIME :cite:`caporaso_qiime_2010` and 
:ref:`taxonomic analysis of rRNA sequences <framework-tutorial-taxonomic-analysis-nonrRNA>`.

Other tools, such as MetaPhlAn :cite:`segata_metagenomic_2012,truong_metaphlan2_2015`,
propose alternatives based on more general clade-specific marker genes. We can
use such approaches to :ref:`analyze taxonomy of non rRNA sequences <framework-tutorial-taxonomic-analysis-rRNA>`.

.. _framework-tutorial-taxonomic-analysis-nonrRNA:

Taxonomic analysis on rRNA sequences
####################################

*In development*

.. _framework-tutorial-taxonomic-analysis-rRNA:

Taxonomic analysis on non rRNA sequences
########################################

To estimate sample composition, we can also use MetaPhlAn2 :cite:`truong_metaphlan2_2015`
on non rRNA sequences. This tool infer the presence and read coverage of 
clade-specific markers to detect taxonomic clades and their relative abundance.

Taxonomic assignation
---------------------

This tool is available on left panel in `Assign taxonomy on non rRNA sequences` 
(`Taxonomic assignation`). In this tutorial, you execute it on non rRNA sequences
from first :ref:`SortMeRNA execution <framework-tutorial-pretreatments-rna-sorting>`.

.. _metaphlan_2_parameters:

.. figure:: /assets/images/framework/tutorial/metaphlan_2.png

In the dataset, we obtain a text file with 59 lines, each line corresponding to
a taxonomic assignation (represented at different taxonomic level) with its
relative abundance.

.. _metaphlan_2_output:

.. figure:: /assets/images/framework/tutorial/metaphlan_2_output.png

Taxonomic assignation visualization
-----------------------------------

The output in plain text is not easy to interpret. We can use visualization tools
to get a graphical representation of MetaPhlAn 2 output. Two solutions can be
used (GraPhlAn ou KRONA).

Interactive visualization
~~~~~~~~~~~~~~~~~~~~~~~~~ 

Krona :cite:`ondov_interactive_2011` is a visualization tool for intuitive 
exploration of relative abundances of taxonomic classifications. Krona requires 
a formatted input file. 

MetaPhlAn2 output has then to be formatted using 
`Format MetaPhlAn2 output for Krona` (in `Assign taxonomy on non rRNA sequences`, 
`Taxonomic assignation`):

.. _format_metaphlan2:

.. figure:: /assets/images/framework/tutorial/format_metaphlan2.png

Krona can then be called (`Krona pie chart from taxonomic profile`, in 
`Visualize data`, in `Post-treatments`)

.. _krona_call:

.. figure:: /assets/images/framework/tutorial/krona_call.png

Krona produces an interactive HTML file. The content can be visualized inside
Galaxy environment by clicking on `View data` on top right of Krona output in 
right panel.

.. _krona_output:

.. figure:: /assets/images/framework/tutorial/krona_output.png

This visualization is similar to the one on EBI metagenomic.

Static, easy to export visualization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 

Alternatively, `GraPhlAn <https://bitbucket.org/nsegata/graphlan/wiki/Home>`_ is 
a tool for producing circular representation of taxonomic analyses, easily 
exportable. This tool requires 2 files: a tree and an annotation file. 

However, MetaPhlAn produces only a :ref:`text file <metaphlan_2_output>`. We 
need to use a tool to extract tree and annotations from MetaPhlAn output. We 
use `export2graphlan <https://bitbucket.org/CibioCM/export2graphlan>`_, available
in section `Visualize data` (in `Post-treatments`). Numerous parameters modulates
informations in annotation file. For our dataset, we fix :

- Levels to annotate in the tree: 5
- Levels to annotate in the external legend: 6,7
- Title font size: 15
- Default size for clades not found as biomarkers: 10
- Minimum value of biomarker clades: 0
- Maximum value of biomarker clades: 250
- Font size: 10
- Minimum font size: 8
- Maximum font size: 12
- Font size for the annotation legend: 11
- Minimum abundance value for a clade to be annotated: 0
- Number of clades to highlight: 100
- Row number contaning the names of the features: 0
- Row number containing the names of the samples: 0

We decide to display the maximum of clade (100, here). If you want more or less,
you can modulate the number of clades to highlight. And if you want to change 
displayed annotations, you can change levels to annotate.

This tool will generate two outputs (a tree and an annotation files). These two
outputs have to be combined in first GraPhlAn script (`Modify an input tree for GraPhlAn`,
in `Visualize data`):

.. _graphlan_annotate_parameters:

.. figure:: /assets/images/framework/tutorial/graphlan_annotate_parameters.png

This tool generates a PhyloXML file, input file for GraPhlAn.

GraPhlAn is available in `Visualize data` section (`Post-treatments`). It generates
an output file (an image) corresponding to circular representation of MetaPhlAn 
outputs. Available parameters have impact on output file format, size, ...

.. _graphlan_parameters:

.. figure:: /assets/images/framework/tutorial/graphlan_parameters.png

With our dataset, we obtain a nice graphical representation of taxonomic diversity
inside our sample, with circle radius being proportional to relative abundance
of the corresponding clade.

.. _graphlan_metaphlan_output:

.. figure:: /assets/images/framework/tutorial/graphlan_metaphlan_output.svg

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames