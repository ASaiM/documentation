.. _for-devs-pretreatments-quality-control-treatment:

Quality treatment
#################

To improve the sequence quality and limit the bias in downstream analyses, :ref:`the sequences must be treated with (generally) <for-users-pretreatments-quality-control-treatment>`:

- Elimination of sequences having a mean quality score below the defined threshold
- Quality trimming on sequence ends
- Elimination of sequences having a N content higher than the defined threshold
- Reduction of nucleotide frequency bias
- Removal of adapter sequences
- Removal of reads with smaller than a threshold

These treatments can be made with 2 types of sequence quality treatments (:ref:`filtering <for-users-pretreatments-quality-control-treatment-filter>` and :ref:`trimming <for-users-pretreatments-quality-control-treatment-trim>) and several tools. Currently only :ref:`PRINSEQ <for-devs-pretreatments-quality-control-treatment-prinseq>` is available in ASaiM framework.


.. _for-devs-pretreatments-quality-control-treatment-prinseq:
PRINSEQ
=======

.. note::

    Input: sequence file with quality values for each base

    Output: quality treated sequence file

PRINSEQ :cite:`schmieder_quality_2011` is a tool for easy and rapid quality control and data preprocessing of metagenomic and metatranscriptomic datasets.




quality_treatment_with_prinseq_length_min": 60,
                    "quality_treatment_with_prinseq_length_max": null,
                    "quality_treatment_with_prinseq_gc_min": null,
                    "quality_treatment_with_prinseq_gc_max": null,
                    "quality_treatment_with_prinseq_score_min": null,
                    "quality_treatment_with_prinseq_score_max": null,
                    "quality_treatment_with_prinseq_score_mean_min": 15,
                    "quality_treatment_with_prinseq_score_mean_max": null,
                    "quality_treatment_with_prinseq_n_percentage": 2,
                    "quality_treatment_with_prinseq_n_number": null,
                    "quality_treatment_with_prinseq_other_base_filter": false,
                    "quality_treatment_with_prinseq_trim_to_length": null,
                    "quality_treatment_with_prinseq_trim_left": null,
                    "quality_treatment_with_prinseq_trim_right": null,
                    "quality_treatment_with_prinseq_trim_left_percentage": null,
                    "quality_treatment_with_prinseq_trim_right_percentage": null,
                    "quality_treatment_with_prinseq_trim_tail_left": null,
                    "quality_treatment_with_prinseq_trim_tail_right": null,
                    "quality_treatment_with_prinseq_trim_ns_left": null,
                    "quality_treatment_with_prinseq_trim_ns_right": null,
                    "quality_treatment_with_prinseq_trim_qual_left": null,
                    "quality_treatment_with_prinseq_trim_qual_right": 20,
                    "quality_treatment_with_prinseq_trim_qual_type": "mean",
                    "quality_treatment_with_prinseq_trim_qual_rule": "lt",
                    "quality_treatment_with_prinseq_trim_qual_window": 5,
                    "quality_treatment_with_prinseq_trim_qual_step 


.. note::

    Under construction

..     
    Tools
    =====

    Adjustable

    .. _for-devs-pretreatments-quality-control-treatment-prinseq:
    PRINSEQ
    --------

    Tool used to filter, reformat and trim next-generation sequence data. It is particular designed for 454/Roche data, but can also be used for other types of sequence data

    Sickle Tool? Other tools? Citation of PRINSEQ?


    Options and how to choose them
    ==============================

    - Elimination of sequences having a mean quality score below the defined threshold
    - Quality trimming : sliding window over the reads and read trimming when the mean score over the windows is below the defined threshold (window size?)
    - Elimination of sequences having a N proportion higher than the defined threshold
    - Reduction of nucleotide frequency bias?
    - Removal of residual sequencing reads derived from the phiX spike-in control sequences and the adaptor sequences employed : BLAST against a database containing these informations  ? Cross_match (slower but more sensitive than BLAST)?
    - After trimming and adaptor removal, removal of reads with lengths lower than a threshold

    Estimation of the impact of these treatments on sequences : read numbers, histogram of read length, ...


    Not only sequencing, but also data analysis costs money. Analyzing poor data wastes CPU time and interpreting the results from poor data wastes people time. The quality control step often shows that the data needs to be preprocessed before any downstream data analysis. The necessary data preprocessing steps highly depend on the type of library being sequenced (whole genome, transcriptome, 16S, metagenome, ...) and on the type of sequencing technology used to generate the data. The following guide should ensure that the data used for downstream analysis is not compromised of low-quality sequences, sequence artifacts, or sequence contamination that might lead to erroneous conclusions. However, there is no "one-size-fits-all" solution and each user must make informed decisions as to the appropriate parameters used for preprocessing.

    Filter options
    --------------

    Length related
    ~~~~~~~~~~~~~~

    Sequences in the SFF files can be as short as 40 bp (shorter sequences are filtered during signal processing). For multiplexed samples, the MID trimmed sequences can be as short at 28 bp (assuming a 12 bp MID tag). Such short sequences can cause problems during, for example, database searches to find similar sequences. Short sequences are more likely to match at a random position by chance than longer sequences and may therefore result in false positive functional or taxonomical assignments. Furthermore, short sequences are likely to be quality trimmed during the signal-processing step and of lower quality with possible sequencing errors.
    In some cases, sequences can be much longer than several standard deviations above the mean length (e.g. 1,500+ bp for a 500 bp mean length with a 100 bp standard deviation). Those sequences should be used with caution as they likely contain long stretches of homopolymer runs as in the following example. Homopolymers are a known issue of pyrosequencing technologies such as 454/Roche [1].

    A rule of thumb for sequence length thresholds of longer-read datasets is to filter sequences shorter than 60 bp (20 amino acids) and longer than twice the mean length.

    Possibilities: 

    - Filter sequences shorter than a threshold
    - Filter sequences longer than a threshold

    Default: filter sequences shorter than 60 bp

    Quality score related
    ~~~~~~~~~~~~~~~~~~~~~

    In addition to the decrease in quality across the read, regions with homopolymer stretches will tend to have lower quality scores. Huse et al. [1] found that sequences with an average score below 25 had more errors than those with higher averages.
    Low quality sequences can cause problems during downstream analysis. Most assemblers or aligners do not take into account quality scores when processing the data. The errors in the reads can complicate the assembly process and might cause misassemblies or make an assembly impossible.

    Most published thresholds for the sequence mean quality score range from 15 to 25.

    Possibilities

    - Filter sequences with at least one quality score below a threshold
    - Filter sequences with at least one quality score above a threshold 
    - Mean filter

      - Filter sequences with quality score mean below a threshold
      - Filter sequences with quality score mean above a threshold

    Default: Filter sequences with quality score mean below 15

    GC content related
    ~~~~~~~~~~~~~~~~~~

    The GC content distribution of most samples should follow a normal distribution. In some cases, a bi-modal distribution can be observed, especially for metagenomic datasets. This filter is rarely used, but proved useful to separate sequences in a bi-modal distribution.

    Possibilities

    - Filter sequences with GC content below a threshold
    - Filter sequences with GC content above a threshold

    Default: no GC filtering

    Ambiguity code related
    ~~~~~~~~~~~~~~~~~~~~~~

    Sequences can contain the ambiguous base N for positions that could not be identified as a particular base. A high number of Ns can be a sign for a low quality sequence or even dataset. If no quality scores are available, the sequence quality can be inferred from the percent of Ns found in a sequence or dataset. Huse et al. [1] found that the presence of any ambiguous base calls was a sign for overall poor sequence quality.

    Ambiguous bases can cause problems during downstream analysis. Assemblers such as Velvet and aligners such as SHAHA2 or BWA use a 2-bit encoding system to represent nucleotides, as it offers a space efficient way to store sequences. For example, the nucleotides A, C, G and T might be 2-bit encoded as 00, 01, 10 and 11. The 2-bit encoding, however, only allows to store the four nucleotides and any additional ambiguous base cannot be represented. The different programs deal with the problem in different ways. Some programs replace ambiguous bases with a random base (e.g. BWA [2]) and others with a fixed base (e.g. SHAHA2 and Velvet replace Ns with As [3]). This can result in misassemblies or false mapping of sequences to a reference sequence and therefore, sequences with a high number of Ns should be removed before downstream analysis.

    Filtering out all reads containing Ns is only suggested if the loss can be afforded (e.g. high coverage datasets or low number of sequences with ambiguous bases). Filtering reads containing more than 1% of ambiguous bases is advised.

    Possibilities

    - Filter sequences with more than a defined percentage of N
    - Filter sequences with more than a defined number of N 
    - Filter sequences with characters other than A, C, G, T or N

    Default: Filter sequences with more than 2% of N

    Data content related
    ~~~~~~~~~~~~~~~~~~~~

    To select a subset of all sequence in a dataset, the number of wanted sequences can be specified. The first X sequences passing all other specified filters can be selected this way.

    The sequence duplicates can be defined using different methods. Exact duplicates are identical sequence copies, whereas 5' or 3' duplicates are sequences that are identical with the 5' or 3' end of a longer sequence. Considering the double-stranded nature of DNA, duplicates could also be considered sequences that are identical with the reverse complement of another sequence.

    Depending on the dataset and downstream analysis, it should be considered to filter sequence duplicates. The main purpose of removing duplicates is to mitigate the effects of PCR amplification bias introduced during library construction. In addition, removing duplicates can result in computational benefits by reducing the number of sequences that need to be processed and by lowering the memory requirements. Sequence duplicates can also impact abundance or expression measures and can result in false variant (SNP) calling.

    PRINSEQ filters duplicates without allowing mismatches, as artificial duplicates tend to have the same errors and error-models are computationally more expensive. Programs such as cdhit-454 [4] use clustering techniques to identify near identical duplicates. However, those methods tend to miss duplicates identified by PRINSEQ due to the used clustering methods. For best results, duplicates should initially be filtered using PRINSEQ and then optionally using clustering methods.

    For metagenomic datasets, the exact and 5' duplicates should be removed. The 3' and reverse complement duplicates can be removed as they do not provide additional information in database searches, but might be useful for variant discovery or assembly.

    TO DO???

    Sequence complexity related
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~

    Low-complexity sequences are defined as having commonly found stretches of nucleotides with limited information content (e.g. the dinucleotide repeat CACACACACA). Such sequences can produce a large number of high-scoring but biologically insignificant results in database searches. PRINSEQ calculates the sequence complexity using the DUST and Entropy approaches as they present two commonly used examples.

    The DUST approach is adapted from the algorithm used to mask low-complexity regions during BLAST search preprocessing [5]. The scores are computed based on how often different trinucleotides occur and are scaled from 0 to 100. Higher scores imply lower complexity. A sequence of homopolymer repeats (e.g. TTTTTTTTT) has a score of 100, of dinucleotide repeats (e.g. TATATATATA) has a score around 49, and of trinucleotide repeats (e.g. TAGTAGTAGTAG) has a score around 32.

    The Entropy approach evaluates the entropy of trinucleotides in a sequence. The entropy values are scaled from 0 to 100 and lower entropy values imply lower complexity. A sequence of homopolymer repeats (e.g. TTTTTTTTT) has an entropy value of 0, of dinucleotide repeats (e.g. TATATATATA) has a value around 16, and of trinucleotide repeats (e.g. TAGTAGTAGTAG) has a value around 26.

    Sequences with a DUST score above 7 or an entropy value below 70 can be considered low-complexity. An entropy value of 50 or 60 would be a more conservative choice.

    TO DO???

    Trim options
    ------------

    Trim by length/position
    ~~~~~~~~~~~~~~~~~~~~~~~

    Sequences can be trimmed to a specific length or a fixed number of nucleotides can be trimmed from either end.

    Possibilities

    - Trim all sequence from the 3'-end to result in sequence with the defined length
    - Trim sequence at the 5'-end by a defined positions
    - Trim sequence at the 3'-end by a defined positions
    - Trim sequence at the 5'-end by a defined percentage of read length
    - Trim sequence at the 3'-end by a defined percentage of read length

    Default: No trim by length/position

    Trim tails
    ~~~~~~~~~~

    Poly-A/T tails can be trimmed from either end specifying a minimum tail length. All repeats of As or Ts with at least this length will be trimmed from the sequence ends. A small number of tails can occur even after trimming poly-A/T tails. For example, a sequence that ends with AAAAATTTTT and that has been trimmed for the poly-T will still contain the poly-A.

    Trimming poly-A/T tails can reduce the number of false positives during database searches, as long tails tend to align well to sequences with low complexity or sequences with poly-A tails in the database.

    Possibilities:

    - Trim poly-A/T tail with a defined minimum length at the 5'-end
    - Trim poly-A/T tail with a defined minimum length at the 3'-end
    - Trim poly-N tail with a defined minimum length at the 5'-end
    - Trim poly-N tail with a defined minimum length at the 3'-end

    Default: No trim tails

    Trim ends by quality scores
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~

    As for Sanger sequencing, next-generation sequencers produce data with linearly degrading quality across the read. The quality scores for 454/Roche sequencers are Phred-based since version 1.1.03, ranging from 0 to 40. Phred values are log-scaled, where a quality score of 10 represents a 1 in 10 chance of an incorrect base call and a quality score of 20 represents a 1 in 100 chance of an incorrect base call.

    Sequences can be trimmed from either end using different rules applied to a sliding window. To stop at the first base that fails the rule defined, use a window size of 1. A bigger window size can trim sequences that might contain a high quality score in between low quality scores without stopping at the high quality score. To move the sliding window over all quality scores without missing any, the step size should be less or equal to the window size.

    The quality trimming during the signal processing step (see Raw data processing PDF file) may not be sufficient. Trimmed sequences can end with low quality bases or even with ambiguous base N (approx. 1%). Reads with RLMIDs (Rapid library multiplex identifiers) may be trimmed in high quality regions as the default behavior will cause the reads to be trimmed at the first position the MID sequence matches, even if it is not the MID but a natural occurring match inside the read.

    The parameters should be set to trim positions with a quality score below 20.

    Possibilities

    - Trim sequence by quality score from the 5'- and/or 3'-end with a defined threshold score
    - Different type of quality score calculation to use (minimum, mean, maximal and sum)
    - Different rules to use to compare quality score to calculated value (less than [lt], greater than [gt] and equal to [et])
    - Adjustable sliding window size used to calculate quality score by type. To stop at the first base that fails the rule defined, use a window size of 1.
    - Adjustable step size used to move the sliding window. To move the window over all quality scores without missing any, the step size should be less or equal to the window size.

    Default: trim sequence by quality score from the 3'-end with a mean score on a 5 bp sliding window (and 5 step size) below a quality of 20


.. rubric:: References

.. bibliography:: ../../../../references.bib
   :cited:
   :style: plain
   :filter: docname in docnames

       