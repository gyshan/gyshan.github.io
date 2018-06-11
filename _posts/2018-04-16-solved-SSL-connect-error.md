---
title: "Solved-SSL connect error"
excerpt: "R package installation"
categories:
  - articles
tags:
  - Bioinformatics
---

Today, I tried to install an R package: [facets](https://github.com/mskcc/facets). During installation, I got stuck by SSL connect error and the error code is as follows. So I tried to install this package locally and got it done.

{% highlight bash %}
# Error code
> library(devtools)
> devtools::install_github("mskcc/facets", build_vignettes = TRUE)
Downloading GitHub repo mskcc/facets@master
from URL https://api.github.com/repos/mskcc/facets/zipball/master
Installation failed: SSL connect error

> devtools::install_github("mskcc/pctGCdata", build_vignettes = TRUE)
Downloading GitHub repo mskcc/pctGCdata@master
from URL https://api.github.com/repos/mskcc/pctGCdata/zipball/master
Installation failed: SSL connect error
{% endhighlight %}

To address this issue, I turned to download the zipball from GitHub, unzip the zipball and install the package locally. Soon after this move, everything goes well.

{% highlight bash %}
>library(devtools)
>devtools::install_local("../../pctGCdata")
>devtools::install_local("../../facets")
{% endhighlight %}

