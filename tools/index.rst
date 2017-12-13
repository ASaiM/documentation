.. _framework-tools:

Tools
=====

More than 200 tools are automatically integrated in the custom Galaxy instance during its deployment. They were chosen for their use in exploitation of microbiota data, and are hierarchically organized (into sections and subsection) to guide users and help them to choose the best tools for a specific analysis.

.. toctree::
    :maxdepth: 2

    file_meta_tools
    genomics
    microbiota


These tools come with databases, which are automatically downloaded and configured during deployment of ASaiM Galaxy instance.

+------------+---------+-------------------------------------------------------------------------------+
| Name       | Version | Comments                                                                      |
+============+=========+===============================================================================+
| SILVA      | 119     | Reduced with HMMER 3.1b1 and SumaClust v1.0.00 and formatted for SortMeRNA    |
+------------+---------+-------------------------------------------------------------------------------+
| ChocoPhlAn | 0.1.1   | Microbial pangenomes                                                          |
+------------+---------+-------------------------------------------------------------------------------+
| UniRef50   |         | Filtered with Diamond to be HUMAnN2 compatible                                |
+------------+---------+-------------------------------------------------------------------------------+
| MetaPhlAn2 | 2.2.5   | Unique clade-specific marker genes identified from ≃ 17,000 reference genomes |
+------------+---------+-------------------------------------------------------------------------------+
