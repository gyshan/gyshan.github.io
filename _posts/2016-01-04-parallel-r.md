---
title: "Running R with parallel under linux"
excerpt: "Example code"
categories:
  - articles
tags:
  - R
---

R is a free, powerful programming language and software environment for statistical computing and graphics supported by the R Foundation.

Recently, I've been dealing with parallel processing in R and have found the [foreach](https://cran.r-project.org/web/packages/foreach/foreach.pdf) and [doMC](https://cran.r-project.org/web/packages/doMC/doMC.pdf) packages to be useful approaches in increasing efficiency of loops. 

The doMC package is a "parallel backend" for the foreach package. It provides a mechanism needed to execute foreach loops in parallel. Usually, we'd better check the maximum number of threads(It's 96 for me) first by using `detectCores`.

{% highlight R %}
library(parallel)
detectCores()
{% endhighlight %}

Then configure a smaller number for subsequent parallel processing (I set 20, which means 20 threads will be reserved for my task). 


**In this task, I select and record good models that satisfying certain conditions (Sp > 0.88, Se > 0.7).**


### Without parallel
{% highlight R %}
optSeeds <- function(input.train){
  seed_lst <- list()
  i <- 0
  for (seed in 1:1000){
    result <- modelSelect(input.train, seed)
    Sens <- result$byClass['Sensitivity']
    Spec <- result$byClass['Specificity']
    Acc <- result$byClass['Balanced Accuracy']
    output <- c(seed, Spec, Sens, Acc)
    if (Spec > 0.88 & Sens > 0.7){
    	i += 1
    	seed_lst[i] <- seed
    }
  }
}

seedLst <- optSeeds(input.train)
{% endhighlight %}

### With parallel
{% highlight R %}
library(foreach)
library(doMC)
registerDoMC(20)

optSeeds <- function(input.train){
  foreach (seed = 1:1000) %dopar% {
    result <- modelSelect(input.train, seed)
    Sens <- result$byClass['Sensitivity']
    Spec <- result$byClass['Specificity']
    Acc <- result$byClass['Balanced Accuracy']
    output <- c(seed, Spec, Sens, Acc)
    if (Spec > 0.88 & Sens > 0.7){
	seed
    }
  }
}

seedLst <- optSeeds(input.train)
{% endhighlight %}


This small change shrunk my time from several hours to less than five minutes, what a lovely change.  

