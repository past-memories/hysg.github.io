---
title: centos配置ssh公钥登录
date: 2017-06-15 14:04:11
tags: centos系统配置
categories: centos
permalink: 9b75e2b8516968af12514590bd5928b2
---
远程登录centos服务器，如果使用用户名和密码登录，是不安全的。纯密码容易被爆破。推荐使用ssh公钥登录服务器。

<!--more-->

### 公共配置
修改sshd配置文件
```
// 切换成root用户
su root
vim /etc/ssh/sshd_config
// 修改成其他端口
Port 22
// 取消注释
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile     .ssh/authorized_keys
// 禁止root用户登录
PermitRootLogin no
// 禁止使用密码登录
PasswordAuthentication no
// 重启sshd服务
service sshd restart
```

### xshell创建密钥
Xshell终端模拟器是一个强大的安全终端模拟软件，它支持SSH1, SSH2, 以及Microsoft Windows 平台的TELNET 协议。Xshell可以在Windows界面下用来访问远端不同系统下的服务器，从而比较好的达到远程控制终端的目的。  
将使用xshell创建一对密钥对，公钥上传到服务器。

![新建密钥](https://hysgsta.b0.upaiyun.com/img/2017/6/15/1.JPG!img)

点击用户密钥生成向导

![新建密钥](https://hysgsta.b0.upaiyun.com/img/2017/6/15/2.JPG!img)

密钥类型选择RSA，密钥长度越长，生成时间就越长。

![新建密钥](https://hysgsta.b0.upaiyun.com/img/2017/6/15/3.JPG!img)

这一步会生成密钥，根据密钥长度不同，生成的时间也不一定

![新建密钥](https://hysgsta.b0.upaiyun.com/img/2017/6/15/4.JPG!img)

复制文本框里面的公钥，备用

然后登录服务器，输入命令
```
mkdir .ssh
chmod 700 .ssh
// 将上面公钥复制到这个文件
vim authorized_keys
chmod 644 authorized_keys
```

### 使用ssh-keygen创建密钥
登录服务器，使用命令创建密钥
```
ssh-keygen -t rsa -b 2048
Generating public/private rsa key pair.
Enter file in which to save the key (/home/hysg/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/hysg/.ssh/id_rsa.
Your public key has been saved in /home/hysg/.ssh/id_rsa.pub.
The key fingerprint is:
44:1d:cb:9b:6a:a7:d3:d4:b8:b4:3f:21:18:e9:d5:8d hysg@iZ2884cni4lZ
The key's randomart image is:
+--[ RSA 2048]----+
|        ....     |
|       . ...     |
|        ..o. o   |
|       .o .oE .  |
|       .S+oo     |
|        o.= o    |
|        o+.+ .   |
|       ..o+ .    |
|        .. ...   |
+-----------------+
```

+ 会让你指定密钥文件的位置和名字，默认在`~/home/.ssh/`下面;
+ 会询问你是否需要输入密码。输入密码之后，以后每次都要输入密码。根据自身的安全需要决定是否需要密码，如果不需要，直接回车;

使用tree命令，查看生成的文件
```
[hysg@iZ2884cni4lZ .ssh]$ tree
.
├── id_rsa
└── id_rsa.pub

0 directories, 2 files
```
其中id_rsa是私钥，id_rsa.pub是公钥，把私钥文件下载到本地备用

### 登录服务器
打开xshell新建连接，点击用户身份验证

![新建密钥](https://hysgsta.b0.upaiyun.com/img/2017/6/15/5.JPG!img)

方法选择公钥验证，用户密钥选择私钥

### 免帐号登录
一般情况下，本地主机登录远程主机的命令是
```
ssh user@192.168.2.1
```
当然还有一种更简便的方法来登录远程主机
```
vim ~/.ssh/config
// 添加
Host node1
   HostName 192.168.2.1
   Port 22
   User user
   IdentityFile /home/hysg/.ssh/id_rsa
// 修改权限
chmod 600 ~/.ssh/config
```
再登录远程主机，可以使用命令
```
ssh node1
```
