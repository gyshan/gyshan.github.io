---
layout: post
title: Basic folder structure for bioinformatics
excerpt: Organize project folder is important
modified:
categories: articles
tags: [Bioinformatics]
comments: true
share: true
---

Yesterday, a friend of mine asked me if there was a good way to organize folders for a bioinformatics project. That is also a good question to me. As for me, when dealing with a relatively light-weight project such as testing a script for GC content counting or performing simple BLAST, I would prefer to use flat folder. 

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

The project folder includes five subfolders, which are `raw`, `bin`, `ref`, `rst` and `Misc`. In addition, the `ReadMe` file should be contained in the project folder. `ReadMe` file is a form of documentation that contains information about other files in this directory. Each subfolder has its own function in this project.

* `raw`: Save raw files, often come from Illumina machine or website
* `bin`: Save developed scripts
* `ref`: Save reference materials
* `rst`: Save important results
* `Misc`: Save Miscellaneous files. The most important subfolder in it is minimal working example (MWE), which is a collection of source code and other essential data files, allowing a bug or problem to be demonstrated and reproduced.

In a word, a well-organized folder can facilitate human readability and therefore be good for the project. Code is more for computers, and well-organized folder structure is for humans. It is actually often more difficult to deal with humans than computers.


---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
