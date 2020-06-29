---
title: "Linux redirection"
excerpt: "What is the meaning of 2>/dev/null"
categories:
  - articles
tags:
  - Linux
---


{% highlight bash %}
2>/dev/null
{% endhighlight %}

In linux, there are three main file descriptors `{0：stdin, 1: stdout, 2: stderr}` and a "black hole" `/dev/null`, everything you write in it will disappear permanently.



In this case, `2>/dev/null` is refers to redirect standard error message into null, if you want to ignore error message, you should have a try.

