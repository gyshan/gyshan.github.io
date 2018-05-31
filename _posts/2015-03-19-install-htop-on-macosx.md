---
title: "Mac OS X 安装 htop"
excerpt: "Install htop on Mac OS X"
categories:
  - articles
tags:
  - Mac
---


在Linux下一直使用htop进行进程查看，今日在Mac上也装了一个。htop是一款Linux系统监控与进程管理软件，与top只提供最消耗资源的进程列表不同，htop提供所有进程的列表，并且使用彩色标识出处理器、swap和内存状态，可以实现更方便、更加人性化的进程管理。

top:

<figure >
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/top.png?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDzs92mXm1QBi0G6LrvjnQ0oAerzN9OeKT%26q-sign-time%3D1527753586%3B1527755386%26q-key-time%3D1527753586%3B1527755386%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3D821eade6e6976e4f1adfd8a2dc6815bc27eb1fdb&token=da035f8311c280781579557d244ab2c7ee089f6e10001&clientIP=124.254.9.174&clientUA=11b9911a-bfda-4ef9-8b4f-6fbaac40101c" alt="image">
</figure>

htop:
<figure >
<img src="https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/htop.png?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKIDtfMrzO6kQY0GC2Q2beqjgl1V2L4fcKSA%26q-sign-time%3D1527753607%3B1527755407%26q-key-time%3D1527753607%3B1527755407%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Da2baa577bed9446726fab2781fbc42c5b08542a2&token=429fc3136340faae322495ab4961179b4be2518310001&clientIP=124.254.9.174&clientUA=153d3902-07e6-414b-882a-4dab109756ae" alt="image">
</figure>

---
在Linux下可以直接`apt-get install htop`安装，但在Mac下需要改变一点点内容。

Command：
{% highlight bash %}
$ curl -O http://themainframe.ca/wp-content/uploads/2011/06/htop.zip
$ unzip htop.zip
$ sudo mv htop /bin
$ rm htop.zip
{% endhighlight %}

Done!


