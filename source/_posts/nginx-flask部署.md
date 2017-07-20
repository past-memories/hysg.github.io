---
title: nginx flask部署
date: 2017-07-07 00:36:12
tags: python
categories: centos
permalink: 98844b7faa44a29f169b7c75120b8574
---
同大多数的web部署方式相同，想跑flask程序，需要nginx和gunicorn。nginx是一个小型web服务器，gunicorn是纯绿色版的Python WSGI UNIX的HTTP服务器。
<!--more-->
### 系统环境

* centos 7.3
* python 3.5.3
* nginx 1.12.0

### 部署pyenv
为了避免python版本的冲突，这里使用pyenv作为python版本的管理工具，避免和系统自带python冲突。pyenv安装参考[pyenv部署python多版本](https://hysg.github.io/2017/05/23/2d0e324e1303a9a0d6bdaf317c31f0c3.html)。

### 安装gunicorn
使用pip命令安装gunicorn
```
pip install gunicorn
```
测试一下
```
from flask import Flask,render_template

app = Flask(__name__)

@app.route('/')
def hello_world():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)
```
