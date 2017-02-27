.. _framework-conception:

Conception 
==========

Analyses of microbiota sequences are complex and include numerous steps such as:

1. Quality control
2. Sort of interesting sequence
3. Functional annotation
4. Taxonomic analysis

Each task may require execution of several tools or software. Selecting the best tools with correct parameter values and combining tools together in an analysis chain is a complex and error-prone process. 

To improve usability and reproducibility in microbiota studies, `Galaxy <https://galaxyproject.org/>`_ may be a good solution. `Galaxy <https://galaxyproject.org/>`_ is a lightweight environment providing a simple graphical interface to bioinformatics tools, while automatically managing computation and data details. 

Galaxy environments can integrate numerous bioinformatics tools using `Galaxy ToolShed <https://toolshed.g2.bx.psu.edu/>`_. But, it can be difficult to choose the best tools with optimal parameters and to orchestrate them in workflow to analyse microbiota sequences. 

To overcome these limitations, we developed ASaiM, an open-source opiniated framework. Based on a custom Galaxy instance, the framework integrates tools and workflows specifically chosen and built for microbiota studies

.. _framework_scheme:

.. figure:: /assets/images/framework/framework_scheme.png

It integrates :ref:`tools <framework-tools>` and :ref:`workflows <framework-workflow>` dedicated to microbiota analyses 