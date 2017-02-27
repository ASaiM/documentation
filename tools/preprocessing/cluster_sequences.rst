.. _framework-tools-preprocessing-cluster:

=================
Cluster sequences
=================

.. _framework-tools-preprocessing-cluster-cdhit:

CD-Hit
######

CD-HIT :cite:`fu_cd-hit:_2012,li_cd-hit:_2006` stands for Cluster Database at High Identity with Tolerance. The program (cd-hit) takes a fasta format sequence database as input and produces a set of 'non-redundant' (nr) representative sequences as output. In addition cd-hit outputs a cluster file, documenting the sequence 'groupies' for each nr sequence representative. The idea is to reduce the overall size of the database without removing any sequence information by only removing 'redundant' (or highly similar) sequences. This is why the resulting database is called non-redundant (nr). Essentially, cd-hit produces a set of closely related protein families from a given FastA sequence database

CD-HIT requires a FastA file as input with protein for CD-HIT PROTEIN, with nucleotide for CD-HIT EST.

CD-HIT generates two output file. The first one is a FastA file containing representative sequences. The second one is a text file listing the mapping of sequences to the representative sequences::

    >Cluster 0
    0 2799aa, >PF04998.6|RPOC2_CHLRE/275-3073... *
    >Cluster 1
    0 2214aa, >PF06317.1|Q6Y625_9VIRU/1-2214... at 80%
    1 2215aa, >PF06317.1|O09705_9VIRU/1-2215... at 84%
    2 2217aa, >PF06317.1|Q6Y630_9VIRU/1-2217... *
    3 2216aa, >PF06317.1|Q6GWS6_9VIRU/1-2216... at 84%
    4 527aa, >PF06317.1|Q67E14_9VIRU/6-532... at 63%
    >Cluster 2
    0 2202aa, >PF06317.1|Q6UY61_9VIRU/8-2209... at 60%
    1 2208aa, >PF06317.1|Q6IVU4_JUNIN/1-2208... *
    2 2207aa, >PF06317.1|Q6IVU0_MACHU/1-2207... at 73%
    3 2208aa, >PF06317.1|RRPO_TACV/1-2208... at 69%

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
