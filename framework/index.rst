.. _framework:

ASaiM framework 
###############

Processing and analysis of gut microbiota data is a complex process with numerous steps:

1. Quality control
2. (Assembly of sequences)
3. Sort of interesting sequence
4. Functional annotation
5. Taxonomic analysis
6. Comparative analysis

To achieve this task, the developed framework must fill the following requirements:

- Generating workflows to process gut microbiota data. Check out the :ref:`workflow generation <framework-workflow>`.
- Having standardized outputs which can be incorporated to the database
- Being easy to use. Check out the :ref:`user manual <framework-use>`
- Being heavily documented
- Being flexible with the tools, the parameters, ... to process specific datasets while keeping standardized outputs
- Being executable on cluster and on local computer
- Being well written to be maintainable

Several conceptions were tested before choosing the actual :ref:`conception of the framework <framework-conception>`, based
on a Galaxy instance.

.. toctree::
    :maxdepth: 2

    conception
    tutorial
    installation
    use
    tools/index
    databases/index
    workflows/index

