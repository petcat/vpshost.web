
---
title: 
categories: guide
tags: [Key ED25519]
date: 2019-03-01

---
无论VPS还是独服，机器到手的第一件事就是禁止密码登录，替换成证书登录。因为安全。

其实换成证书登录非常简单，使用上也非常方便。

1、首先需要生成证书，Putty、Xshell都可以，事实上如果你是使用Windows 10，并保持更新，只需要打开CMD命令窗口，同样可以。
Xsheall 是最为简单的，图形化窗口，工具-----新建用户密钥生成向导，向导模式，简单点下一步就可以了，而putty和cmd窗口都是使用命令生成。下面介绍下使用Windows 10系统CMD窗口来生成。

鼠标右键点击左下角的开始徽标，打开PowerShell窗口（使用PowerShell窗口因为漂亮些），输入以下命令（注，必须加英文双引号，名字随便取）：
`ssh-keygen -t ed25519 -C "SSH-Key"` 

    Generating public/private ed25519 key pair.
    Enter file in which to save the key (C:\Users\thedo/.ssh/id_ed25519): 

这是问你生成的密钥保存在那里，默认文件名是 **id_ed25519** ，默认直接回车，不过建议保存到D盘根目录 D:\ssh-key 这样方便找。C盘根目录可能有权限问题失败。

>>>Enter passphrase (empty for no passphrase):          
Enter same passphrase again:       

这是问你密码，和再次确认密码，就是证书读取密码，不设密码就直接回车。只要你保存好私钥，可以不设密码。

Your identification has been saved in D:\ssh-key.     
Your public key has been saved in D:\ssh-key.pub.      
The key fingerprint is:       
SHA256:xsJIhlo+7z8Zk/rVt4pDgt1xUCni6z54bBxgs8b5gB0 SSH-Key       
The key's randomart image is:   

没错，这样就完成了，打开你的D盘根目录，其中ssh-key是你私钥，一定要保管好，以后都要用，而 ssh-key.pub 是公钥，是放上VPS上的，丢了也没关系，私钥里面也包含公钥的内容。   

2、将公钥放到VPS上，用任意文本编辑器，如Notepad++、Sublime Text等打开公钥文件，你会看到类似于 `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMTpjYMlckGmEUzJrHDxEzZaR6VGJ1Js7Z6LT9GeM8ne SSH-Key-ED25519` 的一行，这就是你的公钥，你需要把它上传到你的VPS，方式一，用 echo 命令写入（将下面改成你的）：

echo `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMTpjYMlckGmEUzJrHDxEzZaR6VGJ1Js7Z6LT9GeM8ne SSH-Key-ED25519` > /root/.ssh/authorized_keys 

方式二，直接将你的公钥文件ssh-key.pub改成authorized_keys，并上传到 /root/.ssh 目录，最后给目录和文件设置读写权限，命令： `chmod 600 /root/.ssh &&  chmod 700 /root/.ssh/authorized_keys`

有多台VPS就重复上面的做法，把你所有的VPS，都如此加上密钥。如果你只有一台VPS，那么你可以直接在VPS上生成，命令是一样的 `ssh-keygen -t ed25519 -C "SSH-Key"`，但是你要把私钥下载下来才能使用，VPS上不建议保存私钥备份。也不建议每一台VPS都生成一套密钥，这样你需要保管和使用多套密钥，会增加混乱和麻烦。

一个专业性的建议是：你可以分别生成两套密钥，重要机器使用一套；玩具、试用、测试等则用另一套。相当于做一个隔离。

3、禁止密码登录、修改默认端口。

使用证书登录了，当然要把不安全的密码登录禁止掉，因为密码存在着暴力猜解的可能，要使密码又复杂又好记，事实上很难做到，很多时候，大多数人往往就是都对自己设置的密码过分自信。尤其现在那么多的拖库事件。编辑 /etc/ssh/sshd_config 找出以下三项并修改：

> #Port  22
> #AuthorizedKeysFile     .ssh/authorized_keys .ssh/authorized_keys2
> #PasswordAuthentication yes


第一行是修改端口，第二行是允许证书，第三行就是密码登录。**#**是注释符，去掉**#**后修改才能生效，端口改成你喜欢的，比如改成3389，假装是Windows远程连接，将yes改成no就是禁止密码登录，对于新手，这里建议暂时保留22 ：

>Port  22
>Port  3389
>AuthorizedKeysFile     .ssh/authorized_keys 
>PasswordAuthentication  no

暂时保留的用处是万一遇到端口没有放行（这在CentOS很常见）不至于没法连接。修改后，重启 SSH 服务 命令： `service ssh restart` 或  `/etc/init.d/ssh restart` 或 `systemctl restart ssh` 都对（视版本不同），当然，直接重启系统，反正是新机器一开始的设置，重启

4、大功告成。以后你就可以使用你的私钥连接你的VPS了，安全大大增加。


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcwNTUyMjM5NSwxMDE0MzQ4NTI2LDE3Nj
EzNDIyMTAsLTE5Mzg1MDUzOTgsMTkzNDY3MzYwOCwxNTYwNTIz
OTAxXX0=
-->