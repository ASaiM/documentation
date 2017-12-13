.. _framework-workflow:

Workflows
=========

To orchestrate tools and help users with their analyses, several workflows populate ASaiM framework. They formally orchestrate tools in a defined order and with defined parameters, but they are customizable (tools, order, parameters).

Analysis of raw metagenomic or metatranscriptomic shotgun data
--------------------------------------------------------------

The workflow quickly produces, from raw metagenomic or metatranscriptomic shotgun data, accurate and precise taxonomic assignations, wide extended functional results and taxonomically related metabolism information


.. figure:: /assets/images/framework/main_workflow.png
    :align: center

    Main ASaiM workflow to analyze raw sequences. Image available under CC-BY license (`https://doi.org/10.6084/m9.figshare.5371396.v3 <https://doi.org/10.6084/m9.figshare.5371396.v3>`_)


This workflow consists of

1. Processing with quality control/trimming (FastQC and Trim Galore!) and dereplication (VSearch :cite:`rognes_vsearch:_2015`)
2. Taxonomic analyses with assignation (MetaPhlAn2 :cite:`truong_metaphlan2_2015`) and visualization (KRONA :cite:`ondov2011interactive`, GraPhlAn :cite:`asnicar2015compact`)
3. Functional analyses with metabolic assignation and pathway reconstruction (HUMAnN2 :cite:`abubucker_metabolic_2012`)
4. Functional and taxonomic combination with developed tools combining HUMAnN2 and MetaPhlAn2 outputs

This workflow has been tested on two mock metagenomic datasets with controlled communities (See :ref:`"Validation" <framework-validation>`).


Assembly of metagenomic data
----------------------------

To reconstruct genomes or to get longer sequences for further analysis, microbiota data needs to be assembled, using the recently developed metagenomics assemblers.

To help in this task, two workflows have been developed in ASaiM, each one using one of each of the well-performing assemblers :cite:`quince2017shotgun,van2017assembling,sczyrba2017critical,greenwald2017utilization,olson2017metagenomic,vollmers2017comparing,awad2017evaluating`

- MEGAHIT :cite:`li2015megahit`

    It is currently the most efficent computationally assembler: it has the lowest memory and time consumption :cite:`van2017assembling,awad2017evaluating,sczyrba2017critical`. It produced some of the best assemblies (irrespective of sequencing coverage) with the fewest structural errors :cite:`olson2017metagenomic` and outperforms in recovering the genomes of closely related strains :cite:`awad2017evaluating`, but has a bias towards relatively low coverage genomes leading to a suboptimal assembly of high abundant community member genomes in very large datasets :cite:`vollmers2017comparing`

- MetaSPAdes :cite:`nurk2017metaspades`

    It is particularly optimal for high-coverage metagenomes :cite:`van2017assembling` with the best contig metrics :cite:`greenwald2017utilization` and produces few under-collapsed/over-collapsed repeats :cite:`olson2017metagenomic`

Both workflows consists of

1. Processing with quality control/trimming (FastQC and Trim Galore!)
2. Assembly with either MEGAHIT or MetaSPAdes
3. Estimation of the assembly quality statistics with MetaQUAST :cite:`mikheenko2015metaquast`
4. Identification of potential assembly error signature with VALET
5. Determination of percentage of unmapped reads with Bowtie2 :cite:`langmead2009ultrafast` combined with MultiQC :cite:`ewels2016multiqc` to aggregate the results.


Analysis of metataxonomic data
------------------------------

To analyze amplicon data, the Mothur and QIIME tool suites are available to ASaiM. We integrated the workflows described in tutorials of Mothur and QIIME websites, as example of amplicon data analyses as well as support for the training material. These workflows, as any workflows available in ASaiM, can be adapted for a specific analysis or used as subworkflows by the users.


Running as in EBI metagenomics
------------------------------

The tools used in the EBI Metagenomics pipeline are also available in ASaiM. We integrate then also a workflow with the same steps as the `EBI Metagenomics pipeline (3.0) <https://www.ebi.ac.uk/metagenomics/pipelines/3.0>`_.

.. figure:: /assets/images/framework/ebi_metagenomics_workflow.png
    :align: center

    EBI Metagenomics workflow (3.0) in ASaiM

Analyses made in EBI Metagenomics website can be then reproduced locally, without having to wait for availability of EBI Metagenomics or to upload any data on EBI Metagenomics. However the parameters must be defined by the user as we can not find them on EBI Metagenomics documentation.

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
