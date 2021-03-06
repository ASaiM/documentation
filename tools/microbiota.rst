.. _framework-tools-microbiota:

==========================
Microbiota dedicated tools
==========================

Metagenomics data manipulation
==============================

+------------------------------------------+---------+------------------------------------------------------------------+
| Name                                     | Version | Galaxy wrapper                                                   |
+==========================================+=========+==================================================================+
| VSEARCH :cite:`rognes_vsearch:_2015`     | 1.9.7   | `vsearch <https://toolshed.g2.bx.psu.edu/view/iuc/vsearch>`_     |
+------------------------------------------+---------+------------------------------------------------------------------+
| Nonpareil :cite:`rodriguez2013nonpareil` | 3.1.1   | `nonpareil <https://toolshed.g2.bx.psu.edu/view/iuc/nonpareil>`_ |
+------------------------------------------+---------+------------------------------------------------------------------+

Assembly
========

+------------------------------------------+---------+-------------------------------------------------------------------+
| Name                                     | Version | Galaxy wrapper                                                    |
+==========================================+=========+===================================================================+
| MEGAHIT :cite:`li2015megahit`            | 1.1.2   | `vsearch <https://toolshed.g2.bx.psu.edu/view/iuc/megahit>`_      |
+------------------------------------------+---------+-------------------------------------------------------------------+
| metaSPAdes :cite:`nurk2016metaspades`    | 3.9.0   | `nonpareil <https://toolshed.g2.bx.psu.edu/view/nml/metaspades>`_ |
+------------------------------------------+---------+-------------------------------------------------------------------+
| metaQUAST :cite:`mikheenko2015metaquast` | 4.5     | `quast <https://toolshed.g2.bx.psu.edu/view/iuc/quast>`_          |
+------------------------------------------+---------+-------------------------------------------------------------------+
| VALET                                    | 1.0     | `valet <https://toolshed.g2.bx.psu.edu/view/iuc/valet>`_          |
+------------------------------------------+---------+-------------------------------------------------------------------+

Metataxonomic sequence analysis
===============================

+-----------------------------------------+---------+------------------------------------------------------------------------+
| Name                                    | Version | Galaxy wrapper                                                         |
+=========================================+=========+========================================================================+
| Mothur :cite:`schloss_introducing_2009` | 1.36.1  | `suite_mothur <https://toolshed.g2.bx.psu.edu/view/iuc/suite_mothur>`_ |
+-----------------------------------------+---------+------------------------------------------------------------------------+
| QIIME :cite:`caporaso_qiime_2010`       | 1.9.1   | `suite_qiime <https://toolshed.g2.bx.psu.edu/view/iuc/suite_qiime>`_   |
+-----------------------------------------+---------+------------------------------------------------------------------------+

Taxonomy assignation on WGS sequences
=====================================

+-------------------------------------------+---------+----------------------------------------------------------------------------------------------------+
| Name                                      | Version | Galaxy wrapper                                                                                     |
+===========================================+=========+====================================================================================================+
| MetaPhlAn2 :cite:`truong_metaphlan2_2015` | 2.6.0   |`suite_metaphlan2 <https://toolshed.g2.bx.psu.edu/view/iuc/suite_metaphlan2>`_                      |
+-------------------------------------------+---------+----------------------------------------------------------------------------------------------------+
| Format MetaPhlAn2                         | 0.1.0   | `format_metaphlan2_output <https://toolshed.g2.bx.psu.edu/view/bebatut/format_metaphlan2_output>`_ |
+-------------------------------------------+---------+----------------------------------------------------------------------------------------------------+
| KRAKEN :cite:`wood2014kraken`             | 0.10.5  | `suite_kraken_0_10_5 <https://toolshed.g2.bx.psu.edu/view/devteam/suite_kraken_0_10_5>`_           |
+-------------------------------------------+---------+----------------------------------------------------------------------------------------------------+

Metabolism assignation
======================

+--------------------------------------------------------+---------+------------------------------------------------------------------------------------------------------------------------------+
| Name                                                   | Version | Galaxy wrapper                                                                                                               |
+========================================================+=========+==============================================================================================================================+
| HUMAnN2 :cite:`abubucker_metabolic_2012`               | 0.11.1  | `suite_humann2 <https://toolshed.g2.bx.psu.edu/view/iuc/suite_humann2>`_                                                     |
+--------------------------------------------------------+---------+------------------------------------------------------------------------------------------------------------------------------+
| Group HUMAnN2 to GO slim term :cite:`batut_group_2016` | 1.2.0   | `group_humann2_uniref_abundances_to_go <https://toolshed.g2.bx.psu.edu/view/bebatut/group_humann2_uniref_abundances_to_go>`_ |
+--------------------------------------------------------+---------+------------------------------------------------------------------------------------------------------------------------------+
| PICRUST :cite:`langille2013predictive`                 | 1.1.1   | `suite_picrust <https://toolshed.g2.bx.psu.edu/view/iuc/suite_picrust>`_                                                     |
+--------------------------------------------------------+---------+------------------------------------------------------------------------------------------------------------------------------+
| InterProScan :cite:`hunter2008interpro`                | 5.0.0   | `interproscan5 <https://toolshed.g2.bx.psu.edu/view/bgruening/interproscan5>`_                                               |
+--------------------------------------------------------+---------+------------------------------------------------------------------------------------------------------------------------------+

Combination of functional and taxonomic results
===============================================

+----------------------------------------+---------+--------------------------------------------------------------------------------------------------------+
| Name                                   | Version | Galaxy wrapper                                                                                         |
+========================================+=========+========================================================================================================+
| Combine MetaPhlAn2 and HUMAnN2 outputs | 0.1.0   | `combine_metaphlan2_humann2 <https://toolshed.g2.bx.psu.edu/view/bebatut/combine_metaphlan2_humann2>`_ |
+----------------------------------------+---------+--------------------------------------------------------------------------------------------------------+

Visualization

+--------------------------------------------------------------------+---------+-----------------------------------------------------------------------------------------+
| Name                                                               | Version | Galaxy wrapper                                                                          |
+====================================================================+=========+=========================================================================================+
| `export2graphlan <https://bitbucket.org/CibioCM/export2graphlan>`_ | 0.19    | `export2graphlan <https://toolshed.g2.bx.psu.edu/view/iuc/export2graphlan>`_            |
+--------------------------------------------------------------------+---------+-----------------------------------------------------------------------------------------+
| GraPhlAn :cite:`asnicar2015compact`                                | 1.0.0   | `suite_graphlan <https://toolshed.g2.bx.psu.edu/view/iuc/suite_graphlan>`_              |
+--------------------------------------------------------------------+---------+-----------------------------------------------------------------------------------------+
| KRONA :cite:`ondov2011interactive`                                 | 2.6.1   | `taxonomy_krona_chart <https://toolshed.g2.bx.psu.edu/view/crs4/taxonomy_krona_chart>`_ |
+--------------------------------------------------------------------+---------+-----------------------------------------------------------------------------------------+


.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
