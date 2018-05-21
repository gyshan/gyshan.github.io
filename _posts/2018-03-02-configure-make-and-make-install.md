---
title: "Configure, make and make install"
excerpt: "Magic behind software installation"
categories:
  - articles
tags:
  - Bioinformatics
---

Install software from source on Linux platform is an extremely common task. I've typed those commands a lot, but I did not understand it very well before. After reading this article[^1] wrote by George, I gradually understand those magic incantation.

{% highlight bash %}
./configure
make
make install
{% endhighlight %}

In short, `configure` makes sure that the system environment is ready to build the software, such as standard libraries and components are in the right place, `make` read commands from *Makefile* and compile the software, `make install` also read commands from *Makefile* and install the software to specified directory.

1.configure

The `configure` step is aimed to produce *Makefile* from *Makefile.in*. At this step, user can define installation directory by `./configure --prefix=/mypath`, especially when the user did not have root privilege. For more information, use `./configure --help`.

2.make

The `make` step is aimed to use *Makefile* to build the software. 

3.make install

The `make install` step is aimed to use *Makefile* to install the software.


Hope everyone goes well with software installation!


[^1]: [The magic behind configure, make and make install](https://robots.thoughtbot.com/the-magic-behind-configure-make-make-install)

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
