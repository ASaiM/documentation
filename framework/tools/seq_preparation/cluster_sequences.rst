.. _framework-tools-available-seq-prep-cluster:

=================
Cluster sequences 
=================

.. _framework-tools-available-seq-prep-cluster-cdhit:

CD-Hit
######

CD-HIT :cite:`fu_cd-hit:_2012,li_cd-hit:_2006` stands for Cluster Database at High Identity with Tolerance. The program (cd-hit) takes a fasta format sequence database as input and produces a set of 'non-redundant' (nr) representative sequences as output. In addition cd-hit outputs a cluster file, documenting the sequence 'groupies' for each nr sequence representative. The idea is to reduce the overall size of the database without removing any sequence information by only removing 'redundant' (or highly similar) sequences. This is why the resulting database is called non-redundant (nr). Essentially, cd-hit produces a set of closely related protein families from a given fasta sequence database


.. _framework-tools-available-seq-prep-cluster-format:

Format cd-hit outputs 
#####################

This tool format cd-hit outputs (cluster information and cluster representative sequences) to rename representative sequences with cluster name and/or extract category distribution inside clusters given a mapping file.

The tool takes as input:

 - The cd-hit output file with cluster information
 - The cd-hit output file with representative sequences for each cluster (optional)
 - A mapping file in tabular format with first column being the sequence names (corresponding to the ones in cluster information file) and the second column being the corresponding categories (optional)

The tool generates different outputs given chosen parameters:

 - A file with representative sequences of each cluster named with the cluster name
 - A tabular file with lines corresponding to clusters, columns to categories (and one column with sequence number in the cluster), and cases to number of sequences of the given category in the cluster

.. rubric:: References

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames