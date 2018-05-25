---
title: "Why should you lowercase your filename"
excerpt: "Lowecase filename is important"
categories:
  - articles
tags:
  - Mac
---

Yesterday, I began to transfer my git configuration from my old machine to my new Macbook Pro. When I rename my file by doing this, an error occured to me:

{% highlight bash %}
$ git mv readme Readme
fatal: destination exists, source=readme, destination=Readme
{% endhighlight %}


It seems like my Mac OS X cannot recognize `Readme` file as same as `readme` file. So I had to convert `readme` file to `tmp_file` and then `tmp_file` to `Readme` file. In Linux, this command can work very well, but in Mac OS X, failed. This is the first time that I realized case-sensitive is so important. Except for this situation, I believe it is very dangerous if keep confusing the case.

Different operating systems (OS) have different case-sensitive level, that is why same command upon can work well on Linux but failed on Mac OS X.

* case-sensitive OS: Linux, Solaris, BSD 
* case-insensitive OS: Windows, Mac OS X

In my working pipeline, my file often transfer between Linux and Mac OS X, so I decide to convert all my filename under **lowercase_with_underscore** principle. The reasons behind this principle are:

* Easy to read, UPPERCASE_WITH_UNDERSCORE is hard to read 
* Easy to distinguish private file from system folder/file such as `Documents` , `Downloads` and so on
* Transfer file with lower risk (Every OSs can recognize your file correctly)
* I love underscore sign





---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
