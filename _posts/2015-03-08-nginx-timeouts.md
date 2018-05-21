---
title: "解决使用 NGINX & Gunicorn 的 504 Timeouts 问题"
excerpt: "Code for 504 timeouts."
tags: 
  - WeChat
  - NGINX
last_modified_at: 2017-03-09T12:26:59-05:00
---


## 问题描述
最近一直在开发一个微信公众号，由于后台计算量较大，nginx常出现`timeout`问题，经过排查，已经解决。错误代码形如：

{% highlight text %}
14:12:16 web.1  | 2014-07-17 14:12:16 [30747] [INFO] Using worker: sync
14:12:16 web.1  | 2014-07-17 14:12:16 [30752] [INFO] Booting worker with pid: 30752
14:13:21 web.1  | 2014-07-17 14:13:21 [30747] [CRITICAL] WORKER TIMEOUT (pid:30752)
14:13:21 web.1  | 2014-07-17 03:43:21 [30752] [INFO] Worker exiting (pid: 30752)
14:13:21 web.1  | 2014-07-17 14:13:21 [30841] [INFO] Booting worker with pid: 30
{% endhighlight %}

## 解决方案

更改`gunicorn`配置文件，我用的是supervisor，故`vi /etc/supervisor/con.f/name.conf`添加一行`timeout = 60*60`，配置完成的name.conf文件如下：
	
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

更改`nginx`配置，补充一行`proxy_read_timeout 1200`，nginx默认为60秒。故`vi /etc/nginx/sites-enabled/test`，配置完成的test文件如下：


{% highlight text %}
server {
    listen 80;
    root /home/mirror/test;
    location / {
		proxy_pass http://127.0.0.1:8100;
		proxy_read_timeout 1200;
		}
    }
{% endhighlight %}

Done!

**温馨提示**: 若配置多个站点，需单独配置gunicorn.conf，然后被supervisor调用.
{:.notice}

---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>



	
	
	
	

	



