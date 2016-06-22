.. _framework-use:

Usage
=====

ASaiM framework is based on a Galaxy instance working as any other Galaxy instance: tools on left panel, history with job execution on right panel, workflows on top panel, etc.

.. _framework_custom_galaxy_instance:

.. figure:: /assets/images/framework/galaxy_instance.png
    :align: center

    Screenshot of the custom Galaxy instance of ASaiM framework

The customization of this Galaxy instance comes from the selected tools and built workflwows, and also its easy deployment.

Before :ref:`deploying the custom Galaxy instance <framework-use-launch>`, the environment must be :ref:`configure <framework-use-configure>` for Galaxy. And, after deployment, the custom Galaxy instance will run as background task and need a manual intervention to :ref:`stop it<framework-use-stop>` and :ref:`clean Galaxy <framework-use-clean>`.

.. _framework_use_virtual_circle:

.. figure:: /assets/images/framework/usage/virtual_circle.png
    :align: center

    Virtual circle to get ASaiM framework correctly running

:ref:`Selected tools <framework-tools>` are automatically installed in Galaxy instance using an Ansible playbook. If you want to add more, :ref:`checkout how to add tools and workflows from ToolShed <framework-use-add-tools>`.

.. _framework-use-configure:

Configure Galaxy environment
############################

PostgreSQL is used to manage databases in Galaxy. It must be launched as a background task and setup for Galaxy (new database and user creation).

On the other hand, a FTP server with ``proftpd`` has to be configured and launched.

All the configuration tasks (postgresql and proftpd) can be done by running:

.. code-block:: bash

    $ ./src/configure.sh


.. _framework-use-launch:

Launch ASaiM framework
######################

To launch the custom Galaxy instance and populate it with dedicated tools and databases :

.. code-block:: bash

    $ ./src/launch_asaim.sh

This task, particularly tool population, can take several hours.

However, once tool population starts, the Galaxy instance can be then browse on `http://127.0.0.1:8080/ <http://127.0.0.1:8080/>`_. And after registration with admin account (email: `asaim-admin@asaim.com`), you can follow tool installation in `Admin` -> `Manage installed tools`.

After installation of the tools, HUMAnN2 databases have to be downloaded (once). It can be done using the dedicated tool available in `STRUCTURAL AND FUNCTIONAL ANALYSIS TOOLS` -> `Analyze metabolism` -> `Download HUMAnN2 databases`. This tool have to be executed twice: once for nucleotide (ChocoPhlAn) database and once for protein (UniRef50) database.

.. _framework-use-add-workflows:

Add workflows
#############

Workflows are not automatically added to the Galaxy instance.

To add them (after tool population):

- Go to `Workflow` menu (top panel)
- Click on `Upload or import workflows` (on top right)
    - Paste the following URL (one at a time) in "Galaxy workflow URL" field
        - Main workflow: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_main_workflow.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_main_workflow.ga>`_
        - Comparative analysis workflows:
            - For taxonomic results: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomic_result_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomic_result_comparative_analysis.ga>`_
            - For functional results (gene families or pathways): `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_functional_result_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_functional_result_comparative_analysis.ga>`_
            - For GO slim terms: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_go_slim_terms_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_go_slim_terms_comparative_analysis.ga>`_
            - For taxonomically-related functional results: `https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomically_related_functional_result_comparative_analysis.ga <https://raw.githubusercontent.com/ASaiM/galaxytools/master/workflows/asaim/asaim_taxonomically_related_functional_result_comparative_analysis.ga>`_
    - Click on `Import`
- Do it again with other workflows


.. _framework-use-add-tools:

Add tools from ToolShed to the custom Galaxy instance
#####################################################

To add tools from ToolShed, you can also add reference to this tool in files in `data/chosen_tools` and then launch:

.. code-block:: bash

    $ ./src/prepare_asaim/populate_galaxy.sh

Alternatively, you can use the web interface and add other tools via ToolShed.
Once register, you go in `Admin` (tool panel) and then `Search Tool Shed` (left panel). You choose which ToolShed to browse, search the wanted tool on the ToolShed, click on it to get `Preview and install` and then on `Install to Galaxy` (on top), choose in which tool section adding it and then click on `Install`.

.. _framework-use-stop:

Stop ASaiM framework
####################

The custom Galaxy instance runs as a background task. Stopping it needs a manual intervention:

.. code-block:: bash

    $ ./src/stop_galaxy.sh


.. _framework-use-clean:

Clean Galaxy environment
########################

When Galaxy instance is configure and launched, a database and several directories are created. They can be cleared after usage with:

.. code-block:: bash

    $ ./src/clean_asaim.sh
