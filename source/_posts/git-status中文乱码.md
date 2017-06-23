---
title: git status中文乱码
date: 2017-06-22 11:15:20
tags: git
categories: centos
permalink: 67f6feda6b2616888986268f97d926b9
---
有时使用命令`git status`时候会乱码。这只是把中文转换成了Unicode编码了。

![git status乱码](https://hysgsta.b0.upaiyun.com/img/2017/6/23/1.png!img)

解决也很简单，只需要一条命令。
```
git config --global core.quotepath false
```
这样中文就不会乱码了。

![git status乱码](https://hysgsta.b0.upaiyun.com/img/2017/6/23/2.png!img)
