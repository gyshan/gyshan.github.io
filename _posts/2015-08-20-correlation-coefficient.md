---
title: "Pearson相关系数和Spearman相关系数"
excerpt: "Concepts for two kinds of relevance coefficients."
categories:
  - articles
tags:
  - Bioinformatics
---

{% include toc %}

## 1. 什么是相关性

相关性系数是用来反映变量间相关关系密切程度的统计指标。它描述了相关性的大小以及方向（正相关or负相关）。说到相关性，有两个评价指标是不得不提的：

#### Pearson product-moment correlation
Pearson相关主要用来评价两组连续变量的线性关系。一个变量变化，另一个变量也成比例变化。



#### Spearman rank-order correlation
Spearman相关主要用来评价两组连续或有序变量的单调关系。一个变量变化，另一个变量也变化，但不一定以固定比例变化。


 
## 2. Pearson and Spearman 相关系数的比较

* Pearson 和 Spearman相关系数的范围均为 [-1,1]；
	
	* 0.8-1.0	极强相关
	* 0.6-0.8	强相关
	* 0.4-0.6	中等强度相关
	* 0.2-0.4	弱相关
	* 0.0-0.2	极弱相关或无相关

* Pearson相关系数只可用于评价线性关系；
* Spearman相关系数只可用于评价单调关系。

<figure >
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/spearman.png" alt="image">
</figure>
[Fig source](https://epilab.ich.ucl.ac.uk/coursematerial/statistics/non_parametric/spearman.html)

## 3. 总结

在生物信息学领域，由于Spearman对数据点无分布要求，适用范围较广，通常作为主要评价指标。
不过，对于非线性关系，是不可用以上两者评价的。倘若错用，即便有时相关系数为0，两组变量间也有可能存在有意义的联系。
<figure >
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/nonlinear.png" alt="image">
</figure>
[Fig source](http://www.ablongman.com/graziano6e/text_site/MATERIAL/statconcepts/relationship.htm)


