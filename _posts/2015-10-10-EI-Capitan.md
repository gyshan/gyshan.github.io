---
title: "Mac升级到EI Capitan后Git无法使用的问题"
excerpt: "A solution for git crush on mac"
categories:
  - articles
tags:
  - Mac
---

## 问题描述
{% highlight bash %}
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
{% endhighlight %}



## 解决方案
重新下载安装`Xcode`，并且安装`Xcode Command Line Tools`。

{% highlight bash %}
xcode-select --install
{% endhighlight %}

完成后，git便可以重新使用了。

