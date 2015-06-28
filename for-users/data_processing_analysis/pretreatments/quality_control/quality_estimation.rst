.. _for-users-pretreatments-quality-control-estimation:

Quality estimation
##################

To estimate sequence quality and treatments to do, many indicators can be checked:

- :ref:`Sequence length <for-users-pretreatments-quality-control-estimation-length>`
- :ref:`Base quality <for-users-pretreatments-quality-control-estimation-quality>`
- :ref:`Base content <for-users-pretreatments-quality-control-estimation-base-content>`
- :ref:`Sequence duplication <for-users-pretreatments-quality-control-estimation-seq-duplication>`
- :ref:`Sequence complexity <for-users-pretreatments-quality-control-estimation-seq-complexity>`
- :ref:`Tag sequence <for-users-pretreatments-quality-control-estimation-tag-sequences>`
- :ref:`Sequence contamination <for-users-pretreatments-quality-control-estimation-seq-contamination>`

. These indicators are controlled with :ref:`available tools <for-devs-pretreatments-quality-control-estimation>` in ASaiM framework to estimate sequence quality.

.. _for-users-pretreatments-quality-control-estimation-length:

Length of sequences
===================

Some high throughput sequencers generate sequence fragments of uniform length, but others can contain reads of wildly varying lengths. The length distribution can be then used as quality measure. You would expect a normal distribution for the best result. However, most sequencing results show a slowly increasing and then a steep falling distribution. 

.. _for-users-pretreatments-quality-control-estimation-quality:

Base qualities
==============

Low quality sequences can cause problems during downstream analysis. Most assemblers do not take into account quality scores when processing the data. The errors in the reads can complicate the assembly process and might cause misassemblies or make an assembly impossible.

During the sequencing, for each infered nucleotide, is computed an error probability for misidentification. This probability is transformed in a quality score ranging from 0 to 40, with 40 being the lower error probability. This quality score can be visualised through different point of view.

In addition to the decrease in quality across the read, regions with homopolymer stretches will tend to have lower quality scores. Therefore, it is helpful to take a look at the average (or mean) quality scores. PRINSEQ provides a plot that shows the distribution of sequence mean quality scores of a dataset, as shown below. The majority of the sequences should have high mean quality scores.

Per sequence quality score
--------------------------

The per sequence quality score report allows to see if a subset of your sequences have universally low quality values. It is often the case that a subset of sequences will have universally poor quality, often because they are poorly imaged (on the edge of the field of view etc), however these should represent only a small percentage of the total sequences. Huse et al. [1] found that sequences with an average score below 25 had more errors than those with higher averages.

Per base sequence quality
-------------------------

This plot is helpful to identify quality scores at the end of longer reads, which would otherwise be grouped with the ends of the shorter reads. The sequences with low quality scores at the ends should be trimmed during data preprocessing.

There is a general degradation of quality over the duration of long runs. In general sequencing chemistry degrades with increasing read length and for long runs you may find that the general quality of the run falls to a level where a warning or error is triggered. 
If the quality of the library falls to a low level then the most common remedy is to perform quality trimming where reads are truncated based on their average quality. For most libraries where this type of degradation has occurred you will often be simultaneously running into the issue of adapter read-through so a combined adapter and quality trimming step is often employed. 
Another possibility is that a warn / error is triggered because of a short loss of quality earlier in the run, which then recovers to produce later good quality sequence. This can happen if there is a transient problem with the run (bubbles passing through a flowcell for example). You can normally see this type of error by looking at the per-tile quality plot (if available for your platform). In these cases trimming is not advisable as it will remove later good sequence, but you might want to consider masking bases during subsequent mapping or assembly. 
If your library has reads of varying length then you can find a warning or error is triggered from this module because of very low coverage for a given base range. Before committing to any action, check how many sequences were responsible for triggering an error by looking at the sequence length distribution module results. 

Per tile sequence quality
-------------------------

In Illumina library, the original sequence identifiant is retained.Encoded in these is the flowcell tile from which each read came.

There could be transient problems such as bubbles going through the flowcell, or they could be more permanent problems such as smudges on the flowcell or debris inside the flowcell lane. 

.. _for-users-pretreatments-quality-control-estimation-base-content:

Base content
============

To estimate sequencing quality, we also need to check base content.

Per sequence GC content
-----------------------

The GC content distribution of most samples should follow a normal distribution. In some cases, a bi-modal distribution can be observed, especially for metagenomic data sets. An unusually shaped distribution could indicate a contaminated library or some other kinds of biased subset. A normal distribution which is shifted indicates some systematic bias which is independent of base position. If there is a systematic bias which creates a shifted normal distribution then this won't be flagged as an error by the module since it doesn't know what your genome's GC content should be. 
 
Issues in the GC content distribution usually indicate a problem with the library. Sharp peaks on an otherwise smooth distribution are normally the result of a specific contaminant (adapter dimers for example), which may well be picked up by the overrepresented sequences module. Broader peaks may represent contamination with a different species. 

Per base sequence content
-------------------------

Per Base Sequence Content checks out the proportion of each base position in a sequence file for which each of the four normal DNA bases has been called.  In a random library there would be little to no difference between the different bases of a sequence run. The relative amount of each base should reflect the overall amount of these bases, but in any case they should not be hugely imbalanced from each other. 
It's worth noting that some types of library will always produce biased sequence composition, normally at the start of the read. Libraries produced by priming using random hexamers (including nearly all RNA-Seq libraries) and those which were fragmented using transposases inherit an intrinsic bias in the positions at which reads start. This bias does not concern an absolute sequence, but instead provides enrichement of a number of different K-mers at the 5' end of the reads. Whilst this is a true technical bias, it isn't something which can be corrected by trimming and in most cases doesn't seem to adversely affect the downstream analysis. It will however produce a warning or error in this module. 

