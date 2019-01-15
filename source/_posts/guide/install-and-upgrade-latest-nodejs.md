---
title: Debian / Ubuntu 新安装、升级 Node.js 最新版本的姿势）
categories: guide
tags: [Node.js]
date: 2019-01-13
---

有两种方法，下载官方的源码编译安装，和包安装；

1、编译安装没啥说的，首先去官网下载 https://nodejs.org/en/download/ 

比如写这篇文章时候是10.15正式版就是 https://nodejs.org/dist/v10.15.0/node-v10.15.0.tar.gz

要是想安装其它旧的版本？可以这里找 https://nodejs.org/dist/

其实目录结构你仔细看一眼，也不用找了， **https://nodejs.org/dist/+版本号+node-版本号.tar.gz** 对应版本号填进去就是。 

下载回来解压缩，cd 进去目录，`./configure && make && make install`  三连击就是了。

2、编译安装是非常耗时的，当然你机器性能好、网络好另说，所以，很推荐使用包管理安装。秒装好

安装也很简单，这里就有说明， https://github.com/nodesource/distributions/blob/master/README.md

支持版本：Debian 8以后的版本，ubuntu 16.04以后版本（ubuntu 14.04 不支持 Node.js 10 以后版本）

Debian 的：

    # Node.js v11.x 版本
    curl -sL https://deb.nodesource.com/setup_11.x | bash -
    apt-get install -y nodejs
    
    # Node.js v10.x 版本
    curl -sL https://deb.nodesource.com/setup_10.x | bash -
    apt-get install -y nodejs
    
    # Node.js v8.x 版本
    curl -sL https://deb.nodesource.com/setup_8.x | bash -
    apt-get install -y nodejs
    
    # Node.js v6.x 版本
    curl -sL https://deb.nodesource.com/setup_6.x | bash -
    apt-get install -y nodejs

Ubuntu 的：

    # Node.js v11.x 版本
    curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
    sudo apt-get install -y nodejs
    
    # Node.js v10.x 版本
    curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
    sudo apt-get install -y nodejs
    
    # Node.js v8.x 版本
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    sudo apt-get install -y nodejs
    
    # Node.js v6.x 版本
    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    sudo apt-get install -y nodejs

---

上面是全新安装的姿势，可你知道 Node.js 版本升级更新是很频繁，从v0.1涨到目前的 v11.x 安装后不久就会出新版本，添加、支持更多的新特性，也修复旧版的Bug，所以用不了多久就要又升级，不过升级方法很简单，如下：使用 `npm n` 命令就可升级，

1. 首先清除 npm 缓存，防止升级出错，w命令： `npm cache npm cache clean -f`
2. 接着安装 n 模块，命令： `npm install -g n`
3. 现在可以使用 `n ls` 查看所有的 nodejs 版本，等于是查看 https://nodejs.org/dist/
4. 然后就可以开始升级了：自动安装到最新的稳定版本命令是 `n stable`，自由选择版本安装是`n 10.15.0`（版本号）

备注：升级前后可先使用`node -v` 查看版本。当然，你也可以重新下载源码，再编译安装新的版本。但显然没这个必要。
