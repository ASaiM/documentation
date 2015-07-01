.. _for-devs-misc-sequence-similarity-report-manipulation:

Manipulation of sequence similarity report files
################################################

Handled formats
===============

Different sequence similarity report format can be managed automatically. However, currently, only Blast tabular output format (corresponding to **outfmt 6** option for **Blast** command-line application) is managed.

For each handled format, information type found in the sequence similarity report is managed with its data type. For example, a file in Blast tabular output format has 12 columns corresponding to:

- query name (``string``)
- target name (``string``)
- identity percentage (``float``)
- alignment length (``int``)
- mismatch number (``int``)
- open gap number (``int``)
- query start position (``int``)
- query end position (``int``)
- target start position (``int``)
- target end position (``int``)
- e-value (``float``)
- bit score (``float``)

Before any extraction or treatment of sequence similarity report file, the format of sequence similarity report file is tested for column number, information format, ...
Each information in similarity report found in a file is formatted given its data type.

Extraction from similarity report files
=======================================

Similarity reports can be extracted from files to be analyzed, processed, ... 

The extraction can be constrained. For example, we may want only similarity reports with a identity percentage inferior to 97%. For each possible information (except ``string`` information), six constraint types are possible (equal, different, inferior, strictly inferior, superior or strictly superior) and can be combined (identity percentage superior to 65% but inferior to 97%).

Extracted similarity report information can be then reduced to only interesting information (only query name, for example).  

.. note::

   Code path: ``src/misc/sequence_similarity_report_manipulation.py``
