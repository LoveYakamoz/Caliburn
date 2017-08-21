# pip-pop学习笔记

作者：[Kenneth Reitz](https://www.kennethreitz.org/)

![](../image/kennethreitz.jpg)

目前为止， pip-pop提交了41个commit, 看来学习会稍微简单一些。

该库包含两个小工具：pip-diff 和 pip-grep



## 简介
因为平时需要处理很多requirements.txt文件，令人烦恼。所以K神就自己搞了这个小工具
文件目录

=======bin

&emsp;　|___ pip-diff.py  : 比较给定的两个requirements文件的不同，列出 stale or fresh packages.

&emsp;　|___ pip-grep.py  : 在给定的一个requirements文件中，搜索指定的package

=======tests

&emsp;　|___ test-requirements.txt   用于测试的requirements文件

&emsp;　|___ test-requirements2.txt  用于测试的requirements文件

.gitignore :github过滤的配置文件

.travis.yml：持续集成travis的配置文件

LICENSE

README.rst

requirements.txt

setup.py ：安装方法

tox.ini ：openstack的测试工具配置文件



各文件意义

## 开发历程

讲解：主要版本变化

## 代码剖析

### pip-diff

### pip-grep



## 心得体会
1. super
2. raise valueerror
3. format
4. docopt
5. kwargs使用
