---
title: Wordpress 一键化安装
categories: guide
tags: [wordpress]
date: 2016-06-12
---

Wordpress 大家都熟悉，这里就不作详细介绍了，假如你是用 VPS 建站的，那么以下是一键安装命令集。即使虚拟主机，只要可 SSH 账户登陆也可使用。

首先 VPS 已经安装好 PHP 环境，常见如 Lnmp 一键包，绑好域名，进入你的网站根目录，一般是  `/home/wwwroot/xxx.com`

然后输入如下命令集合，即可完成安装前的准备工具，不再需要上传下载代码：

```
wget https://wordpress.org/latest.tar.gz && tar xzf latest.tar.gz && mv wordpress/* . && rm -rf latest.tar.gz wordpress && chown -R www:www * 
```

Note：如果是虚拟主机，那最后的命令 `chown -R www:www *` 是不需要的。

另: 现在最新版本的WP已经集成多语言（2015/08/31），安装时候可以自由选择语言，已经不需要去 <http://cn.wordpress.org> 下载中文版本。