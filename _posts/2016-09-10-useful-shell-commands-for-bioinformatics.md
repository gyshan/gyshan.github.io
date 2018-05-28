---
title: "Useful shell commands for bioinformatics"
excerpt: "Common shell commands"
categories:
  - articles
tags:
  - Bioinformatics
---

A large portion of biological data are raw files, such as fasta、fastq、bam（binary)、sam、vcf and so on.
Mostly, trying to deal with those files with shell commands towards small tasks are way much better than using stardard programming language(python and perl).
Here, I want to record some of those tricks.

# samtools
{% highlight bash %}
##1. Pre-process bam for certain software
# cut bam to target region, bear in mind that chr1 is in [in.bam] 
samtools view -b [in.bam] [chr1:XXXXXXX-YYYYYYY] > [out.bam]
# sort bam
samtools sort [out.bam] [out.sorted.bam]
# index bam
samtools index [out.sorted.bam]
##2. Extract certain region from ref.fasta
samtools faidx [ref.fasta] chr1:XXXXXXX-YYYYYYY
##3. mpileup
samtools mpileup -d 1000000 -q 30 -Q 30 -A -B -l [in.bed] -f [ref.fasta] [in.bam] > [out.mpileup]
{% endhighlight %}

# shell
{% highlight bash %}
#1. Sort file according to column three.
sort -n -k3 [in.file]
#2. Remove empty line from file
sed -i '/^$/d' [in.file] > [out.file]
#3. Extract row that have str 'S' in  column six.
awk '$6 ~ /S/ {print}' [in.sam]
#4. Search bam file from certain directory
find . -name "\*.bam"
#5. Sum the fourth column from mpileup file.
awk '{ sum += $4 }; END { print sum }' [mpileup] > [out.file]
#6. Sum the coverage of bed file
awk -F'\t' 'BEGIN{SUM=0}{ SUM+=$3-$2 }END{print SUM}'
#7. Remove chr fro bed file
sed 's/^chr//'
#8. Replace \s to \t in file
awk -v OFS="\t" '$1=$1'
#9. Get lines from file
sed -n 2,4p somefile.txt
sed '2,4!d' somefile.txt
{% endhighlight %}

