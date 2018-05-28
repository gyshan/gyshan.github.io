---
title: "Download TCGA data from ftp"
excerpt: "Agile trick for downloading cancer omics data from TCGA"
categories:
  - articles
tags:
  - Bioinformatics
---

[TCGA(The Cancer Genome Atlas)](https://tcga-data.nci.nih.gov/tcga/) is a widely used website for cancer genomics download. <strike>The traditional pathway is loading to website -> select matrix -> submit your Email and wait for a .tgz file link returns.</strike> The time you received link is depends on how many tasks ahead of you. It will often take you several hours to download only one cancer omics data.

Here, there remains an alternative choice to download TCGA data. You can click to call on a [ftp website](https://tcga-data.nci.nih.gov/tcgafiles/ftp_auth/distro_ftpusers/anonymous/tumor/) to check the data structure. And then direct to the destination link you want to download and use `mirror` in ftp or `wget` directly to retrieve folders/files. This small trick can reduce your waiting time. Even though it will be very hard to download large folders smoothly, but it will be extremely useful when downloading relatively small folders.

