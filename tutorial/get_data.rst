.. _framework-tutorial-get-data:

Get the data
============

To illustrate why and how to use ASaiM framework on microbiota sequences, a 
dataset of metagenomic sequences from an lean human is used. The data are coming 
from a study on core gut microbiome in obese and lean twins :cite:`turnbaugh_core_2009`, 
available on `EBI metagenomic <https://www.ebi.ac.uk/metagenomics/projects/SRP000319>`_. 
We chosed data from 
`Patient TS1 <https://www.ebi.ac.uk/metagenomics/projects/SRP000319/samples/SRS000998/runs/SRR029687/results/versions/1.0>`_ 
(lean woman). Raw data are available 
`here <ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR029/SRR029687/SRR029687.fastq.gz>`_. 

These data were also analyzed with `EBI metagenomic <https://www.ebi.ac.uk/metagenomics/about>`_. 
Our quality control, taxonomic and functional analyses results can be compared to 
the `one obtained by EBI metagenomic workflow <https://www.ebi.ac.uk/metagenomics/projects/SRP000319/samples/SRS000998/runs/SRR029687/results/versions/1.0>`_.

You can also take your own dataset (paired-end or not) of microbiota data. 

The chosen dataset has to be uploaded in Galaxy environment with `Get Data` -> `Upload 
file` in `Common tools` section in left panel of Galaxy interface. 

.. _get_data:

.. figure:: /assets/images/framework/tutorial/get_data.png

Several download options are proposed

    * direct upload, for files < 2 Gb
    * FTP upload, required for files > 2 Gb

The downloaded file will then be visible inside right panel (`History`)

.. _upload_data:

.. figure:: /assets/images/framework/tutorial/upload_data.png

This right panel will concentrate all files (input files, output files and any
intermediary files). In this panel, you can also "follow" execution of a task.
When a task is launched, the expected output files will be visible on the right
panel, in orange boxes. When the task is done, the output file
boxes will become green or red in case of execution error.