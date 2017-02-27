.. _framework-tutorial-transform:

Transform the history of tool execution into a workflow
=======================================================

The whole analysis process is complex and error-prone. Indeed, if you want to
analyze a new dataset with same analysis process, you need to reconfigure each
tool with correct input, correct parameters, correct databases, ...

To enhance reproducibility, workflows can be generated and shared inside a 
Galaxy environment. Workflows model data flow between several tools and processes.
Their use is :ref:`intuitive <framework-workflow-usage-run>`. They can be 
:ref:`built <framework-workflow-usage-construction>` from scratch or from an 
history.

In our case, we have processed a dataset with several step. We want to extract
the corresponding workflow to reproduce analyses in a new dataset, for example.

To use workflow, you need to be registered on the instance (top panel):

.. _register:

.. figure:: /assets/images/framework/tutorial/register.png

Registration is only local (you could use whatever id and password).

Then to extract workflow from history, you click on `History options` on right 
panel and then on `Extract workflow`. It will fill central panel with workflow
steps and attributes:

.. _worfklow_extraction:

.. figure:: /assets/images/framework/tutorial/worfklow_extraction.png

You can then modify workflow name and create it. It will then appear in `Workflow`
section, accessible from top panel. You can then edit, share, ... it

.. _extracted_worfklow:

.. figure:: /assets/images/framework/tutorial/extracted_workflow.png
