---
layout: post
title: Sublime 安装 PEP8 
excerpt: "install PEP8 within Sublime."
modified: 
categories: articles
tags: [Mac]
comments: true
share: true
---

Python 遵循一套`PEP8`代码规范，今天发现了一个 Sublime 下格式纠正的插件，甚是好用，记录如下。

## 安装插件

* `cmd+shift+P`>>`Package Control: Install Package`
* 找到`Python PEP8 Autoformat`这个包并安装

## 配置 User settings

找到User settings编辑如下内容，保存并退出。
`Preferences`>>`Package Settings`>>`Python PEP8 Autoformat`>>`Settings - User`
{% highlight text %}
{
    // autoformat code on save ?
    "autoformat_on_save": false,

    // enable possibly unsafe changes (E226, E24, W6)
    // aggressive level, 0 to disable:
    "aggressive": 0,

    // list codes for fixes; used by --ignore and --select
    "list-fixes": false,

    // do not fix these errors / warnings (e.g. ["E501", E4", "W"])
    "ignore": [],

    // select errors / warnings (e.g. ["E4", "W"])
    "select": [],

    // Maximum line length
    "max-line-length": 79
}
{% endhighlight %}



## 启用

找到写好的代码，用`ctrl+shift+r`纠正一下吧。


---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
