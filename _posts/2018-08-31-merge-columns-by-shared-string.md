---
title: "Merge columns by shared string"
excerpt: "Split and merge"
categories:
  - articles
tags:
  - Bioinformatics
  - R
---

Imagine there is a data frame demo looked like this and we need to combine columns which hold the same tag. What should we do?

{% highlight text %}
### binary_var_dat
          EGFR_T790M KRAS_K201S BRAF_K220Q NOTCH_N22K EGFR_V600E EGFR_Q333S EGFR_F222Q KRAS_F22X
S1                 0          0          1          0          1          0          0         1
S1_xxxxxx          0          0          0          0          1          0          1         1
S2                 0          0          1          0          0          0          0         0
S2_xxxxxx          1          0          1          0          1          0          1         0
S3                 0          1          1          0          0          0          0         1
S3_xxxxxx          0          0          1          0          1          0          1         0
S4                 0          0          0          1          1          0          0         1
S4_xxxxxx          0          1          1          0          0          0          1         1
S5                 0          0          1          0          1          0          0         0
S5_xxxxxx          1          0          0          0          1          1          1         1
S6                 0          0          1          0          0          0          0         1
S6_xxxxxx          0          0          1          0          1          0          1         1
{% endhighlight %}

{% highlight text %}
### gene_mat
          EGFR KRAS BRAF NOTCH
S1           1    1    1     0
S1_xxxxxx    2    1    0     0
S2           0    0    1     0
S2_xxxxxx    3    0    1     0
S3           0    2    1     0
S3_xxxxxx    2    0    1     0
S4           1    1    0     1
S4_xxxxxx    1    2    1     0
S5           1    0    1     0
S5_xxxxxx    4    1    0     0
S6           0    1    1     0
S6_xxxxxx    2    1    1     0
{% endhighlight %}


More specifically, if we want to convert `binary_var_dat` to `gene_mat`, what procedures can we take?
Here is my solution:
1. Split each column names by its delimiter;
2. Replace column names by its splited string;
3. Merge columns with the same column name.


{% highlight R %}
pre_gene_mat <- binary_var_dat
colnames(pre_gene_mat) <- sapply(strsplit(colnames(pre_gene_mat), split = "_"), '[', 1)
pre_gene_mat <- as.matrix(pre_gene_mat)
coln <- colnames(pre_gene_mat)
gene_mat <- pre_gene_mat %*% sapply(unique(coln),"==", coln)

{% endhighlight %}

To be honest, I spend almost half an hour effort on this problem. The reason I took so much time is that I have been suspected that `data frame` in R should only possess unique row names and column names. Surpringly, it is very flexible --- unique row names and flexible column names. 

In specific circumstances, if you want duplicated row names, just transpose the data frame and do whatever you want. I like this design philosophy.

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
