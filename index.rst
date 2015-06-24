ASaiM: a pipeline generator and runner to process and analyze intestinal microbiota data
########################################################################################

ASaiM is a tool to generate and run pipeline of tools to process and analyze metagenomic and metatranscriptomic data from intestinal microbiota. `Read more about the project <http://asaim.github.io/about/>`_

Numerous tools and programs are available to extract useful information from metagenomic and metatranscriptomic data. However, these tools are often dedicated to a small part to data processing or they are difficult to use. ASaiM provides different tools and programs to process data from raw sequences to functional and taxonomic analyses in complex pipelines. 

The pipeline construction is facilitated by the web interface (link) used to generate a configuration file. This file describes the tools to use, the parameters and the succession of these tools. It is used to run the pipeline with ASaiM. ASaiM connects the different choosen tools by formatting inputs and outputs. 

Running ASaiM
=============

To generate a pipeline, a configuration file in JSON have to be generated, either manually (check out :ref:`configuration-file` for information about the format) or using the web interface (link).

Currently, a pipeline can only be executed on local machine after download and installation of code sources. To install it and its features, check out :ref:`installation`. Execution is then invoked with **make** command from data repository

.. code-block:: bash

   make -f path/to/src/makefile target


What now ?
==========

If you are a user and you want to use ASaiM to process and analyze high throughput data, check out the :ref:`tutorial` and go to :ref:`for-users`.

If you are an curious user or a potential developper and you want to have more information about ASaiM, go to :ref:`for-devs`.

Contributions and Feedback
==========================

Useful links:

- There's a mailing-list for any feedback or question: https://groups.google.com/forum/?hl=fr#!forum/asaim-users
- The repository and issue tracker are on GitHub : https://github.com/asaim

Documentation index
===================

.. toctree::
   :maxdepth: 4

   installation
   tutorial
   for-users/index
   for-devs/index
   faq
   glossary

