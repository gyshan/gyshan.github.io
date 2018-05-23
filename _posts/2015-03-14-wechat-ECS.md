---
title: "阿里云ECS搭建微信公众平台"
excerpt: "ECS+Gunicorn+Supervisor+WeRoBot"
categories:
  - articles
tags:
  - WeChat
---


最初微信公众平台是架设在SAE上，还是比较省心，后来增加了一个查文献的需求，对XML文档解析时无论怎样调试都报错，研究了很久之后发现并不是我的问题，其中一个很重要的解析包依赖C库，而SAE平台是不支持C语言的，于是我便选择自己搭建后台。


{% include toc %}

## 购买服务器

我是在阿里云上买的服务器，新用户可以申请6个月的免费试用，最大的缺点就是没有公网IP。我升级了1M的公网IP，花了100多块钱的银子，还算实在，升级后主要配置为：

1. OS Ubuntu 14.04 64位
2. CPU 1核
3. 内存 1GB
4. 带宽 1M
5. 地域 北京

如果后台暂时没有过多的访问人数，这个就足够了，用户增长后，可以弹性升级配置，下面我们需要部署一个适合开发的Python环境。

## 主要组件展示

1. Ubuntu
2. [Nginx](http://docs.gunicorn.org/en/latest/deploy.html#nginx-configuration)
3. [Gunicorn](http://docs.gunicorn.org/en/latest/)
4. Python
5. Pip
6. Virtualenv
7. Flask
8. [Supervisor](http://supervisord.org/configuration.html)
9. WeRoBot SDK

简单说下主要逻辑关系，我们用Nginx作为Web服务器，该服务器无法直接和Flask (or Python)交互，所以我们需要引入Gunicorn，它是一个独立的WSGI容器，可以容纳WSGI应用并且提供HTTP服务。而后，用Supervisor 管理服务器进程，当某个应用挂掉，可以自动重启。

## 安装Virtualenv及必要组件

用来创建不同的Python隔离环境，可以保证一个干净的环境。
{% highlight bash %}
$ adduser newuser
$ sudo apt-get update 
$ sudo apt-get install zsh # 强烈推荐该shell
$ sudo apt-get install -y python python-pip python-virtualenv nginx gunicorn # 安装各类组件

$ sudo mkdir /home/mirror && cd /home/mirror 
$ sudo virtualenv test # 此时在mirror文件夹下创建一个虚拟环境

$ cd /home/mirror/test 
$ sudo source ./bin/activate # 激活虚拟环境

# 取消激活命令为
deactivate
{% endhighlight %}

## 安装Flask & WeRoBot SDK

{% highlight bash %}
$ sudo pip install flask
$ sudo pip install flask_werobot
$ sudo vim app.py 
{% endhighlight %}

Elementary code in app.py:
{% highlight python %}
from flask import Flask
from flask.ext.werobot import WeRoBot

app = Flask(__name__)
robot = WeRoBot(app, token = "Yourtoken", rule = '/test')

@robot.handler
def echo(message):
    return 'Hello World'
{% endhighlight %}

然后去微信公众平台把Token改为你自己设置的Token。

## 文件树展示

上面配置好了以后，你的目录应该会长成这个样子。
{% highlight text %}
home/mirror //用户目录
├── logs
└── test //项目目录
	├── bin
	│   ├── activate
	│   ├── easy_install
	│   ├── gunicorn
	│   ├── pip
	│   └── python
	├── include/
	├── lib/  
	├── local
	│   ├── bin 
	│   ├── include 
	│   └── lib 
	└── app.py //主程序
{% endhighlight %}

## 配置 Nginx
{% highlight bash %}
$ sudo /etc/init.d/nginx start	#启动nginx

$ sudo rm /etc/nginx/sites-enabled/default	#删除默认配置
$ sudo touch /etc/nginx/sites-available/test	#建立项目文件
$ sudo ln -s /etc/nginx/sites-available/test /etc/nginx/sites-enabled/test	#设置软链接

$ sudo vim /etc/nginx/sites-enabled/test	#编辑项目文件
{% endhighlight %}

添加：
{% highlight text %}
server {
    location / {
        proxy_pass http://127.0.0.1:8000;
    }
}
{% endhighlight %}
当HTTP请求得到`/`，便会反向代理到`127.0.0.1`8000端口。
重启 nginx:
{% highlight bash %}
$ sudo /etc/init.d/nginx restart
{% endhighlight %}

## 配置 Supervisor
{% highlight bash %}
$ sudo apt-get install -y supervisor	#安装
$ sudo vim /etc/supervisor/conf.d/test.conf	#创建配置文件
{% endhighlight %}
添加：
{% highlight text %}
[program:test]

command = /home/mirror/test/bin/gunicorn app:app -b localhost:8100
directory = /home/mirror/test
timeout = 60*60
user = mirror
autostart = true
autorestart = true
redirect_stderr = true
stdout_logfile = /home/mirror/logs/supervisor.log
{% endhighlight %}

## 启动Supervisor
{% highlight bash %}
$ sudo supervisorctl reread
$ sudo supervisorctl update
$ sudo supervisorctl start test

## 重启supervisor
$ sudo supervisorctl restart test
{% endhighlight %}

## 微信平台端设置

进入微信公众平台--->开发者模式--->设置URL和Token
<figure >
<img src="https://dn-shanguangyu.qbox.me/wechat.png" alt="image">
</figure>

如果配置没有问题，顺利通过，用微信给你的公众平台发消息应该能看到'hello world!'。

**Tips:** 出现任何问题，重启supervisor，倘若仍不能够解决，请查看log文件。
{: .notice}

## 参考

1. [werobot](https://flask-werobot.readthedocs.org/en/latest/)
2. [VPS环境搭建详解](http://beiyuu.com/vps-config-python-vitrualenv-flask-gunicorn-supervisor-nginx/)
3. [Flask on Ubuntu](https://realpython.com/blog/python/kickstarting-flask-on-ubuntu-setup-and-deployment/#disqus_thread)

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
