---
title: "Transfer files in the background between servers"
excerpt: "Solution for file transferring"
categories:
  - articles
tags:
  - Bioinformatics
---

Sometimes, We need to transfer files between servers in the background, and it is imperative to have a password. The solution is to use screen command to emulate a screen and make it running in the background.


{% highlight bash %}
$ screen   # [1]
$ rsync -avz hostname@XXX.XXX.XX.X:/data/path ./   # [2]
Enter your password:   # [3]

Press `control`+`A`   # [4]
Press `D`   # [5] 
{% endhighlight %}

Here, your job is running in the background. If you want to check the running job, type the commands below:

{% highlight bash %}
$ screen -ls   # Show screen sessions
$ screen -r [session you want to enter]   # Enter specific screen session
$ screen -X -S [session you want to kill] quit   # Kill specific screen session
{% endhighlight %}




