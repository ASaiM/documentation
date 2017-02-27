.. _environment:

ASaiM 
=====

ASaiM is a bioinformatics environment for optimised processing and analysis of massive microbiota data, particularly gut microbiota data.


.. _environment-context:

Context 
#######

Massive data of intestinal microbiota are available in the public data repositories such as `ENA <http://www.ebi.ac.uk/ena>`_, `NCBI <http://www.ncbi.nlm.nih.gov/>`_, `DDBJ <http://www.ddbj.nig.ac.jp/>`_, ... For example, in the ENA public data repository, 721 studies contain in their description the word "intestin", "gut" or "feac" and in their name "meta" (09/26/2015). 
However, this data is not easy to identify (many of these 721 studies are not relevant) and query. 
Moreover the datasets underwent different analyses and the results of different projects can not be compared directly.
Datasets from public data repositories need to be formated to make them informative and standardized and then extract information such as which organisms are present or which functions are done in a specific sample of gut microbiota.

For that, data from public data repositories must be re-analyzed using a full analytical workflow with several steps, such as the standard defined by :cite:`ladoukakis_integrative_2014`: 

1. Quality control
2. (Assembly of sequences)
3. Sorting of pertinent sequence
4. Functional annotation
5. Taxonomic analysis
6. Comparative analysis

Several solutions could be used :cite:`ladoukakis_integrative_2014`:

- QIIME :cite:`caporaso_qiime_2010`, Mothur :cite:`schloss_introducing_2009`, ...

    These tools are useful to analyze microbiota data. Most of them are available through command line, which is more convenient to 
    analyze large and numerous datasets. However, the execution by command line is also a limitation for many users. Also, these tools are only one or few steps in the data analysis process, and are mostly dedicated to the analysis of 16S rDNA datasets

- MEGAN :cite:`huson_integrative_2011`

    This tool targets metagenomic data but lacks critical tasks such as taxonomic and functional analysis

- CAMERA :cite:`seshadri_camera:_2007`
    
    This pipeline is no longer supported starting from 1st of July 2014

- IMG/M :cite:`markowitz_img/m_2014,markowitz_img/m:_2008`

    IMG/M is an experimental metagenome data management and analysis system. It provides a genome database from bacterial, archaeal and selected eukaryotic organisms and a suite of tools for data exploration and comparative data analysis. This tool is designed for assembled metagenomes and does not provide any tool for quality control and other tasks up to assembly. Moreover, it is not modular and can be used only via the web-based interface

- MG-RAST :cite:`meyer_metagenomics_2008,aziz_rast_2008` 

    This tool uses an automated pipeline to analyze the data and standardize the outputs. Numerous tools are also available but none for quality control and assembly of the sequences. Also this tool is only available through a web interface, where datasets have to be uploaded. Data analysis is then decentralized. We do not have any control on that and it could take time. This solution is not convenient for large and numerous datasets, such as the ones in public data repositories

- EBI metagenomics :cite:`hunter_ebi_2014`
    
    EBI metagenomics tool is similar to MG-RAST or IMG/M with an automated pipeline via a web-based interface. The advantage over other solutions is that this tool used EBI expertise in sequence data archiving and analysis. However, this solution, like MG-Rast or IMG/M, is not convenient to analyze large and numerous datasets 
   
- CloVR-metagenomics :cite:`angiuoli_clovr:_2011`

    CloVR-metagenomics is desktop application which can be complemented by a cloud-based instance. It provides a defined pipeline for automated sequence analysis. However, this solution lacks some tools such as quality control, assembly or gene detection

- SmashCommunity :cite:`arumugam_smashcommunity:_2010`
    
    This solution provides an automated workflow from sequence assembly to comparative analysis, with numerous tools. However all these tools have to be installed locally before any execution and SmashCommunity is only executable with command-line, no user-friendly interface being available

- RAMMCAP :cite:`li_analysis_2009`

    RAMMCAP is a metagenomic platform with a workflow which enables a complete metagenomic analysis. The strength of this platform relies on the minimization of the computation cost of the various processing tasks. However, it does not provide a user-friendly interface and each of the required programs has to be compiled and installed separetely. This is a weakness for an inexperienced user.

- MetAMOS :cite:`treangen_metamos:_2013`

    This tool is an open source, modular and customizable framework for metagenomic assembly and analysis to produce genomic scaffolds, open-reading frames and taxonomic or functional annotations. This tool is mainly focused on metagenome assembly and is presented as the assembly-centric counterpart to QIIME and Mothur. It also provides several interesting tools for analysis. This tool is guided by two principles: modularity and robustness. It encourages users to tailor the tool to the biological questions they want to answer, not the opposite. However, this tool does not provide many useful sotfwares, is managed only with command line (useful for numerous analyses but not for a single specific analysis) and the pipeline definition lacks of visual and documented information.

- Galaxy :cite:`goecks_galaxy:_2010,giardine_galaxy:_2005`

    Galaxy is an open, web-based platform for performing accessible, reproducible, and transparent genomic science. This platform offers numerous tools and also several worflows to analyze metagenomic datasets, such as `Galaxy metagenomic pipeline <https://usegalaxy.org/u/aun1/p/windshield-splatter>`_ :cite:`kosakovsky_pond_windshield_2009`, `Orione <https://orione.crs4.it/>`_ :cite:`cuccuru_orione_2014`, BioMaS :cite:`fosso_biomas:_2015`, `Huttenhower Lab Galaxy instance <http://huttenhower.sph.harvard.edu/galaxy/>`_. It combines a user-friendly web-based interface and an use with an API for command-line. However, the available metagenomic workflows have to be adapted to process gut microbiota data with specific databases such as the catalog of reference genes in the human gut microbiome :cite:`li_integrated_2014`

None of these solutions respond to all following requirements

- Complete analytical workflow such as the one proposed by :cite:`ladoukakis_integrative_2014` with gut microbiota specific databases
- User-friendly interface and command-line use to automate analysis of numerous datasets
- Data management capabilities


.. _environment-solution:

Solution 
########

New sequencing platforms produce huge amount of short reads. Notwithstanding, inappropriate use of sequence analysis procedures may result in numerous errors and misinterpretation. This is particularly true for exploration of metagenomic and metatranscriptomic data from complex microorganims communities colonizing all environments. Hence as these communities are highly studied, there is an urgent need for modular, accessible and sharable user-friendly tools.

ASaiM is an open-source opinionated framework dedicated to microbiota sequence analyses. With a selected collection of tools, workflows and databases, ASaiM helps exploitation of taxonomic and metabolic information from raw microbiota sequences, using a custom Galaxy instance

.. _framework_custom_galaxy_instance:

.. figure:: /assets/images/framework/galaxy_instance.png
    :align: center

    Screenshot of the custom Galaxy instance of ASaiM framework

This framework is developed to :

      - be easy to use for all from beginners to expert. Check by yourself :ref:`how to construct and execute a workflow <framework-workflow>` or follow the :ref:`tutorial <framework-tutorial>` with available toy dataset
      - incorporate numerous but carefully selected tools. Check out all the available :ref:`tools <framework-tools>`.
      - help generation of modular workflows. Look at the availables :ref:`workflows <framework-workflow>`.
      - improve transparency and reproducibility of microbiota studies

ASaiM provides therefore a powerful framework to easily and rapidly exploit microbiota data in a reproducible and transparent environment.


.. rubric:: References

.. bibliography:: assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames


