---
title: "Install Blat on mac with one-line command"
excerpt: "Quick answer"
categories:
  - articles
tags:
  - Bioinformatics
---

Blat is a bioinformatics software tool for sequence alignment. When I googled `install blat on mac`, what came to my screen are numerous trouble shooting posts. Here, I want to present a one-line command solution:

{% highlight bash %}
conda install -c bioconda blat  # Imagine you already have conda installed
{% endhighlight %}

If do not have conda installed on your Mac, install it with following commands:
{% highlight bash %}
wget https://repo.continuum.io/miniconda/Miniconda2-latest-MacOSX-x86_64.sh
sh Miniconda2-latest-MacOSX-x86_64.sh
{% endhighlight %}


