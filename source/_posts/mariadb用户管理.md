---
title: mariadb用户管理
date: 2017-06-16 14:04:09
tags: mariadb基础
categories: mariadb
permalink: cb4778f37a1703d3f2eff90be200c6c2
---
### 数据库版本
查看数据库版本
```
mariadb> SELECT VERSION();
+-----------------+
| VERSION()       |
+-----------------+
| 10.2.6-MariaDB |
+-----------------+
1 row in set
```

<!--more-->

### 新建用户
在客户端登录mariadb数据库，使用sql命令新建用户
```
mariadb>CREATE USER 'username'@'host' IDENTIFIED BY 'PASSWORD';
```
其中HOST字段可以设置为

+ IP地址，如192.168.2.2

+ 地址段，如192.168.2.%

+ 主机名，如localhost

+ 通配符，如%

### 删除用户
删除用户使用命令
```
mariadb>DROP user 'username'@'host';
```
### 用户授权
+ 给用户授权，使用命令

```
mariadb>GRANT privileges ON databasename.tablename TO 'username'@'host';
```
privileges可以指定为`INSERT，DROP，UPDATE，SELECT`等

如赋予用户增删改查的权利
```
mariadb>GRANT INSERT，DROP，UPDATE，SELECT ON test.* TO 'username'@'host';
```

+ 查看已授权用户权限

```
mariadb>SHOW GRANTS FOR 'username'@'host';
```
如查看root用户在127.0.0.1主机上权限
```
SHOW GRANTS FOR 'root'@'127.0.0.1';
+----------------------------------------------------------------------------------------------------------------------------------------+
| Grants for root@127.0.0.1                                                                                                              |
+----------------------------------------------------------------------------------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'root'@'127.0.0.1' IDENTIFIED BY PASSWORD '*6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9' WITH GRANT OPTION |
+----------------------------------------------------------------------------------------------------------------------------------------+
1 row in set
```
### 给其他用户授权
如果用户A想给其他用户授权，给用户A授权的语句就不太一样
```
mariadb>GRANT privilege ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
```
这样用户A就能给其他用户授权了
### 移除用户权限
移除用户权限使用命令，
```
mariadb>REVOKE privilege ON databasename.tablename FROM 'username'@'host';
```
### 重置用户密码
+ 未登录用户，重置密码，使用命令

```
mariadb>SET PASSWORD FOR 'username'@'host' = PASSWORD('newpassword');
```

+ 已经登录用户，重置密码，使用命令

```
mariadb>SET PASSWORD = PASSWORD("newpassword");
```
### 刷新权限
最后，要刷新数据库用户权限
```
mariadb>FLUSH PRIVILEGES;
```
### 数据库用户权限表
|权限|描述|
|---|---|
|INSERT|增|
|DROP|删|
|UPDATE|改|
|SELECT|查|
|INDEX|索引|
|VIEW|视图|
|ROUTINE|储存过程|
