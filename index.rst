ASaiM: an environment to analyze intestinal microbiota data
===========================================================

New generation of sequencing platforms coupled to numerous bioinformatics tools has led to rapid technological progress in metagenomics and metatranscriptomics to investigate complex microorganism communities. Nevertheless, a combination of different bioinformatic tools remains necessary to draw conclusions out of microbiota studies. Modular and user-friendly tools would greatly improve such studies.


We therefore developed ASaiM, an Open-Source Galaxy-based framework dedicated to microbiota data analyses. ASaiM offers sophisticated analyses to scientists without command-line knowledge. ASaiM provides a powerful framework to easily and quickly explore microbiota data in a reproducible and transparent environment.

A framework built on the shoulders of giants
********************************************

To develop a modular, accessible, redistributable, sharable and user-friendly framework for scientist, we developed ASaiM using

- `Galaxy <https://galaxyproject.org>`_ as the foundation
    
    `Galaxy <https://galaxyproject.org/>`_ is a lightweight environment providing a simple graphical interface to bioinformatics tools, while automatically managing computation and data details. It improves the usability and reproducibility of biological studies.

- `Galaxy ToolShed <https://toolshed.g2.bx.psu.edu/>`_, `BioBlend <http://bioblend.readthedocs.io/en/latest/>`_ and `Ephemeris <https://ephemeris.readthedocs.io/en/latest/>`_ to install the tools, the worklows and the databases inside the Galaxy environment
- `Conda <https://conda.io/docs/index.html>`_ to install the tools and their dependencies
- `Docker <https://www.docker.com/>`_ to containerize and ship everything

... Dedicated to microbiota analyses
************************************

ASaiM integrate a comprehensive set of microbiota related :ref:`tools <framework-tools>`, predefined and tested 
:ref:`workflows <framework-workflow>` dedicated to microbiota analyses.

Tools, workflows and ASaiM are supported by :ref:`training material <framework-tutorials-tours>` and documentation:

.. toctree::
  :maxdepth: 4

  installation
  tutorials_tours
  tools/index
  workflows
  validation

