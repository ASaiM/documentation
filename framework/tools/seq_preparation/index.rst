.. _framework-tools-available-seq-prep:

====================
Sequence preparation
====================

Raw sequences data need to be pretreated (quality, assembly, sorting, ...) to facilitate downstream analyses. Actually, metagenomic and metatranscriptomic datasets are complex and not only sequencing, but also data analysis costs. Sequence pretreatments may reduce this complexity and inherent misinterpretation of these data.

The necessary data treatments highly depends on the data and technologies used to generate them. The following guide and the proposed treatments should ensure that the data are not too bad. However, there is no "one-size-fits all" solution.

Before any taxonomic or functional assignations, the sequences have to pre-processed with several step.

+------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------+
| Subsection                                                                         | Tool                                                                                                                                                                 | Galaxy wrapper                                                                                                               | 
+                                                                                    +----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
|                                                                                    | Name                                                                                                                                                     | Version   | Name                                                                                                          | Revision     |
+====================================================================================+==========================================================================================================================================================+===========+===============================================================================================================+==============+
| :ref:`Assemble paired-end sequences <framework-tools-available-seq-prep-assemble>` | :ref:`FastQ joiner <framework-tools-available-seq-prep-assemble-fastq-joiner>` :cite:`blankenberg_manipulation_2010`                                     | 1.0.1     | `fastq_paired_end_joiner <https://toolshed.g2.bx.psu.edu/view/devteam/fastq_paired_end_joiner/6a7f5da7c76d>`_ | 6a7f5da7c76d |
+                                                                                    +----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
|                                                                                    | :ref:`FastQ-join <framework-tools-available-seq-prep-assemble-fastq-join>` :cite:`aronesty_ea-utils_2011`                                                | 1.1.2-806 | `fastq_join <https://toolshed.g2.bx.psu.edu/view/lparsons/fastq_join/8ec3dfde378b>`_                          | 8ec3dfde378b |
+------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
| :ref:`Control quality <framework-tools-available-seq-prep-control-quality>`        | :ref:`FastQC <framework-tools-available-seq-prep-control-quality-fastqc>` (`Documentation <http://www.bioinformatics.babraham.ac.uk/projects/fastqc/>`_) | 0.11.4    | `fastqc <https://toolshed.g2.bx.psu.edu/view/devteam/fastqc/3fdc1a74d866>`_                                   | 3fdc1a74d866 |
+                                                                                    +----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
|                                                                                    | :ref:`PRINSEQ <framework-tools-available-seq-prep-control-quality-prinseq>` :cite:`schmieder_quality_2011`                                               | 0.20.4    | prinseq                                                                                                       | 8ec3dfde378b |
+------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
| :ref:`Vsearch tools <framework-tools-available-seq-prep-vsearch>`                  | :ref:`Vsearch tools <framework-tools-available-seq-prep-vsearch>` :cite:`rognes_vsearch:_2015`                                                           | 1.9.7     | `vsearch <https://toolshed.g2.bx.psu.edu/view/iuc/vsearch/4258854759ba>`_                                     | 4258854759ba |
+------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
| :ref:`Cluster sequences <framework-tools-available-seq-prep-cluster>`              | :ref:`CD-HIT (EST/PROTEIN) <framework-tools-available-seq-prep-cluster-cdhit>` :cite:`fu_cd-hit:_2012,li_cd-hit:_2006`                                   | 4.6.4     | `cdhit <https://toolshed.g2.bx.psu.edu/view/bebatut/cdhit/54d811ad2b52>`_                                     | 54d811ad2b52 |
+                                                                                    +----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
|                                                                                    | :ref:`Format cd-hit outputs <framework-tools-available-seq-prep-cluster-forma>`                                                                          |           | `format_cd_hit_output <https://toolshed.g2.bx.psu.edu/view/bebatut/format_cd_hit_output/4015e9d6d277>`_       | 4015e9d6d277 |
+------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
| :ref:`Manipulate RNA <framework-tools-available-seq-prep-manipulate-rna>`          | :ref:`FastQ joiner <framework-tools-common-tools-manipulate-file-paste>` :cite:`blankenberg_manipulation_2010`                                           | 1.0.1     | `fastq_paired_end_joiner <https://toolshed.g2.bx.psu.edu/view/devteam/fastq_paired_end_joiner/6a7f5da7c76d>`_ | 6a7f5da7c76d |
+------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+
| :ref:`Search similarity <framework-tools-available-seq-prep-search_similarity>`    | :ref:`FastQ joiner <framework-tools-common-tools-manipulate-file-paste>` :cite:`blankenberg_manipulation_2010`                                           | 1.0.1     | `fastq_paired_end_joiner <https://toolshed.g2.bx.psu.edu/view/devteam/fastq_paired_end_joiner/6a7f5da7c76d>`_ | 6a7f5da7c76d |
+------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+---------------------------------------------------------------------------------------------------------------+--------------+






.. toctree::
    :hidden:

    assemble_paired_end_sequences
    control_quality
    vsearch
    cluster_sequences
    manipulate_rna
    search_similarity

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames