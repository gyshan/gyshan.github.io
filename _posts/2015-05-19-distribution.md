---
layout: post
title: 正态分布与幂律分布
excerpt: Normal distribution and power-law distribution

modified: 
categories: articles
tags: [Bioinformatics]
comments: true
share: true
---

在我们的日常生活中，总是会被各式各样的现象所包围，小到人们的身高分布，大到国家的财富分布。久而久之，人们抽象出了两个通用的模型来解释这些现象，一个叫做[正态分布](http://zh.wikipedia.org/wiki/%E6%AD%A3%E6%80%81%E5%88%86%E5%B8%83)，另一个叫做[幂律分布](http://baike.baidu.com/view/1730411.htm)。

#正态分布
<figure >
<img src="https://dn-shanguangyu.qbox.me/normal_distribution.png" alt="image">
</figure>
正态分布 (normal distribution) 又叫高斯分布 (Gaussian distribution)，是重要的概率分布之一，其概率密度函数为

$$\varphi_{\mu,\sigma}(x)=\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{(x-\mu)^2}{2\sigma ^2}}$$

由于形似钟形，又经常称之为钟形曲线。在生产与科学实验中，很多随机变量的概率分布都可以近似用正态分布描述。例如生物体的身长、体重，地区降水量等等。除此之外，还有一些常见的概率分布是由它直接导出的，例如对数正态分布、t分布、F分布等等，导致经常遇到这种情况：

>要使用xx检验，必须满足正态分布。

有人说过：直线属于人类，曲线属于上帝。每个人追求的曲线也许不同，男人追求不断向上的曲线，女人追求玲珑浮凸的曲线，而真正的上帝曲线应该是这个形似钟形的神秘曲线，无影无形，却又无处不在。

#幂律分布
<figure >
<img src="https://dn-shanguangyu.qbox.me/pareto.gif" alt="image">
</figure>
很早就知道二八法则的概念，最早是说社会上 20% 的人占有 80% 的社会财富，强调世界充满了重要的少数与琐碎的多数，这个法则在管理学、社会学等很多方面都有体现，再往上走一步，这种概率分布可以用一种更加科学的名词来表征，叫做幂律分布。

幂律分布 (power law distribution) 是一种常见的统计现象，简单地说就是两个变量为幂函数的关系，而这种简单的关系却能够与很多领域的实际情况相吻合，尤其是生物学、生态学这类典型的无标度网络。与随机网络不同，这种无标度网络的度常常是集散分布，大部分节点只有较少的连接，而少数节点有大量的连接。这类无标度网络的特性是：当节点意外失效或改变时，对网络的影响一般很小，只有 hub 节点受到改变，才会让网络产生剧烈的震荡。对于目前的中国，Mr. Xi 就是一个典型的 hub 节点。


---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