There are a number of common scenarios for these issues:

- Overrepresented sequences: If there is any evidence of overrepresented sequences such as adapter dimers or rRNA in a sample then these sequences may bias the overall composition and their sequence will emerge from this plot. 
- Biased fragmentation: Any library which is generated based on the ligation of random hexamers or through tagmentation should theoretically have good diversity through the sequence, but experience has shown that these libraries always have a selection bias in around the first 12bp of each run. This is due to a biased selection of random primers, but doesn't represent any individually biased sequences. Nearly all RNA-Seq libraries will fail this module because of this bias, but this is not a problem which can be fixed by processing, and it doesn't seem to adversely affect the ablity to measure expression. 
- Biased composition libraries: Some libraries are inherently biased in their sequence composition. The most obvious example would be a library which has been treated with sodium bisulphite which will then have converted most of the cytosines to thymines, meaning that the base composition will be almost devoid of cytosines and will thus trigger an error, despite this being entirely normal for that type of library 
- If you are analysing a library which has been aggressivley adapter trimmed then you will naturally introduce a composition bias at the end of the reads as sequences which happen to match short stretches of adapter are removed, leaving only sequences which do not match. Sudden deviations in composition at the end of libraries which have undergone aggressive trimming are therefore likely to be spurious.

Ambiguous bases or Per base N content
-------------------------------------

Sequences can contain the ambiguous base N for positions that could not be identified as a particular base. A high number of Ns can be a sign for a low quality sequence or even dataset. If no quality scores are available, the sequence quality can be inferred from the percent of Ns found in a sequence or dataset. Ambiguous bases can cause problems during downstream analysis, particularly with assemblers such as Velvet.

If a sequencer is unable to make a base call with sufficient confidence then it will normally substitute an N rather than a conventional base call. 
It's not unusual to see a very low proportion of Ns appearing in a sequence, especially nearer the end of a sequence. However, if this proportion rises above a few percent it suggests that the analysis pipeline was unable to interpret the data well enough to make valid base calls. 

The most common reason for the inclusion of significant proportions of Ns is a general loss of quality, so the results of this module should be evaluated in concert with those of the various quality modules. 
Another common scenario is the incidence of a high proportions of N at a small number of positions early in the library, against a background of generally good quality. Such deviations can occur when you have very biased sequence composition in the library to the point that base callers can become confused and make poor calls. This type of problem will be apparent when looking at the per-base sequence content results.

.. _for-users-pretreatments-quality-control-estimation-seq-duplication:

Sequence duplication
====================

In genomic projects, sequence duplication is investigated. Duplicated car arise when there are too few fragments present at any stage prior to sequencing. However, in metagenomic and even more in metatranscriptomic sequences are duplicated sequences. So it seems difficult to distinguish in such datasets between real and artificial duplicates

.. _for-users-pretreatments-quality-control-estimation-seq-complexity:

Sequence complexity
===================

Sequences can exhibit low-complexity parts, which are defined as having commonly found stretches of nucleotides with limited information content (e.g. the dinucleotide repeat CACACACACA). Such sequences can introduce bias in database searches with a large number of high-scoring but biologically insignificant results. Many different approaches can be used to estimate the sequence complexity.

The DUST approach is adapted from the algorithm used to mask low-complexity regions during BLAST search preprocessing [6]. The scores are computed based on how often different trinucleotides occur and are scaled from 0 to 100. Higher scores is, lower complexity is. Sequences with complexity scores above 7 can be considered as low-complexity sequences. For examples, a sequence of homopolymer repeats (e.g. TTTTTTTTT) has a score of 100, of dinucleotide repeats (e.g. TATATATATA) has a score around 49, and of trinucleotide repeats (e.g. TAGTAGTAGTAG) has a score around 32.

The Entropy approach evaluates the entropy of trinucleotides in a sequence. The entropy values are scaled from 0 to 100 and lower entropy values imply lower complexity. For example, a sequence of homopolymer repeats (e.g. TTTTTTTTT) has an entropy value of 0, of dinucleotide repeats (e.g. TATATATATA) has a value around 16, and of trinucleotide repeats (e.g. TAGTAGTAGTAG) has a value around 26. Sequences with an entropy value below 70 can be considered low-complexity.

.. _for-users-pretreatments-quality-control-estimation-tag-sequences:

Tag sequences
=============

Tag sequences are artifacts at the ends of sequence reads such as multiplex identifiers, adapters, and primer sequences that were introduced during pre-amplification with primer-based methods. The base frequencies across the reads present an easy way to check for tag sequences. If the distribution seems uneven (high frequencies for certain bases over several positions), it could indicate some residual tag sequences. This doesn't indicate a problem as such - just that the sequences will need to be adapter trimmed before proceeding with any downstream analysis. 

An other way is to look at kmer content and find those which do not have even coverage through the length of your reads and could correspond to tag sequences.  

.. _for-users-pretreatments-quality-control-estimation-seq-contamination:

Sequence contamination
======================

One way to identify possible sequence contamination is to look at dinucleotide odds ratios. Dinucleotide abundances have been shown to capture the majority of variation in genome signatures and can be used to compare a metagenome to other microbial or viral metagenomes. Principal component analysis (PCA) is then used to group metagenomes from similar environments based on dinucleotide abundances. This can help to investigate if the correct sample was sequenced, as viral and microbial metagenomes show distinct patterns. Anomalies in the odds ratios can also be used to identify discrepancies in metagenomes such as human DNA contamination (depression of the CG dinucleotide frequency).
   