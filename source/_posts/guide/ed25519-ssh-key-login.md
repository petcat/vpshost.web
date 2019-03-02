
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

2、将公钥放到VPS上，用任意文本编辑器，如Notepad++、Sublime Text等打开公钥文件，你会看到类似于 `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMTpjYMlckGmEUzJrHDxEzZaR6VGJ1Js7Z6LT9GeM8ne SSH-Key-ED25519` 的一行，这就是你的密钥


echo `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMTpjYMlckGmEUzJrHDxEzZaR6VGJ1Js7Z6LT9GeM8ne SSH-Key-ED25519` > /root/.ssh/authorized_keys 

chmod 600 /root/.ssh &&  chmod 700 /root/.ssh/authorized_keys


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNzA0NDcwNDksMTc2MTM0MjIxMCwtMT
kzODUwNTM5OCwxOTM0NjczNjA4LDE1NjA1MjM5MDFdfQ==
-->