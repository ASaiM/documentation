.. _framework-tools:

Tools 
=====

Several tools populate the Galaxy instance. And to conserve the idea of an Galaxy 
instance dedicated to analyses of gut microbiota data, the conserved tools were 
carefully choosen. 

Most of the common tools are coming from standard Galaxy instance. But specific 
tools such as the one dedicated to specific tasks are automatically imported from 
the `Galaxy Tool Shed <https://toolshed.g2.bx.psu.edu/>`_. However, wrappers of 
some of these tools were not complete (lack of some parameters, for example) and 
some wanted tools were not integrated in the  or `Galaxy Tool Shed <https://toolshed.g2.bx.psu.edu/>`_. 
Several wrappers were then developed and integrated in the 
`test Galaxy Tool Shed <https://testtoolshed.g2.bx.psu.edu>`_. The corresponding 
source code are available in a `dedicated GitHub repository <https://github.com/ASaiM/galaxytools>`_.

To help analyses of microbiota data, the available tools are organised in section 
and subsection. This organisation follow the recommended order to process metagenomic 
or metatranscriptomic sequences of gut microbiota.

.. toctree::
    :maxdepth: 2

    usage
    common_tools/index
    pretreatments/index
    taxonomic_assignation/index
    functional_assignation/index
    post_treatments/index

    

