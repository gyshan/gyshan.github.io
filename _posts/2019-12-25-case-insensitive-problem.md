---
title: "Case insensitive problem"
excerpt: "Be careful when transfer files between Win and Linux platform"
categories:
  - articles
tags:
  - Bioinformatics
  - Linux
---

Recently, we start to transfer a project (comprised code files in multiple folders) from Linux to Windows platform. After compressed the project at the Windows platform, then pull back this project to the Linux platform again.

The mysterious thing happens - the project goes well on Linux, but after compression on Windows and decompression on Linux, the project is down. 

At first, we attribute the problem to the compression software and dig it in multiple aspects. After quite a long time debugging, we realized that we are in the wrong way. After that, we change the target and finally locate the problem: case-insensitive problem.

There are two folders in our project: `pod` and `Pod`. When transferring the project from Linux to Win, all files from `pod` and `Pod` folders were dumped into the `pod` folder. After pulling back to the Linux platform, the necessary `Pod` folder is missing, and the error occurs. After dealing with the naming problem, the project goes well again.

The key to this problem is because of case discordant. The Linux platform supports the case-sensitive naming system, while the Windows platform does not. The good news is [Windows 10 now offers an optional case-sensitive file system](https://www.howtogeek.com/354220/how-to-enable-case-sensitive-folders-on-windows-10/).

Even though I have described the same problem in my [previous post](https://shanguangyu.com/articles/why-should-you-lowercase-your-filename/), but when a similar error occurs, I still forgot it. Here, I would like to remind myself again that when dealing with a project between Linux and Windows platforms, we should consider this kind of case discordant problem.

