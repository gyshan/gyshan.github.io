---
title: "InDel left-alignment"
excerpt: "InDel left-alignment is recommended"
categories:
  - articles
tags:
  - Bioinformatics
---

[InDel](https://en.wikipedia.org/wiki/Indel) is a common concept in molecular biology, while the representation for InDels are non-unique. There are at least two representations: left-alignment and right-alignment. Actually it does not really matter, but it good to have a convention. I would like to suggest using left-alignment with these reasons:

{% highlight text %}
ref            : CGTATGATCTA [GCGCGC] TAGCTAGCTAGC
left-alignment : CGTATGATCTA [--GCGC] TAGCTAGCTAGC
right-alignment: CGTATGATCTA [GCGC--] TAGCTAGCTAGC
{% endhighlight %}


1. Standard
Statistical genetics center of university of michigan denote that [left-alignment](https://genome.sph.umich.edu/wiki/Variant_Normalization#Left_alignment) is necessary.


2. Community
Most famous tools are stick to left-alignment, such as [GATK](https://software.broadinstitute.org/gatk/documentation/tooldocs/3.8-0/org_broadinstitute_gatk_tools_walkers_indels_LeftAlignIndels.php), [ANNOVAR](http://annovar.openbioinformatics.org/en/latest/articles/VCF/) and related databases:

* avsnp138
* avsnp142
* clinvar_20150330
* 1000g2014oct
* exac03
* esp6500siv2

> The standard convention is to place an indel at the left-most position possible.   ---GATK

> Since left-normalization is gaining more and more popularity, my suggestion is to just use left-normalization, and that database curators as well as users both use this practice, so that we can compare apples to apples.   ---ANNOVAR


In the end, I would prefer to stick to the convention --- **left-alignment**.



