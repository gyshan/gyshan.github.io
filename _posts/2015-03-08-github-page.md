---
layout: post
title: 我的 GitHub Page 操作流
excerpt: My workflow of GitHub Page
modified: 2015-03-10
categories: articles
tags: [Mac]
<!-- image:
  feature: so-simple-sample-image-1.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/ -->
comments: true
share: true
---



刚开始学习[GitHub Page](https://pages.github.com/) 以及 [Jekyll](http://jekyllrb.com/)。

## 本地文件夹初始化，创建新仓库（初始化）

{% highlight bash %}
$ git init
{% endhighlight %}

## 检出仓库（初始化）

{% highlight bash %}
$ git clone username@host:/path/to/repository
{% endhighlight %}

## 工作流（每日常规）

**写文章**
{% highlight text %}
Writing blog
{% endhighlight %}

**本地预览**	
{% highlight bash %}
$ bundle exec jekyll serve
{% endhighlight %}

**提交工作目录到暂存区**	
{% highlight bash %}
$ git add --all .
{% endhighlight %}

**生成暂存区快照并提交至HEAD**	
{% highlight bash %}
$ git commit -m "代码提交信息"
{% endhighlight %}

**HEAD push 到远端仓库**	
{% highlight bash %}
$ git push origin gh-pages
{% endhighlight %}

## Done!

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>

	

	



