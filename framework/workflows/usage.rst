.. _framework-workflow-usage:

Usage of workfows in a Galaxy instance 
======================================

To use/generate a workflow, you need to be registered on the instance (top panel). Registration is only local (you could use whatever id, password).

All workflows (build and automatically added ones) are available from 'Workflow' in the top panel.

.. _workflow_panel:

.. figure:: /assets/images/framework/workflows/workflow_panel.png

   Workflow panel in a Galaxy instance

Run a workflow
##############

Before running a workflow, datasets needed in the workflow have to uploaded on Galaxy instance (using 'Get Data' -> 'Upload file' in 'Common Tools' section on the left panel).

To run a defined workflow, you need to go in 'Workflow' in the top panel. When you chosed your workflow, you click on it and you click on 'Run'. A new window will open:

.. figure:: /assets/images/framework/workflows/running_workflow.png

   Panel to choose input datasets for workflows

You can then choose input datasets and then click on 'Run workflow'. All steps in the workflow will be launched in the current history (on the right panel)

Construction of a workflow
##########################

A workflow in a Galaxy instance is easy to build either from an history of data processing or from scratch.

From an history
---------------

You applied several tools and treatments on your data and you want to extract the corresponding workflow to keep a track. It is easy. From your history (with all your processing steps), you click on 'History option' (on top of right panel) and then on 'Extract workflow'

.. figure:: /assets/images/framework/workflows/workflow_extraction.png

   How to extract a workflow from an history?

A new panel will open where you choose workflow name and steps to conserve

.. figure:: /assets/images/framework/workflows/workflow_extraction_2.png

   Workflow description when extracted from an history

From scratch
------------

To build a workflow from scratch, you have to go on :ref:`workflow panel <_workflow_panel>` and click on 'Create a new workflow'. It will open a new panel to enter workflow description (name and annotation) and then the Galaxy workflow editor:

.. figure:: /assets/images/framework/workflows/workflow_editor.png

   Galaxy workflow editor

On the left panel, you could find all available tools and also workflows. The right panel displays parameters for a tool. On the central panel, the workflow with the data flow is displayed.

To add tools (or workflows), you click on them on the left panel and they will be added on the central panel. You can connect inputs and outputs to model the data flow. Input dataset have to added using 'Inputs' -> 'Input dataset'. 

When needed, the workflow can be saved using the menu on top right of the central panel.
