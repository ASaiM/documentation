.. _framework-workflow:

Workflows
=========

To orchestrate tools and help users with their analyses, several workflows populate ASaiM framework. They formally orchestrate tools in a defined order and with defined parameters, but they are customizable (tools, order, parameters).

The :ref:`main workflow <framework-workflows-analyses-microbiota-sequences>` processes from raw sequences to produces accurate and precise taxonomic assignations, multi-level functional results and taxonomically-related metabolism information, in few hours on a commodity computer.

Other workflows are also proposed for comparative analyses.

Workflows are not automatically added to the Galaxy instance. Check out :ref:`how to add them <framework-use-add-workflows>`.

.. toctree::
    :maxdepth: 2

    usage
    microbiota_data_analyses
    comparative_analyses
