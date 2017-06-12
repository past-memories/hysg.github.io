---
title: 二进制安装mariadb
date: 2017-05-29 18:30:03
tags:
categories:
permalink: 40f6edeae4284dc5c42a15b52b5d0c95
---
### mariadb简介
>MySQL是一个关系型数据库管理系统，是最流行的关系型数据库管理系统，由于其体积小、速度快、总体拥有成本低，并且之前是完全开>源，所以大受欢迎。但由于后面MySQL卖给了SUN，随后SUN被Oracle收购，虽然也有开源免费版本，但是很多功能都需要另外购买商业版>本，导致现在MySQL使用份额逐渐减少。所以MariaDB就是因为这种原因诞生出来，成为数据库管理系统是MySQL的一个分支。
MariaDB数据库管理系统是MySQL的一个分支，主要由开源社区在维护，采用GPL授权许可。开发这个分支的原因之一是：甲骨文公司收购了MySQL后，有将MySQL闭源的潜在风险，因此社区采用分支的方式来避开这个风险。

<!--more-->

[mariadb官网](https://mariadb.org/)

### 系统环境

+ centos 6.8
+ mariadb 10.1.24

### 安装依赖
```
yum install -y libaio
```
### 安装mariadb

+ 下载安装包
可以到mariadb官方网站或者到我准备的镜像站下载安装包

```
cd /usr/local/
wget https://inmir.b0.upaiyun.com/mariadb/generic/10/mariadb-10.1.24-linux-x86_64.tar.gz
// 解压安装包
tar -xzf mariadb-10.1.24-linux-x86_64.tar.gz
// 重命名文件目录
mv mariadb-10.1.24-linux-x86_64  mysql
```

+ 新建组和用户

```
groupadd mysql
useradd mysql -g mysql -s /sbin/nologin -M
```

+ 添加系统环境变量

```
echo "PATH=$PATH:/usr/local/mysql/bin" > /etc/profile.d/mysql.sh
// 重读配置文件
source /etc/profile.d/mysql.sh
```

+ 准备文件

新建数据库文件目录
```
mkdir -p /data/mysql
```
新建日志文件目录
```
mkdir /var/log/mysql
```
新建配置文件文件目录
```
mkdir /etc/mysql
```
复制启动脚本
```
cp /usr/local/mysql/support-files/mysql.server /etc/rc.d/init.d/mysqld
chmod +x /etc/rc.d/init.d/mysqld
```
复制配置文件
```
cp /usr/local/mysql/support-file/my-small.cnf /etc/mysql/my.cnf
```
在配置文件中添加下面的内容
```
[client]
default-character-set=utf8mb4
[mysqld]
basedir         = /usr/local/mysql
datadir         = /data/mysql/data
user = mysql
character-set-server=utf8mb4
default-storage-engine = innodb
bind-address = 127.0.0.1
// 禁用域名解析
skip-name-resolve = on
```

+ 初始化数据库

初始化数据库，注意有没有报错信息
```
./mysql_install_db --user=mysql --datadir=/data/mysql/ --basedir=/usr/local/mysql/
```
初始化数据库成功，就像下面这样

![初始化数据库](https://hysgsta.b0.upaiyun.com/img/2017/6/12/1.JPG!img)

+ 如果数据库初始化成功，就可以启动数据库了

启动数据库
```
service mysqld start
```
数据库启动成功，就开始监听3306端口

![初始化数据库](https://hysgsta.b0.upaiyun.com/img/2017/6/12/2.JPG!img)

+ 数据库安全设置

使用mysql安全设置可以重置root用户密码，禁止root用户远程登录，删除匿名用户和test数据库

![初始化数据库](https://hysgsta.b0.upaiyun.com/img/2017/6/12/3.JPG!img)

 这样mariadb就安装成功了。
