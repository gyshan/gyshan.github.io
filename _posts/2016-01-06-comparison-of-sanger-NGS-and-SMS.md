---
title: "Comparison of sanger, NGS and SMS"
excerpt: "An article to summarize three methods in sequencing"
categories:
  - articles
tags:
  - Bioinformatics
---



It's a big era for sequencing. About forty years ago, [Frederick Sanger](https://en.wikipedia.org/wiki/Frederick_Sanger) and colleagues brought Sanger sequencing technique to the world. During the past four decades, tremendous progress has been made in terms of speed, read length and throughput, along with a sharp reduction of per-base cost. Many sequencing techniques appeared in this megatrend as well as multiple outstanding companies. No matter what exciting techniques have been developed, these three main generations will not be ignored in this revolution: Sanger, NGS and SMS. Here I will present some knowledge about the difference between them.

### Sanger Sequencing
Sanger sequencing, which is used by the Human Genome Project (HGP), has finished its sequencing phase in 2003 from 1984. This project took hundreds of labs working together, and cost of around $100 million.

pros

* High precision 「error rate: 0.001% - 1%」
* Long read
 
cons

* Low throughput
* High cost


### Next-Generation Sequencing (NGS)
With its unprecedented throughput, scalability, and speed, next-generation sequencing enables researchers to study biological systems at a level never been possible. Illumina NGS utilizes a fundamentally different approach from the classic Sanger chain-termination method. It leverages sequencing by synthesis (SBS) technology - tracking the addition of labeled nucleotides as the DNA chain is copied - in a massively parallel fashion. In addition, the cost of sequencing a single human genome is under $1000, which means detecting SNPs and structural variants or construct big databases will not only just a dream any more.

pros

* Low cost
* High throughput
* Decent Precision「error rate: 0.46% - 2.4%」

cons

* Short read (which will lead to a low precision when perform sequence assembly)

### Single Molecule Sequencing (SMS)

This DNA sequencing technology is done on a chip that contains many ZMWs (zero-mode waveguide), a structure that creates an illuminated observation volume that is small enough to observe only a single nucleotide of DNA being incorporated by DNA polymerase. Inside each ZMW, a single molecule of single stranded DNA template is immobilized to the bottom through which light can penetrate and create a visualization chamber that allows monitoring of the activity of the DNA polymerase at a single molecule level. The signal from a phospho-linked nucleotide incorporated by the DNA polymerase is detected as the DNA synthesis proceeds which result in the DNA sequencing in real time. Plus, it cost under $100 for genome sequencing.

pros

* Long read
* High throughput

cons

* Indel (insert & delete)
* Low precision 「error rate: 11% - 14%」


### Discussion

When it mentions to sequencing, the ultimate goal is to get a human genome directly. If there is a machine able to sequence human genome directly, the following discussion will make no sense.

But it is not. We still need sequence multiple reads and assemble them. Theoretically, small reads (30-40bp) can assemble a genome very well if there has a circumstance without **repeats** or **heterozygous**. Back to reality, we need to confront the fact that the problems are still here that wait to be settled. Lots of assembly algorithms are dealing with these two tricky problems: de Brujin graph, Newbler, AMOS and CAP3, etc.

**NGS is a big trend, sanger is "Gold standard", while SMS is the future.** Even though the SMS has an extremely high error rate right now, but it will definitely come into a blossom era when genius scientists just keep moving on. There are two major classes of assembly algorithms: **overlap-layout-consensus (OLC)** and **de-brujin-graph (DBG)**. Considering the computational consumption of time and memory, the OLC algorithm is more suitable for the low-coverage long reads, whereas the DBG algorithm is more suitable for high-coverage short reads and especially for large genome assembly. In the next decades, it may be a glorious era for OLC.

>Entering the second decade of 21st century, high-quality genome sequences for many species are still in great demand by the genomics field. Besides the second-generation sequencing technologies, there are many other new technologies helpful for de novo sequencing, including the single molecular sequencing PacBio (www.pacificbiosciences.com) and the Optical Mapping physical technology OpGen (www.opgen.com), which has recently entered the market. PacBio produces extreme long reads (1–10 kb) but with a high error rate (15–20%), whereas OpGen can generate 100 kb–1 Mb length physically linked markers, which facilitates the physical map construction. Driven by the development of these technologies, we see a bright future for de novo assembly of large genomes, with the standard likely to be raised from draft sequence to chromosome level sequence and from haploid sequence to diploid sequence. The development of assembly algorithms is tied closely to the development of sequencing technologies. The history has turned from OLC for Sanger sequencing, to DBG for second-generation sequencing, and the future will likely lead back to OLC for long reads sequencing. In the next few years, short reads assembly and long reads assembly may co-exist and both the OLC and DBG algorithms will be improved continuously. Small simple genomes can be assembled well with pure short reads, middle difficulty genomes can use the hybrid assembly method using both long and short reads, whereas large complex genomes will rely more on long reads assembly. As outlined here, it is clear that sequencing technologies and assembly algorithms will change rapidly over the next few years, and assembly will get easier and better as technologies continue improve.


<figure>
<img src="/download/Nmircro.jpg" alt="image">
</figure>

### References
1. [NGS](http://www.illumina.com/technology/next-generation-sequencing.html)
2. [SMS_Wiki](https://en.wikipedia.org/wiki/Single_molecule_real_time_sequencing)
3. [Ten years of NGS technology](http://www.sciencedirect.com/science/article/pii/S0168952514001127)
4. [The properties and applications of single-molecule DNA sequencing](http://www.genomebiology.com/2011/12/2/217)
5. [Comparison of the two major classes of assembly algorithms: overlap–layout–consensus and de-bruijn-graph_2011](http://bfg.oxfordjournals.org/content/early/2011/12/18/bfgp.elr035)

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
