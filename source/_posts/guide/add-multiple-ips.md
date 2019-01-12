---
title: 服务器或 VPS 增加多个IP地址（Debian/Ubuntu篇）
categories: guide
tags: [多IP]
date: 2016-06-13
---

如果你的VPS或独立服务器，可以申请到多个IP，但又没有自动添加上去，需要你手动添加，可以看这里。

以下是永久添加方案，编辑 `/etc/network/interfaces` 添加上你的新IP，假设你原有IP为 11.11.11.11，需要添加 22.22.22.22 和 33.33.33.33 新IP，按以下样例修改：

>auto lo
iface lo inet loopback

>auto eth0
iface eth0 inet static
address 11.11.11.11
netmask 255.255.255.0
gateway 11.11.11.1

>auto eth0:0
iface eth0:0 inet static
address 22.22.22.22
netmask 255.255.255.0

>auto eth0:1
iface eth0:1 inet static
address 33.33.33.33
netmask 255.255.255.0

>dns-nameservers 8.8.8.8 8.8.4.4

Note: **gateway** 网关不用修改，只需要原来的那一组，只需要按着顺序添加 eth0:0 , eth0:1 , eth0:X 一直加下去，而 **address** IP地址改成你的新IP地址：（x改成你的）

>auto eth0:x
iface eth0:x inet static
address xx.xx.xx.xx
netmask 255.255.255.0

修改之后，用命令`/etc/init.d/networking restart` 重启网络，但这样新IP还不能用，还需要将新IP上线，命令： `ifup eth0:0` 有多个IP，就按顺序 `ifup eth0:1` `ifup eth0:2` `ifup eth0:3` `ifup eth0:x` …… 让新IP都上线可用。
大功告成！

Note: 对应的IP下线命令是 `ifdown eth0:X`  （**X**改成对应的数字，这里就不重复了）

现在就可以用上新加的IP了。