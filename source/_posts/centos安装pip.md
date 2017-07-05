---
title: centos安装pip
date: 2017-05-25 18:03:08
tags: pip配置
categories: python
permalink: 2d261affc14ef8960fb0c2dd554bf7c2
---
### pip简介
pip为包管理器，跟linux上众多的包管理器的功能大致相同，就是对包进行管理，使得包的安装，更新和卸载更容易。在python2.7.9以上和3.4以上自带pip包管理器。

<!--more-->

### pip安装
首先去下载geit.pip.py文件

```
// 官方下载地在
wget https://bootstrap.pypa.io/get-pip.py
// 我提供的镜像站
wget https://inmir.b0.upaiyun.com/python/tool/get-pip.py
下载完成以后，使用python命令安装
python get-pip.py
```

### 解决警告
pip安装完以后，会有一句警告
```
DEPRECATION: The default format will switch to columns in the future. You can use --format=(legacy|columns) (or define a format=(legacy|columns) in your pip.conf under the [list] section) to disable this warning.
```
在pip的配置文件中，添加
```
vim ~/.pip/pip.conf
[list]
format=columns
// 或者
[list]
format=legacy
```
### 配置本地源
如果从官方源下载速度太慢，可以配置其他源,

+ 临时使用

```
// 清华大学源
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
// 豆瓣源
pip install -i https://pypi.douban.com/simple some-package
```

+ 设置默认

```
[global]
// 清华大学源
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
// 豆瓣源
index-url = https://pypi.douban.com/simple
```
### requirements.txt依赖
查看别人的Python项目时，经常会看到一个requirements.txt文件，里面记录了当前程序的所有依赖包及其精确版本号。

requirements.txt可以通过pip命令自动生成和安装

生成requirements.txt文件
```
pip freeze > requirements.txt
```
安装requirements.txt依赖
```
pip install -r requirements.txt
```
