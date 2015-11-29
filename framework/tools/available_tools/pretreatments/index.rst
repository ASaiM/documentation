.. _framework-tools-available-pretreatments:

Pretreatments
#############

Raw sequences data need to be pretreated (quality, assembly, sorting, ...) to facilitate downstream analyses. Actually, metagenomic and metatranscriptomic datasets are complex and not only sequencing, but also data analysis costs. Sequence pretreatments may reduce this complexity and inherent misinterpretation of these data.

The necessary data treatments highly depends on the data and technologies used to generate them. The following guide and the proposed treatments should ensure that the data are not too bad. However, there is no "one-size-fits all" solution.

Before any taxonomic or functional assignations, the sequences have to pre-processed with several step.

.. toctree::
    :maxdepth: 2

    assemble_paired_end_sequences
    control_quality/index
    rdp_tools
    vsearch_tools
    cluster_sequences
    manipulate_rna
    search_similarity