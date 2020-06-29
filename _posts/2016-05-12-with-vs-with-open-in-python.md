---
title: "open() vs with open() in python"
excerpt: "You should use `with` statement when performing file IO"
categories:
  - articles
tags:
  - Python
---

Ever curious whether `open()` and `with open()` in python mean the same thing? Recently, I found the explanation at [Understanding Python's "with" statement](http://effbot.org/zone/python-with-statement.htm). Basically, using `with` statement just ensures that you don't forget to `close()` the file.

