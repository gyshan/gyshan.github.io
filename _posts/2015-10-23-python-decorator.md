---
title: "Python Decorator"
excerpt: "Example code of python decorator"
categories:
  - articles
tags:
  - Python
---

{% include toc %}


## 函数
在Python中，一切函数皆对象。函数作为Python中的一等公民，可以进行很多有用的操作：

* 将函数赋给变量
{% highlight python %}
def greet(name):
    return "hello "+name

greet_someone = greet
print greet_someone("John")

# Outputs: hello John
{% endhighlight %}
* 在函数里定义其他函数
{% highlight python %}
def greet(name):
    def get_message():
        return "Hello "

    result = get_message()+name
    return result

print greet("John")

# Outputs: Hello John
{% endhighlight %}
* 函数可以作为参数传递给其他函数
{% highlight python %}
def greet(name):
   return "Hello " + name 

def call_func(func):
    other_name = "John"
    return func(other_name)  

print call_func(greet)

# Outputs: Hello John
{% endhighlight %}
* 函数可以返回其他函数
{% highlight python %}
def compose_greet_func():
    def get_message():
        return "Hello there!"

    return get_message

greet = compose_greet_func()
print greet()

# Outputs: Hello there!
{% endhighlight %}
* 内部函数可读取外参
{% highlight python %}
def compose_greet_func(name):
    def get_message():
        return "Hello there "+name+"!"

    return get_message

greet = compose_greet_func("John")
print greet()

# Outputs: Hello there John!
{% endhighlight %}


## 装饰器
先看一个形象的例子
{% highlight python %}
class entryExit(object):

    def __init__(self, f):
        self.f = f

    def __call__(self):
        print "Entering", self.f.__name__
        self.f()
        print "Exited", self.f.__name__

@entryExit
def func():
    print "inside func()"

func()

# Outputs: 
# Entering func
# inside func()
# Exited func
{% endhighlight %}

装饰器作为一种语法糖可以使用函数作为参数并且返回函数。在这个例子里，Python提供语法糖来连接`entryExit`和`func`函数，省却了`func = entryExit(func)`这样的繁复表达。一方面提供更加简洁的代码，另一方面不用改变原函数的函数名。

总的来说，装饰器能让你的程序更加优雅。当你需要扩展某个函数，却又不想修改它，尝试下装饰器吧。


## References

1. [A guide to Python's function decorators](http://thecodeship.com/patterns/guide-to-python-function-decorators/)
2. [Decorators for Functions and Methods](https://www.python.org/dev/peps/pep-0318/)
3. [Understanding Python Decorators in 12 Easy Steps!](http://simeonfranklin.com/blog/2012/jul/1/python-decorators-in-12-steps/)

