---
layout: post
title: Setup sftp plugin for sublime
excerpt: SFTP setting protocal
modified:
categories: articles
tags: [Mac]
comments: true
share: true
---



I do not want to use [vi](https://en.wikipedia.org/wiki/Vi) in remote server, especially when dealing with large amounts of coding work. Instead, I want to write code in my laptop with [sublime](https://www.sublimetext.com/), and make it simultaneously sync to a remote server. 

[SFTP](https://wbond.net/sublime_packages/sftp), a plugin for sublime can deal with the problem above, which can map a local folder/file to remote folder/file. Here is how I setup this plugin.

* Table of Contents
{:toc}


## Install Package Control Package

* Open Sublime console by pressing `Ctrl` +`~`
* Copy the long command below and press `Enter`

Sublime Text 2

{% highlight bash %}

import urllib2,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')

{% endhighlight %}



Sublime Text 3

{% highlight bash %}

import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

{% endhighlight %}

* Restart Sublime

## Install SFTP



* Press `Command`/`Control`  + `Shift` +`P`
* Type `SFTP` and install

## Setup config file in json format

* Drag a folder to sublime and this folder will show up in the sidebar
* Right click on this folder and select `SFTP/FTP`  -> `Map to Remote...`
* A file named `sftp-config.json` will show up in this folder
* Change four field with your own customization: `host`, `user`, `password` and `remote_path` , save it.

{% highlight json %}

{
// The tab key will cycle through the settings when first created
// Visit http://wbond.net/sublime_packages/sftp/settings for help

// sftp, ftp or ftps
"type": "sftp",

"save_before_upload": true,
"upload_on_save": false,
"sync_down_on_open": false,
"sync_skip_deletes": false,
"sync_same_age": true,
"confirm_downloads": false,
"confirm_sync": true,
"confirm_overwrite_newer": false,

"host": "yourip",    <- Here is where you want to change
"user": "yourname",     <- Here is where you want to change
"password": "yourpassword",    <- Here is where you want to change  
//"port": "22",

"remote_path": "yourpath",  <- Here is where you want to change
"ignore_regexes": [
    "\\.sublime-(project|workspace)", "sftp-config(-alt\\d?)?\\.json",
    "sftp-settings\\.json", "/venv/", "\\.svn/", "\\.hg/", "\\.git/",
    "\\.bzr", "_darcs", "CVS", "\\.DS_Store", "Thumbs\\.db", "desktop\\.ini"
],
//"file_permissions": "664",
//"dir_permissions": "775",
//"extra_list_connections": 0,
"connect_timeout": 30,
//"keepalive": 120,
//"ftp_passive_mode": true,
//"ftp_obey_passive_host": false,
//"ssh_key_file": "~/.ssh/id_rsa",
//"sftp_flags": ["-F", "/path/to/ssh_config"],
//"preserve_modification_times": false,
//"remote_time_offset_in_hours": 0,
//"remote_encoding": "utf-8",
//"remote_locale": "C",
//"allow_config_upload": false,
}

{% endhighlight %}



## Enjoy coding

* Right click your code in this folder and choose `SFTP/FTP`
* Then you can do whatever you want to do, such as `Upload File`, `Download File` ...



---
Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA </a>
