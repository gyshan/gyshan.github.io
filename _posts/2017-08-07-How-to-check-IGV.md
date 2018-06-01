---
title: "How to check IGV"
excerpt: "Memo of NGS variant checking by IGV"
categories:
  - articles
tags:
  - Bioinformatics
---

Integrative Genomics Viewer ([IGV](http://software.broadinstitute.org/software/igv/)) is a high-performance visualization tool for interactive exploration of large, integrated genomics datasets.

> When I check my bam file by IGV tool, what should I focus on?

Mostly, when I found that a variant is quite uncertain, there are three important steps that I need to finish:

1. Check sequencing quality control indicators such as average_depth_on_target, capture_ratio and so on;
2. If all QC indicators are qualified, check bam file by IGV tool;
3. If QC and IGV are both OK, check variant calling pipeline and parameters.

IGV checking is at the heart of the troubleshooting process, when I look at the whole reads profile by IGV, here is what I will do:

1. Jump to questioned position;
2. Check depth profile of the region;
3. Sort alignments by base [^1];
4. Check depth and mapQ score of each read [^2];
5. Check if variant is at the edge of Amplicon/Target;
6. Check if variant is in the region which has extremely high GC content.

In short, most of our problems can be clarified by the IGV. If a problem can not be solved by IGV, recheck mapping procedure.


[^1]: Make sure it is easy to view the reads that with the same property. (SNV, Softclip, ...)
[^2]: If there are multiple SNVs in a relatively short region (<100bp) which supported by low mapQ reads, it is necessary to blast if the sequence of target gene is similar to other genes in reference. The similarity of the target gene with another will significantly lower the mapQ of the reads in the target region. (eg. PRSS1 and PRSS2).




