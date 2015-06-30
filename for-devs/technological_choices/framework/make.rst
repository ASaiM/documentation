.. _for-devs-make:

Make
####

To execute the generated pipeline, :ref:`Docker and data containers <.. _for-devs-docker:>` are used. Their build and run are facilitated with a ``makefile``. Several commands are possible which must be executed from the data repository:

    ``make -f /path/to/src/code/makefile run_pipeline``
        To execute the generated pipeline

    ``make cog``
        To construct the data container with :ref:`cog database <for-devs-databases-COG>`

    ``make -f /path/to/src/code/makefile extract_interesting_module_sequences``
        To :ref:`extract sample sequences corresponding the interesting modules <>`

    ``make -f /path/to/src/code/makefile extract_interesting_pathway_sequences``
        To :ref:`extract sample sequences corresponding the interesting pathways <>`

    ``make clean``
        To remove unused docker containers and images
