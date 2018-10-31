---
title: "Customized color key for pheatmap"
excerpt: "R snippets"
categories:
  - articles
tags:
  - Bioinformatics
  - R
---

[Pheatmap](https://cran.r-project.org/web/packages/pheatmap/pheatmap.pdf) is an R package, which is famous for its heatmap annotation function. Standard color key profile is well-proportioned based on the value of related data frame. If we want to set different split point or uneven color range, what should we do? Here is the code:


{% highlight R %}
library(pheatmap)
set.seed(9527)
dat <- cbind(matrix(rnorm(120), 30, 40), matrix(sample(15, 120, T), 30))
my.breaks <- c(seq(-3, 0, by=0.1), seq(0.1, 20, by=5))
my.color <- c(colorRampPalette(colors = c("blue", "white"))(length(my.breaks)/2), colorRampPalette(colors = c("white", "red"))(length(my.breaks)/2))
pheatmap(dat, 
         color = my.color,
         breaks = my.breaks
)
{% endhighlight %}

Plus, it should be noticed that we should avoid red-green schema when it is supposed to be shown to someone else. About 8.73% of males and 1.69% of females were found to be color blind[^1] and will have trouble reading red-green heatmap.

[^1]: Ahsana S, Hussain R, Fareed M, et al. Prevalence of red-green color vision defects among Muslim males and females of Manipur, India[J]. Iranian journal of public health, 2013, 42(1): 16.
