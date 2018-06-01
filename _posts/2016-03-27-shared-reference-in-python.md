---
layout: post
title: Shared reference in python
excerpt: Shared reference trap
modified: 2016.03.27
categories: articles
tags: [Python]
comments: true
share: true
---

Shared Reference is an extremely common trick in python programming language, which means that a single object can be able to be referenced by multiple variables. 

In Fig 1, L1 is an object of a list. The assignment statement `L2 = L1` enables L2 to share the memory space of L1, it will turn up that L1 and L2 share the same memory space. In other words, L2 will change simultaneously with L1.

<figure>
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/SR0.gif" alt="image">
<figcaption>Fig 1: Shared Reference.</figcaption>
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/SR1.gif" alt="image">
<figcaption>Fig 2: Make a copy of variable instead of shared reference.</figcaption>
</figure>

When next time we want to use an assignment in python, think carefully if we really want shared reference, or just a copy.

Plus, thank [Philip Guo](http://pythontutor.com/) for his visualization tool.

