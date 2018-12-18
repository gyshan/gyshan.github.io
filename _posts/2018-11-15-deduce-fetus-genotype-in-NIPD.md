---
title: "Deduce fetus genotype in NIPD"
excerpt: "Explore cffDNA in maternal blood"
categories:
  - articles
tags:
  - Bioinformatics
---

Non-invasive prenatal diagnosis (NIPD) based on the analysis of cell-free fetal DNA (cffDNA) in maternal plasma is now available in clinical practice for a small number of single gene disorders. A key challenge for the development of NIPD is the low level of cffDNA present alongside the high background of maternal cfDNA in maternal plasma. Determine fetus genotype accurately from cffDNA is of great importance for the family's choice.

Imagine we have determined the target variant (**aa**) from a proband patient with autosomal recessive conditions and his/her mother decide to have a second pregnancy. How can we deduce fetus genotype of this target variant from a maternal peripheral blood diagnosis? Here is the thing:
1. Draw maternal peripheral blood from pregnant mom
2. Isolate white blood cell (WBC) and plasma from maternal blood
3. Analysis two types of samples by NGS methods
4. Achieve target attributes: frequency in WBC, frequency in plasma and the concentration of cffDNA

Now, start fetus genotype deducing. The reason behind our deducing method is to compare different plasma theoretical frequencies of three genotypes (AA, A**a**, **aa**) to the actual frequency and find the best match. Let’s do this:

Theoretical scheme:

| Maternal genotype | Fetus genotype | plasma frequency (fetus_conc: c) | plasma frequency (fetus_conc: 5%) |
|-------|--------|---------|---------|
| AA | AA | 0 | 0 |
| AA | Aa | c/2 | 2.5% ||
| Aa | AA | (1-c)/2 | 47.5% |
| Aa | Aa | 50% | 50% |
| Aa | aa | (1+c)/2 | 52.5% |
| aa | Aa | 1-c/2 | 97.5% |
| aa | aa | 1 | 1 |


Assuming parameters:

1. Frequency in WBC: 47% (A**a**)
2. Concentration of cffDNA: 10%
3. Frequency in plasma: 41% (A**a**)


Deducing:

{% highlight text %}
WBC: a = 47 units, A = 53 units
Plasma: 
1. Maternal: a = 47 units, WBC-frq = 47/100 = 47%
2. plasma-a = actual-a-alleles-in-maternal + theoretical-a-alleles-in-fetus
3. If fetus-AA: plasma-a = 47*0.9+0*0.1, plasma-frq = 42.3/100 = 42.3%
4. If fetus-Aa: plasma-a = 47*0.9+50*0.1, plasma-frq = 47.3/100 = 47.3%
5. If fetus-aa: plasma-a = 47*0.9+100*0.1, plasma-frq = 52.3/100 = 52.3%
{% endhighlight %}

Conclusion:

Congratulations! The genotype of the fetus is AA, and the mother will yield a healthy baby.

At the end of this small article, I would like to say that the accuracy of `fetal concentration` and `plasma frequency` is crucial for fetal genotype inference. Therefore, it can not be too hard to improve those two metrics.


**a**: disease-causing allele
{: .notice}