---
title: centos安装docker
date: 2017-06-21 11:14:51
tags: docker
categories: centos
permalink: 5e9fb620725e9c4b79e7cfb04aa397ab
---
### 系统环境

 + centos 7.3

### docker简介
Docker是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。
<!--more-->
### 安装docker
centos 7.x版本才支持docker，低于centos 7的版本不正常docker，所以要使用centos 7版本。
另外centos官方yum仓库的docker太老，推荐使用docker官方yum仓库。

配置yum仓库。
```
[dockerrepo]
name=Docker Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/docker/yum/repo/centos7
enabled=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/docker/yum/gpg
```
缓存索引
```
yum mackecache
```
最后安装docker
```
yum install docker-engine
```
类似这样就安装docker成功了

![安装docker](https://hysgsta.b0.upaiyun.com/img/2017/6/23/3.JPG!img)

启动docker
```
systemctl start docker
```
输入命令，查看docker版本

![docker版本](https://hysgsta.b0.upaiyun.com/img/2017/6/23/4.JPG!img)

新建一个docker组
```
groupadd docker
```
为了安全，把新用户添加进docker组
```
usermod -aG docker hy
```
因为某些原因，在国内直接调用docker官方源，下载速度很慢。不过可以使用docker加速器。

注册daocloud，可以使用daocloud加速器。
```
curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://******.m.daocloud.io
```
### 输出hello world
启动docker成功，就用docker输出hello world吧！
```
$docker run hello-world
```

![输出hello world](https://hysgsta.b0.upaiyun.com/img/2017/6/23/5.JPG!img)
