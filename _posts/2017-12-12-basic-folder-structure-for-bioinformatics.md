---
title: "Basic folder structure for bioinformatics"
excerpt: "Organize project folder is important"
categories:
  - articles
tags:
  - Bioinformatics
---

Yesterday, a friend of mine asked me if there was an excellent way to organize folders for a bioinformatics project. That is also an excellent question to me. As for me, when dealing with a relatively light-weight project such as testing a script for GC content counting or performing pure BLAST, I would prefer to use a flat folder. 

However, when developing a relatively heavy-weight product such as an algorithm, like microsatellite instability determination or an auto-interpretation algorithm for NGS variants under ACMG guidelines, a flat folder structure is not well enough to support a project like this. 

Therefore, it is necessary to organize the project folder seriously. The basic idea for organizing the folder is to guarantee the traceability and clarity. So, I strongly recommend the structure below:

{% highlight text %}
.
├── 00.raw
│   └── raw_fasta.fa
├── 01.bin
│   └── process.py
├── 02.ref
│   ├── 20160211_report.pptx
│   └── material.pdf
├── 03.rst
│   ├── publication.png
│   └── svm.xlsx
├── Misc
│   └── MWE
│       ├── demo_input
│       └── work.sh
└── ReadMe
{% endhighlight %}

The project folder includes five subfolders, which are `raw`, `bin`, `ref`, `rst` and `Misc`. Besides, the `ReadMe` file should contain in the project folder. `ReadMe` file is a form of documentation that contains information about other files in this directory. Each subfolder has its function in this project.

* `raw`: Save raw files, often come from Illumina machine or website
* `bin`: Save developed scripts
* `ref`: Save reference materials
* `rst`: Save important results
* `Misc`: Save Miscellaneous files. The most critical subfolder in it is a minimal working example (MWE), which is a collection of source code and other essential data files, allowing a bug or problem to be demonstrated and reproduced.

In a word, a well-organized folder can facilitate human readability and therefore be good for the project. The code is more for computers, and a well-organized folder structure is for humans. It is often more challenging to deal with humans than machines.