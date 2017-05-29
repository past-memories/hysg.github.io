---
title: pyenv部署python多版本
date: 2017-05-23 00:36:25
tags: python3
categories: python
permalink: 2d0e324e1303a9a0d6bdaf317c31f0c3.html
---
## pyenv简介
pyenv让你可以轻松地在不同版本的Python之间切换。pyenv使用起来很简单，并且遵循了UNIX传统的单一用途工具。
<!--more-->
### 系统版本

+ centos 7.2

### 解决依赖
```
yum install git gcc make patch zlib-devel -y
yum install gdbm-devel openssl-devel sqlite-devel -y
yum install bzip2-devel readline-devel -y
```
#### 新建用户
pyenv使用普通用户就能安装，所以就直接使用普通用户身份安装并使用
```
// 新建用户
useradd hy
// 切换到普通用户
su hy
// 回到当前用户的家目录cd
```
#### 安装pyenv
```
curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
```
#### 设置环境变量
修改配置文件
```
vim .bash_profile
PATH=~/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
// 重读配置文件
source .bash_profile
```
#### 部署多python版本
可以新建一个目录做为一个python版本
```
mkdir python35
cd python35
pyenv install -v 3.5.3
pyenv local 3.5.3
pip install --upgrade pip
```
#### 常见问题
如果感觉从python官网下载的python包太慢，可以提前把下载python源码包
```
cd ~/.pyenv
mkdir cache
// 把下载好的python包放在cache目录里面
cd cache
// 我在又拍云存的源码包
wget https://inmir.b0.upaiyun.com/python/Python-3.5.3.tar.xz
```
