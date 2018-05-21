---
layout: post
title: A genius CNV calling strategy
excerpt: Genius strategy, genius guy
modified:
categories: articles
tags: [Bioinformatics]
comments: true
share: true
---

Several days ago, we found that one specific gene of Copy Number Variation(CNV) in Life sequencing platform is not so accurate as we expect.

We are used to construct a baseline from several negative samples (CN=2; N>10), which is employed to call CNV of every new samples in a long time. But the problem is that the CNVs of new samples become increasingly biased from FISH result (a gold-standard of CNV) along with the time going. We think that the problem is everything is changing except for this baseline, especially baseline is extremely biologically sensitive to experimental condition, pipeline and enzyme.

One of my genius colleagues has reached out an idea, why not convert **static baseline** to **dynamical baseline**. So when we want to call a CNV of certain sample, an automatic baseline is yielded from the same batch of this sample(ignoring positive or negative). After first calling, remove the samples which possess the highest and lowest CN value and reconstruct the baseline. At last, utilize the latest baseline to call CNV of the sample.

I am pleased to be able to work with this guy. Now he is decided to leave and I believe he has his own choice and plan. Wish him a good future.

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
