---
title: centos快速安装zabbix
date: 2017-07-23 16:20:08
tags:
categories:
permalink:
---
zabbix源配置
```
[zabbix]
name = zabbix
enable = 1
baseurl = https://mirror.tuna.tsinghua.edu.cn/zabbix/zabbix/3.0/rhel/7/x86_64/
gpgcheck = 1
gpgkey=https://mirror.tuna.tsinghua.edu.cn/zabbix/RPM-GPG-KEY-ZABBIX
```
epel源安装
```
yum install ifping iksemel iksemel-devel
```
server机安装
```
yum install zabbix zabbix-agent zabbix-get \
            zabbix-server-mysql zabbix-web \
            zabbix-web-mysql zabbix-sender
```
node机安装
```
yum install zabbix-agent
```
