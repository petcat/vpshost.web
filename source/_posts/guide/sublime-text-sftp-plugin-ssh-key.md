---
title: Sublime Text 编辑器 sftp 插件使用 ssh key 的正确姿势
categories: guide
tags: [sublime, sublime text]
date: 2016-06-03
---

Sublime Text sftp 插件是个神器，以后直接就可以在 Sublime Text 编辑修改内容了，不需要使用的 sftp/FTP 工具登陆再修改代码了，可是我一直安装后没搞定，无它，我是使用SSH密钥登录服务器的而不是密码，而恰好这里遇到了问题。

以下就是 Sublime Text sftp 插件的默认配置， 

```
{
    // The tab key will cycle through the settings when first created
    // Visit http://wbond.net/sublime_packages/sftp/settings for help
    
    // sftp, ftp or ftps
    "type": "sftp",

    "sync_down_on_open": true,
    "sync_same_age": true,
    
    "host": "example.com",
    "user": "username",
    //"password": "password",
    //"port": "22",
    
    "remote_path": "/example/path/",
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
```

大家一看就很好理解，主机名、IP，端口，用户名密码等等，很好解理也很好修改，要是密码登陆就没啥问题的，可问题关键很多人像我一样是使用 SSH 密钥登陆管理，问题就卡在倒数第二段的 `"ssh_key_file": "~/.ssh/id_rsa",` 配置上了。

都知道这行是配置密钥路径的，但是怎么配置都不对。例如我自己的密钥是放在 `D:\sshkey\sshkey.ppk` 目录里，要是 直接把路径填上去吧，不好意思，填的时候， Sublime Text 就直接提示代码飘红了，出错了，先不管，填上去，一测试果然是错的，无法连接上机器。 明知错在  `\` 上，这我是知道，Windows 与 Linux 路径表示上的斜杠是不同方向的，按 Windows 格式  `\` 是不对，但是换成 Linux 格式  `/` 也是不对啊，怎么办，什么才是正确使用姿势？搜索好多文章，终于搞定了，原来是这样转换的：`"ssh_key_file": "D:\/sshkey\/sshkey.ppk",`  实质就是把 Windows 与 Linux 的路径斜杠都加上就可以了，囧 -_-