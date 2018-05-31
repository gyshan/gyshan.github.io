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
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/SR0.gif?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDujMtb7YIPrKT407JUBvyaWcHpK5lvI1a%26q-sign-time%3D1527753741%3B1527755541%26q-key-time%3D1527753741%3B1527755541%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Da3ae8d21042c4a5c9da87062eb76351ea9c1250c&token=e8d5d397053643eca398199a2a550963e3af057410001&clientIP=124.254.9.174&clientUA=b898f8d9-bed8-4811-b417-70d7f5e654ad" alt="image">
<figcaption>Fig 1: Shared Reference.</figcaption>
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/SR1.gif?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDIlX7NRbpnhWWgtijx47pnefWIKJl6CMq%26q-sign-time%3D1527753758%3B1527755558%26q-key-time%3D1527753758%3B1527755558%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dc7948ca10ef7dd1e58ea2551c97c811679672d5f&token=983a259fd8df29f894c3181c7a210c64a60e82f510001&clientIP=124.254.9.174&clientUA=e88f7c9b-1739-4f37-a879-717cc393bb25" alt="image">
<figcaption>Fig 2: Make a copy of variable instead of shared reference.</figcaption>
</figure>

When next time we want to use an assignment in python, think carefully if we really want shared reference, or just a copy.

Plus, thank [Philip Guo](http://pythontutor.com/) for his visualization tool.

