.. _for-devs-technological-choices:

ASaiM framework 
###############

ASaiM framework relies mainly on a :ref:`configuration file <for-devs-configuration-file>` describing the generated pipeline. This pipeline is then executed by call of the different choosen modules, submodules and tools. These calls and the interface between the different tools is made with ``Python`` scripts and modules. 

A pipeline to process metatranscriptomic or metagenomic sequences need several tools and databases. To avoid to install them and their dependencies on each computers, they are included in a :ref:`Docker image <for-devs-docker-images>` which is easily loaded into :ref:`Docker container <for-devs-docker-container>` using :ref:`make <for-devs-make>`.

.. toctree::
   :maxdepth: 2

   configuration_file
   code_architecture
   docker
   make
   .. workflow_manager
   
   

