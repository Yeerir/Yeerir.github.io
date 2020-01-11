---
layout: post
title:  "离线（单机）安装python-docx(Windows系统)"
date:   2020-01-11 16:16:16
categories: python
tags: python
excerpt: 最近安装python-docx遇到问题，记录下来吧。
mathjax: true
---

# 离线（单机）安装python-docx(Windows系统)



##特别说明

如果能联网，就直接
```
pip install python-docx 
```
就行了，不用往下看了。

下面是想在一台不能上网的电脑上安装python-docx的步骤。当然你还需要一台能上网的电脑/手机，能够下载需要的安装包/库。



## 详细步骤

###1. 查看python版本及可安装扩展库的版本信息


```
#查看python版本
python -V
```
```
#查看可安装扩展库的版本信息
import pip
print(pip._internal.pep425tags.get_supported())
```
我的电脑是win64位，python装的是win32位，我用的是上面命令。

如果报错，可以试下print(pip.pep425tags.get_supported())

###2. 下载安装包安装


到python-docx官网上，找到符合上述条件的python-docx版本下载，我下载的是这个：
https://files.pythonhosted.org/packages/e4/83/c66a1934ed5ed8ab1dbb9931f1779079f8bca0f6bbc5793c06c4b5e7d671/python-docx-0.8.9.tar.gz

解压python-docx-0.8.9.tar.gz，然后执行
```
cd python-docx-0.8.9
python setup.py install
```
如果能安装成功，恭喜你！以及不用往下看了。

###3. lxml包报错调试


我在装的过程中，出现了错误，显示缺少 lxml 包，提示安装lxml>= x.x.x。

找到官方网站 [https://pypi.org/project/lxml/#files](https://pypi.org/project/lxml/#files)
下载符合上述条件的 lxml版本，我这里选的(‘cp35’,’cp35m’,’win32’)

但是实际安装的时候出现了错误：

**“lxml-4.4.2-cp35-cp35m-win32.whl is not a support wheel on this platform”**

上网查这个错误的原因可能是pip 需要更新或者lxml版本不对。

####3.1更新pip。
到pip官网上下载最新版的pip，这里我两个(.whl文件和tar.gz文件)都下载了。

果然，用pip install pip-19.3.1-py2.py3-none-any.whl 时，报错。是无法打开/复制XXXXX文件到XXXXX文件夹。这时候用pip-19.3.1.tar.gz安装，解压，然后
```
cd pip-19.3.1
python setup.py install
```
安装成功。这个会自动卸载uninstall旧版本的pip。

更新了pip后，再装 lxml-4.4.2-cp35-cp35m-win32.whl，还是失败，错误是一样的。
“lxml-4.4.2-cp35-cp35m-win32.whl is not a support wheel on this platform”

####3.2找其他lxml版本尝试
官方网址除了(‘cp35’,’cp35m’,’win32’)没有找到其他版本符合要求的。去国内镜像网址查看，以下两个网址常用：
```
http://pypi.douban.com/simple/
https://pypi.tuna.tsinghua.edu.cn/simple
```
Ctrl+F搜索lxml，点击lxml，查看不同版本，这里cp35的版本我都安装不上，最后找的cp32的版本。
```
pip install lxml-3.4.1-cp32-none-win32.whl
```
lxml安装成功。

这时候可以安装python-docx-0.8.9了：
```
cd python-docx-0.8.9
python setup.py install
```
终于，python-docx 安装成功！！！



## 小记

我能说我费劲装上python-docx以后发现，它只能处理docx格式的word文档，不能处理doc格式的，而doc格式转为docx格式可能会有些不兼容的内容，😭前方的路还很长。
