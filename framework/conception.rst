.. _framework-conception:

==========
Conception 
==========

Analyses of gut microbiota sequences are complex and involve numerous steps:

1. Quality control
2. (Assembly of sequences)
3. Sort of interesting sequence
4. Functional annotation
5. Taxonomic analysis
6. Comparative analysis

These analyses can be helped with a dedicated framework which must fill the following requirements:

- Generating workflows to process gut microbiota data. Check out the :ref:`workflow generation <framework-workflow>`.
- Having standardized outputs which can be incorporated to the database
- Being easy to use. Check out the :ref:`user manual <framework-use>`
- Being heavily documented
- Being flexible with the tools, the parameters, ... to process specific datasets while keeping standardized outputs
- Being executable on cluster and on local computer
- Being well written to be maintainable

Several conceptions were tested to develop the framework and worflow management that fit with requirements

- Basic one with Python scripts calling tools: not formal, first draft, first try to understand conception complexity
- Several workflow tool managers (Airflow from Airbnb, Luigi from Spotify, Cloudslang, ...): not convenient for flexibility in worflow conception (dependencies between the tasks)
- Home-made workflow manager in Python based on configuration file and scripts: more formal and closer to needed conception but difficulties in task dependencies and worflow management
- Galaxy (current one): worflow manager relying on output/input dependencies (better model of the data flow for meta-omic data processing)

Despite several cons, Galaxy was choosen as tool and workflow management. Then, ASaiM framework is based on a light Galaxy instance dedicated to process gut microbiota datawith selected tools, workflows and databases.