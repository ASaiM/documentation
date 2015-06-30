.. _for-devs-configuration-file:

Configuration file
##################

A generated pipeline and its description (tools and parameters) is saved in a configuration file in JSON format. This format allow an hierarchy similar to the one found in code architecture or in the documentation. 

Then, a configuration file (save in ``config_file.json`` file) is constructed given the following scheme:

.. code-block:: none

   {
    "input_filepath": ["R1_sequences.fastq","R2_sequences.fastq"],

    "pretreatments": {
        "execute_pretreatments": true,
        "quality_control": {
            "execute_quality_control": true,
            "quality_estimation": {
                "execute_quality_estimation": true,
                "fastqc": {
                    "execute_quality_estimation_with_fastqc": true,
                    ...
                    <parameters>
                    ...
                },
                ...
            },
            "quality_treatment":{
                "execute_quality_treatment": true,
                "prinseq":{
                    "execute_quality_treatment_with_prinseq": true,
                    ...
                    <parameters>
                    ...
                },
                ...
            },
            ...            
        },
        "paired_end_assembly":{
            "execute_paired_end_assembly": true,
            "fastq_join":{
                "execute_paired_end_assembly_with_fastq_join": true,
                ...
                <parameters>
                ...
            },
            ...            
        },
        "rna_sorting":{
            "execute_rna_sorting": true,
            "sort_me_rna":{
                "execute_rna_sorting_with_sort_me_rna": true,
                ...
                <parameters>
                ...
            },
            ...
        }
    },

    "taxonomic_assignation":{
        "execute_non_rRNA_taxonomic_assignation": true,
        "metaphlan":{
            "execute_non_rRNA_taxonomic_assignation_with_metaphlan": true,
            ...
            <parameters>
            ...
        },
        ...        
    },

    "functional_assignation": {
        "execute_functional_assignation": true,
        "protein_ncrna_db_search":{
            "execute_protein_ncrna_db_search": true,
            "blast":{
                "execute_protein_ncrna_db_search_with_blast": true,
                ...
                <parameters>
                ...
            },
            ...
        },
        "humann":{
            "execute_functional_assignation_with_humann": true
            ...
            <parameters>
            ...
        },
        ...
    }

   }

Each module and submodule is then checked and execute if ``execute_module`` is ``True``. This describes then the pipeline and treatment plumbing.

The parameters of a tool can be modified, their names are given in the description of the tool (check at :ref:`tool description <for-devs-framework-tools>`).

Any word different from the one used in these manual are not take into account.