---
layout: post
title: 几道小题
excerpt: "Example code for basic interview questions by python."
modified: 
categories: articles
tags: [Python]
comments: true
share: true
---

* Table of Contents
{:toc}

## 1. 字典操作

{% highlight python %}
# Question: get two dict d1 and d2, yield d3.
d1 = {"a1":"b1", "a2":"b2", "a3":"b3"}
d2 = {"b1":"c1", "b3":"c3"}
d3 = {"a1":"c1", "a3":"c3"}

# Answer
d3 = {}
d1 = dict(zip(d1.values(),d1.keys()))
for k, v in d2.iteritems():
	d3[d1[k]] = v
print d3

{% endhighlight %}

## 2. 随机产生20个字符
{% highlight python %}
import string
import random

''.join(random.choice(string.ascii_lowercase) for _ in range(20))

{% endhighlight %}

## 3. 冒泡排序
{% highlight python %}

def bubbleSort(list):
	for i in xrange(len(list)-1, 0, -1):
		for j in xrange(i):
			if list[j] > list[j+1]:
				list[j], list[j+1] = list[j+1], list[j]
	return list

{% endhighlight %}

## 4. 有序列表合并
{% highlight python %}
def mergeSortedLists(a, b):
    l = []
    while a and b:
        if a[0] < b[0]:
            l.append(a.pop(0))
        else:
            l.append(b.pop(0))
    return l + a + b
{% endhighlight %}

## 5. 快速排序
{% highlight python %}
def qsort(ary):
	if len(ary)<=1:
		return ary
	else:
		return qsort([x for x in ary[1:] if x<ary[0]]) + [ary[0]] + qsort([x for x in ary[1:] if x>=ary[0]])
	
{% endhighlight %}

## 6. Fibonacci
{% highlight python %}
def fib(n):
	a, b = 1, 1
	for i in range(n-1):
		a, b = b, a+b
	return a
{% endhighlight %}

## 6. 字符串反转
{% highlight python %}
# s[start:end:step]

a = 'abcde'
ra = a[::-1]

{% endhighlight %}

## 7. 两数组相同元素计数
{% highlight python %}

def match_arrays(v, r):
    return sum(1 for x in v if x in r)

{% endhighlight %}

## 8. 元音替换
{% highlight python %}
# 'this is my string' -> 'th3s 6s mt str15ng'
def vowel_2_index(string):
    vowels = 'aeiouAEIOU'
    return ''.join(x if x not in vowels else str(n + 1) for n,x in enumerate(string))

{% endhighlight %}

## 9. 检测两字符串是否有共同子串
{% highlight python %}
#("Something", "Home") -> True
def substring_test(str1, str2):
    for n in xrange(len(str2)-1):
        if str2[n:n+2].lower() in str1.lower():
            return True
    return False
{% endhighlight %}

## 10. 两奇数间插破折号
{% highlight python %}
# '1003567' -> '1003-567'
import re

def insert_dash(num):
    return re.sub(r'([13579])(?=[13579])', r'\1-', str(num))
{% endhighlight %}

## 11. Fibonacci（快速+负区间）
{% highlight python %}
from numpy import matrix

def fib(n):
    return (matrix(
        '0 1; 1 1' if n >= 0 else '-1 1; 1 0', object
        ) ** abs(n))[0, 1]

{% endhighlight %}



---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
