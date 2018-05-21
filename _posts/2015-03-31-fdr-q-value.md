---
layout: post
title: FDR 和 q-value
excerpt: Difference between FDR and q-value
modified: 2015-11-03
categories: articles
tags: [Bioinformatics]
comments: true
share: true
---


最近在做一个肝癌预测的项目，建模使用的数据源在[The Cancer Genome Atlas (TCGA)](https://tcga-data.nci.nih.gov/tcga/tcgaHome2.jsp)下载。

在调研文献时，看到了许多 FDR、 q-value 等指标，于是做了个小小的调研。关于假设检验的指标，脑海中第一反应便是p-value，众多科学家做统计的主要目标常常就是为了追逐一个小于 0.05 的 p 值。一般 p < 0.05 表示实验具有统计学差异，今天看到 q-value ，不太熟悉，学习并记录如下。

先简要谈谈 p-value ，用统计方法进行决策的过程中，一般会提出两个假设：

* H0: null hypothesis
* H1: alternative or research hypothesis

假设检验的目的就是利用统计的方式，推测 H0 是否成立。那好，先假设 H0 事实上成立，如果统计检验的结果不支持，造成「Type I error」，如果假设 H0 事实上不成立，但统计检验的结果支持，造成「Type II error」。**p-value** 指的是犯「Type I error」的概率，本质上是控制 FPR (False Positive Rate)。

关于两类错误，打个简单的比方，用验孕棒检测一位女士是否怀孕。

* H0: 已怀孕
* H1: 未怀孕

先假设孕妇事实怀孕，检测后发现没有怀孕，此乃「Type I error」（我一般理解为误诊率），再假设孕妇并未怀孕，检测后发现怀孕，此乃「Type II errror」。如果我们的 p-value < 0.01「真的是相当严格的标准了」，就表示用此种验孕棒检测时，检测100次测错次数小于1次，这是个小概率事件，表示验孕棒还是相当可靠的。

但是，一旦涉及到多重比较，这种准确性便远远不够了。小小开个脑洞，我们拿1万个验孕棒做成100*100的array，现在我们一次性可以帮一万名女士检测是否怀孕。那么对于这一万名女性，其中「10000X0.01=100」人便会得到错误的结果，可能就因为这里的错误，导致这些女性改变人生轨迹，这是不可饶恕的。所以，对于多重检验，如果不进行任何控制，犯「Type I error」的概率便会随着假设检验的个数迅速增加。为了合理控制，有必要引入一个更加严格的指标，也就是 **q-value**。

在多重假设检验中，有许多方法来克服这个问题。比如对每个测试用例赋校正后的 p-value，或者将 p-value 的阈值从 5% 下降到一个更为合理的阈值。许多传统的技术例如 [Bonferroni correction](https://en.wikipedia.org/wiki/Bonferroni_correction) 从某种意义上来说显得较为保守，他们主要是依靠减少假阳性的个数，同时也会减少 TDR (True Discovery Rate)。FDR（False Discovery Rate）方法则是一种更加新颖靠谱的方法。这个方法同样会对每个测试用例赋校正后的 p-value，但是，它还控制了错误发现的个数。在实际研究中，我们能够容忍出现少量误诊，但需要在误诊的人数和出现误诊概率两个参数间找到一个平衡。这里需要提到一个概念: FWER (familty-wise error rate)，即至少出现一次「Type I error」的概率。

>  In statistics, family-wise error rate (FWER) is the probability of making one or more false discoveries, or type I errors, among all the hypotheses when performing multiple hypothesis tests. 			---[Wiki](https://en.wikipedia.org/wiki/Familywise_error_rate)

FDR 可以在「Type I error」~ FWER 寻找平衡。换句话说，FDR 方法在多重检验中依靠牺牲 p 值 (增长「Type I error」）来提高整体的统计效能。q-value 指的是用 FDR 方法校正后的 p 值，计算方法如下：

{% highlight R %}
P.Values ​​<- runif ( 100 )
Q.Values <- p.adjust (P.Values, method = "fdr")
{% endhighlight %}

## References
1. [Adjust P-values for Multiple Comparisons](https://stat.ethz.ch/R-manual/R-devel/library/stats/html/p.adjust.html)
2. [False discovery rate](https://en.wikipedia.org/wiki/False_discovery_rate)
3. [Family-wise error rate](https://en.wikipedia.org/wiki/Familywise_error_rate)
4. [How does multiple testing correction work?](http://www.nature.com/nbt/journal/v27/n12/full/nbt1209-1135.html)

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
