
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

鼠标右键点击左下角的开始徽标，打开PowerShell窗口（使用PowerShell窗口因为漂亮些），输入以下命令（注，必须加英文双引号，名字随便取和）：
`ssh-keygen -t ed25519 -C "SSH-Key"` 

    Generating public/private ed25519 key pair.
    Enter file in which to save the key (C:\Users\thedo/.ssh/id_ed25519): 
这是问你生成的密钥保存在那里，默认是
Enter passphrase (empty for no passphrase): (密码,如果想使用时不输密码,留空即可)
(回车,返回结果)
Enter same passphrase again: (再次确认密码,留空的还是直接回车)
(回车,返回结果)
Your identification has been saved in /home/xxx/.ssh/id_ed25519.
Your public key has been saved in /home/xxx/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx XXX(这几位是最上面填写的名称,在在公钥最后显示)
The key's randomart image is:(返回的随即生成图形)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTc2Njg5NTE2LC0xOTM4NTA1Mzk4LDE5Mz
Q2NzM2MDgsMTU2MDUyMzkwMV19
-->