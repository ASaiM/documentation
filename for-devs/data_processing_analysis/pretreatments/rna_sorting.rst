.. _for-devs-pretreatments-rna-sorting:
RNA sorting
###########

.. note::

    Under construction

..
    BLAST (bit score >50) against a database of rRNA sequences constructed from the All-species Living Tree Project SSU database, ASF SSU sequences and 5S and LSU sequences [62] representative of intestinal microbes

    Tools
    =====

    2 steps

    - BLASTN against LSU and SSU ribosomal RNA databases from the ARB-Silva database (E-values inferior or equal to 10:sup:`-5`, bit score superior or equal to 52 and overlap superior or equal to 50 bp)
    - rRNA-hmm and tRNA-scan programs in the Rammcap package (default setting)

    2 iterative steps

    - SortMeRNA softare using the dafult rRNA database included in the software package (which are? update?)
    - BLASTN on the remaining reads using a filtering database consisting of complete ribosomal RNA loci, and tRNA sequences of bacteria, archeae and eukaryota taken from the NCBI and SILVA databases (database? taxonomic affiliation? minimum alignment bit score (54)?)


    Removal of potential host contaminant RNA

    Removal of human RNA (for example)

    Mapping (BLASTX??) of potential mRNA transcript on: 1) database of human derived transcripts (Ensemble); 2) the human genome; and 3) a database of 1078 bacterial genomes downloaded from the NCBI, using the software tool BWA [37]

    SortMeRNA
    ---------

    SortMeRNA is a local sequence alignment tool for filtering, mapping and OTU-picking. The core algorithm is based on approximate seeds and allows for fast and sensitive analyses of NGS reads. The main application of SortMeRNA is filtering rRNA from metatranscriptomic data. Addi- tional applications include OTU-picking and taxonomy assignation available through QIIME v1.9+ (http://qiime.org, currently the development version to be released in early December). Sort- MeRNA takes as input a file of reads (fasta or fastq format) and one or multiple rRNA database file(s), and sorts apart aligned and rejected reads into two files specified by the user. SortMeRNA works with Illumina, 454, Ion Torrent and PacBio data, and can produce SAM and BLAST-like alignments.


    Other tools? Citation of SortMeRNA?
    Kopylova et al  2012: comparison with other tools
    * SSU-ALIGN: Nawrocki et al 2009
    * Meta-RNA: Huang et al 2009
    * rRNASelector: Lee et al 2011
    * riboPicker: Schmeider et al 2012
    * BLASTN


    In SortMeRNA version 1.99 beta and up, users have the option to output sequence alignments for their matching rRNA reads in the SAM or BLAST-like formats. Depending on the desired quality of alignments, different parameters choices must be set. Table 1 presents a guide to setting parameters choices for most use cases. In all cases, output alignments are always guaranteed to reach the threshold E-value score (default E-value=1). An E-value of 1 signifies that one random alignment is expected for aligning all reads against the reference database. The E-value in SortMeRNA is computed for the entire search space, not per read.

    SortMeRNA alignment parameter guide
    * num-alignment
    > *  Very fast for 1: Output the first alignment passing E-value threshold (best choice if only filtering is needed)
    > *  Speed decrease for higher value: Higher INT signifies more alignments will be made & output
    > *  Very slow for 0: All alignments reaching the E-value threshold are reported (this option is not suggested for high similarity rRNA databases, due to many possible alignments per read causing a very large file output)
    * best
    > *  Fast for 1: Only one high-candidate reference sequence will be searched for alignments (determined heuristically using a Longest Increasing Sub- sequence of seed matches). The single best alignment of those will be reported
    > *  Speed decrease for higher values: Higher INT signifies more alignments will be made, though only the best one will be reported
    > *  Very slow for 0: All high-candidate reference sequences will be searched for alignments, though only the best one will be reported

    SortMeRNA options
    * rejected reads filepath + base file name
    * output FASTA/FASTQ file (for aligned and/or rejected reads) (off by default)
    * output SAM alignment (for aligned reads only) (off by default)
    * add SQ tags to the SAM file (off by default)
    * output alignments in various Blast-like formats: pairwise, tabular (Blast -m 8 format), tabular + column for CIGAR, tabular + columns for CIGAR and query coverage
    * output overall statistics (off by default)
    * report first INT alignments per read reaching E-value (--num_alignments 0 signifies all alignments will be output) (-1 by default)
    * report INT best alignments per read reaching E-value by searching --min_lis INT candidate alignments (--best 0 signifies all candidate alignments will be searched) (1 by default)
    * search all alignments having the first INT longest LIS. LIS stands for Longest Increasing Subsequence, it is computed using seeds' positions to expand hits into longer matches prior to Smith-Waterman alignment. (2 by default)
    * output null alignment strings for non-aligned reads off to SAM and/or BLAST tabular files (off by default)
    * both paired-end reads go in --aligned fasta/q file off (interleaved reads only, see Section 4.2.4 of User Manual) (off by default)
    * both paired-end reads go in --other fasta/q file off (interleaved reads only, see Section 4.2.4 of User Manual) (off by default)
    * SW score (positive integer) for a match (2 by default)
    * SW penalty (negative integer) for a mismatch (-3 by default)
    * SW penalty (positive integer) for introducing a gap (5 by default)
    * SW penalty (positive integer) for extending a gap (2 by default)
    * SW penalty for ambiguous letters (N's) (scored as --mismatch)
    * search only the forward strand (off, by default)
    * search only the reverse-complementary strand (off, by default)
    * number of threads to use (1, by default)
    * E-value threshold (1, by default)
    * INT Mbytes for loading the reads into memory (maximum -m INT is 4096) (1024, by default)
    * %id similarity threshold (the alignment must still pass the E-value threshold) (0.97, by default)
    * %query coverage threshold (the alignment must still pass the E-value threshold) (0.97, by default)
    * FASTA/FASTQ file for reads matching database < %id (set using --id) and < %cov (set using --coverage) (alignment must still pass the E-value threshold) (off, by default)
    * output OTU map (input to QIIME's make_otu_table.py) (off, by default)
    * three intervals at which to place the seed on the read (L is the seed length set in ./indexdb_rna) (L,L/2,3, by default)
    * number (or percent if INT followed by % sign) of nucleotides to add to each edge of the read prior to SW local alignment (4, by default)
    * number of seeds matched before searching for candidate LIS (2, by default)
    * search for all 0-error and 1-error seed matches in the index rather than stopping after finding a 0-error match (<1% gain in sensitivity with up four-fold decrease in speed) (off, by default)
    * add pid to output file names (off, by default)

    Databases
    =========

    order

    SortMeRNA? which database?
    Pb with eukaryotic databases : elimination of all eukaryotic sequences even the ones of microorganisms
    Give the choice of database 
    Limit the database to human origin sequences

    SortMeRNA comes prepackaged with 8 databases : 
    * silva-bac-16s-id90
    > * %id: 90
    > * #seq (clustered): 12798 
    > * origin: SILVA SSU Ref NR v.119
    > * #seq (original): 464618 
    * silva-arc-16s-id95
    > * %id: 95
    > * #seq (clustered): 3193
    > * origin: SILVA SSU Ref NR v.119 origin
    > * #seq (original): 18797
    * silva-euk-18s-id95
    > * %id: 95
    > * #seq (clustered): 7348
    > * origin: SILVA SSU Ref NR v.119
    > * #seq (original): 51553
    * silva-bac-23s-id98
    > * %id: 98
    > * #seq (clustered): 4488
    > * origin: SILVA LSU Ref v.119
    > * #seq (original): 43822
    * silva-arc-23s-id98
    > * %id: 98
    > * #seq (clustered): 251
    > * origin: SILVA LSU Ref v.119
    > * #seq (original): 629
    * silva-euk-28s-id98
    > * %id: 98
    > * #seq (clustered): 4935
    > * origin: SILVA LSU Ref v.119
    > * #seq (original): 13095
    * rfam-5s-id98
    > * %id: 98
    > * #seq (clustered): 59513
    > * origin: RFAM
    > * #seq (original): 116760
    * rfam-5.8s-id98
    > * %id: 98
    > * #seq (clustered): 13034
    > * origin: RFAM
    > * #seq (original): 225185

    HMMER 3.1b1 and SumaClust v1.0.00 were used to reduce the size of the original databases to the similarity listed in column 2 (%id) of the table above (see /sortmerna/rRNA databases/README.txt for a list of complete steps).
    These representative databases were specially made for fast ltering of rRNA. Approximately the same number of rRNA will be filtered using silva-bac-16s-id90 (12802 rRNA) as using Greengenes 97% (99322 rRNA), but the former will run significantly faster. id %: members of the cluster must have identity at least this % id with the representative sequence

    Before using SortMeRNA, the fasta database must be indexed using the command indexdb rna available with SortMeRNA package. The databases are stored with SortMeRNA sources. To had other database, need to add them into the same directory

    The command comes with several options

    - fast for aligning ~99% related species
    - sensitive for aligning ~75-98% related species
    - if not fast or sensitive, seed length
    - maximum number of positions to store for each unique L-mer

    Addition of other databases???

    Tests output
    ============

       