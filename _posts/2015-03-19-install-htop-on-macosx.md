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
<img src="https://dn-shanguangyu.qbox.me/top.png" alt="image">
</figure>

htop:
<figure >
<img src="https://dn-shanguangyu.qbox.me/htop.png" alt="image">
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


