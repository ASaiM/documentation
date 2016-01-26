.. _framework-workflows-microbiota-sequences-pretreatments:

Pretreatments
=============

Before any analyses (taxonomic or functional), raw sequences have to be pre-processed 
(quality control, sequence sorting and construction of long sequences).

Steps depend on type of input sequences (paired-end or single):

.. _microbiota_data_analysis_pretreatment_workflow:

.. figure:: /assets/images/framework/workflows/pretreatment_workflow.png

   Workflows to pre-process microbiota data from raw sequences

In Galaxy, two workflows manage steps of data pretreatment given the type of
input sequences

.. _microbiota_pretreatment_paired_end_workflow:

.. figure:: /assets/images/framework/workflows/microbiota_pretreatment_paired_end_workflow.svg

   Workflow to pre-process microbiota data from raw sequences in Galaxy (paired-end sequences)

.. _microbiota_pretreatment_single_workflow:

.. figure:: /assets/images/framework/workflows/microbiota_pretreatment_single_workflow.svg

   Workflow to pre-process microbiota data from raw sequences in Galaxy (single sequences)

Quality control and treatment
#############################

Paired-end sequences assembly (for paired-end sequences only)
#############################################################

Split of paired-end sequences (for single sequences only)
#########################################################

This step is needed for 16S reconstruction 

rRNA (rDNA) sorting
###################

16S reconstruction
##################