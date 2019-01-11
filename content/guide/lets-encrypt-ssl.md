---
title: Let's Encrypt SSL 免费证书安装使用
categories: guide
tags: [免费SSL证书, SSL证书]
date: 2016-06-13 23:32:19
---

Let's Encrypt SSL 免费证书出来一段时间了，不过在试用了好几个第三方工具，都遇到不同的问题都没成功，后干脆换回官方的工具，这里就以官方的工具为例写个笔记。

官方证书工具下载：（如果还没装git就先安装） 
`git clone https://github.com/letsencrypt/letsencrypt.git`

官方工具有点无语就是需要占用443/80端口，也就是要把网站暂停一下，把 Nginx 或 Apache 临时停掉
`service nginx stop`
或
`service httpd stop`

进入**letsencrypt**目录，运行：

`./letsencrypt-auto certonly --standalone -d xxx.com -d www.xxx.com -m xxx@email.com --agree-tos`

Note:上面 xxx.com 和 xxx@email.com 请修改成自己的。邮箱不验证，不需要填你Whois的邮箱，这是用来丢失证书之后重置的。

稍等片刻，程序自动返回以下的成功信息：

>Requesting root privileges to run letsencrypt...

>IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at
   /etc/letsencrypt/live/xxx.com/fullchain.pem. Your cert will
   expire on 2016-07-14. To obtain a new version of the certificate in
   the future, simply run Let's Encrypt again.
 - If you lose your account credentials, you can recover through
   e-mails sent to xxxx@email.com.
 - Your account credentials have been saved in your Let's Encrypt
   configuration directory at /etc/letsencrypt. You should make a
   secure backup of this folder now. This configuration directory will
   also contain certificates and private keys obtained by Let's
   Encrypt so making regular backups of this folder is ideal.
 - If you like Let's Encrypt, please consider supporting our work by:

   >Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le


证书是放在 **/etc/letsencrypt/live/xxx.com** 目录，其中 fullchain.pem 是拼好的完整证书链证书，privkey.pem 是私钥，将它们在需要的配置文件引用即可。

>/etc/letsencrypt/live/xxx.com/fullchain.pem
/etc/letsencrypt/live/xxx.com/privkey.pem

当然最后记得重启 Nginx 或 Apache 就大功告成了。

Note：Let's Encrypt SSL 免费证书是一种短期证书，只有90天期限，到期前记得重新运行一次命令即可续期90天了。

`./letsencrypt-auto renew`

当然，可以加进cron定时任务里，先在/root根目录写个脚本，比如命名为 `ressl.sh` 内容如下：

```
#!/bin/bash
service nginx stop
cd /xxxx/letsencrypt
./letsencrypt-auto renew
service nginx start
```

然后使用`rontab -e`命令，加入以下内容，这样就可以定期每60天更新一次

`0 0 1 */2 * /root/ressl.sh > /dev/null 2>&1`

另：也可以是 `crontab -e` 
`0 0 1 */2 * ./letsencrypt-auto renew >> /dev/null 2>&1`

Note: 上面xxxx换成你所在的目录和域名邮箱等，例如你是在root目录下载的，就是 /root 目录了