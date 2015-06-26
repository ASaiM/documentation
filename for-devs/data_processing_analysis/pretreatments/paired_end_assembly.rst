.. _for-devs-pretreatments-paired-end-assembly:

Pretreatments of high throughput sequencing data
################################################

Assembly of paired-end

FastQJoin
=========

This is the default method to join paired-end Illumina data:

Similar to audy's stitch program, but in C, more efficient and supports some automatic benchmarking and tuning. It uses the same "squared distance for anchored alignment" as other tools.

fastq-join produces a "report". This is just a list of lengths of joined reads. Also it chooses the "better quality base" when overlapping. Very stable code at this point.

Etc
This uses our sqr(distance)/len for anchored alignment quality algorithm. It's a good measure of anchored alignment quality, akin (in my mind) to squared-deviation for means.

Overlapping Bases
When the bases match : The higher quality base is used, and it is increased by up to 3

When the bases don't match : If one quality is greater than "3" (50%), then the the resulting quality is the difference between the two qualities (reduced quality due to mismatch), or "3" )(50%), whichever is greater.

Examples:
40 vs 3 = 37 : second base has low quality... doesn't change top by much
40 vs 40 = 3 : two equal quality bases that don't match = qual of 3
2 vs 2 = 2 : neither base has a high quality

Some caveats: Illumina's quality scores are not accurate and estimates vary by chemistry and sequencer. I would recommend using a profiling tool, on PhiX, and adjusting your qualities using the results of the tool. For example the quality score "2" has a true quality, typically of "11" ... this is Illumina's code for "quality estimation failure". The quality scores at the high end ("34-40") are often overestimates.

-j, --min_overlap
Applies to both fastq-join and SeqPrep methods. Minimum allowed overlap in base-pairs required to join pairs. If not set, progam defaults will be used. Must be an integer. [default: None]
-p, --perc_max_diff
Only applies to fastq-join method, otherwise ignored. Maximum allowed % differences within region of overlap. If not set, progam defaults will be used. Must be an integer between 1-100 [default: None]

Citations of FastQJoin?

SeqPrep
=======

Other tools
===========

   