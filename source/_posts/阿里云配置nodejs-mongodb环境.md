---
title: 阿里云配置nodejs+mongodb环境
date: 2017-05-25 18:00:37
tags: node.js
copyright: true
---

阿里云系统：ubuntu14.04

首先，在阿里云上安装nodejs，我一开始直接在线安装，发现真的是奇慢无比，于是在这里改用源码安装。。。

##1.首先，我们去nodejs官网，下载指定版本的压缩包
下载完成后，


```
scp -r 你的压缩包名字 root@你的公网ip
```

然后ssh登录你的阿里云，
解压文件并安装

```
  tar xvf 压缩包文件名 
  cd 文件名 
  ./configure 
 make 
 make install 
 cp /usr/local/bin/node /usr/sbin/ 

查看当前安装的Node的版本 
node -v 
npm -v

v.....
```
这样，就安装完了，在make编译的时候要等大概20分钟，喝杯茶先（- -）

##2.我们来下载mongodb

不得不吐槽一下，直接下也是奇慢无比。。。。速度只有?b/s你敢信？等到猴年马月，于是我决定替换一下镜像源= =

操作过程:

###1、添加 MongoDB 公共GPG钥匙。 

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
```

###2、创建列表文件(并替换国内镜像源)

```
echo "deb http://mirrors.aliyun.com/mongodb/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

###3、重新加载本地包数据库

```
sudo apt-get update
```

###4、安装MongoDB

```
sudo apt-get install -y mongodb-org
```
###5、启动MongoDB 
```
sudo service mongod start
```
###6、打开MongoDB 
```
sudo mongo 
```
注意，这里运行mongod可能会报错`/data/db not found`
要在/目录下创建相应文件夹

##3.如果你想卸载mongodb
```
1.sudo apt-get remove mongodb

2.sudo apt-get remove --auto-remove mongodb

3.sudo apt-get purge --auto-remove mongodb
```