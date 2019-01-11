---
title: 安装 Composer
categories: guide
tags: [composer]
date: 2016-06-01
---

*站长不是程序员，当然对这些的了解没那么深刻，若有表述错误，欢迎指正，谢谢。*

Composer 是一个 PHP 模块库安装助手，类似于 npm 之于 Nodejs 的作用。

事实上，PHP 一样在新发展，新的模块、新的特性，目前很多新开发的 PHP 源码已经大量使用新的技术，而通过 Composer 就可以轻松安装所需要的依赖了，而不需要用户一个一个的去安装。只要在程序声明一下依赖关系，一条命令就可以搞定。
同样的，有了 Composer 也促进了 PHP 的发展，程序员开发时候不再局限于过去原有的限制，也不需要担心用户使用的环境，都可以放心应用最新的技术资源，就算用户使用的虚拟主机环境很陈旧，也可以通过 Composer 更新依赖。

Composer 官方网站：http://getcomposer.org
国内非官方的中文网站： http://phpcomposer.com

安装 Composer 很简单，VPS 的话，以下两条命令即可：
```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```
*Note: 第一条是使用 curl 下载官方最新版本，第二条则是复制到 `/usr/local/` 目录，指定成全局可引用的命令。*

所以，以后要是需要 Composer ，只需到程序目录运行 Composer 的安装命令即可，例如： `composer install`

既然是定位于 PHP 服务，虚拟主机当然也可以使用，当然虚拟主机无法设置成全局。需要手动去[官网](https://getcomposer.org/download/)下载 *composer.phar* （扩展名就是.phar），例如目前最新的的1.1.2版本 <https://getcomposer.org/download/1.1.2/composer.phar>
然后通过 `php composer.phar install` 进行安装，嗯，就是多了 php 来驱动。