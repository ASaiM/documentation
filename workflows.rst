.. _framework-workflow:

Workflows
=========

To orchestrate tools and help users with their analyses, several workflows populate ASaiM framework. They formally orchestrate tools in a defined order and with defined parameters, but they are customizable (tools, order, parameters).

Analysis of raw metagenomic or metatranscriptomic shotgun data
--------------------------------------------------------------

A workflow quickly produces, from raw metagenomic or metatranscriptomic shotgun data, accurate and precise taxonomic assignations, wide extended functional results and taxonomically related metabolism information


.. figure:: /assets/images/framework/main_workflow.png
   :align: center

    Main ASaiM workflow to analyze raw sequences. Image available under CC-BY license (`https://doi.org/10.6084/m9.figshare.5371396.v3 <https://doi.org/10.6084/m9.figshare.5371396.v3>`_) 


This workflow consists of 

1. Processing with quality control/trimming (FastQC and Trim Galore!) and dereplication (VSearch :cite:`rognes_vsearch:_2015`)
2. Taxonomic analyses with assignation (MetaPhlAn2 :cite:`truong_metaphlan2_2015`) and visualization (KRONA :cite:`ondov2011interactive`, GraPhlAn :cite:`asnicar2015compact`)
3. Functional analyses with metabolic assignation and pathway reconstruction (HUMAnN2 :cite:`abubucker_metabolic_2012`)
4. Functional and taxonomic combination with developed tools combining HUMAnN2 and MetaPhlAn2 outputs

This workflow has been tested on two mock metagenomic datasets with controlled communities (See :ref:`"Validation" <framework-validation>`).


Analysis of amplicon data
-------------------------

To analyze amplicon data, the Mothur and QIIME tool suites are available to ASaiM. We integrated the workflows described in tutorials of Mothur and QIIME websites, as example of amplicon data analyses as well as support for the training material. These workflows, as any workflows available in ASaiM, can be adapted for a specific analysis or used as subworkflows by the users.


Running as in EBI metagenomics
------------------------------

The tools used in the EBI Metagenomics pipeline are also available in ASaiM. We integrate then also a workflow with the same steps as the EBI Metagenomics pipeline. Analyses made in EBI Metagenomics website can be then reproduced locally, without having to wait for availability of EBI Metagenomics or to upload any data on EBI Metagenomics. However the parameters must be defined by the user as we can not find them on EBI Metagenomics documentation.

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames