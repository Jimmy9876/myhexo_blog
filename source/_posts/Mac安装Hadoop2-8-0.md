---
title: Mac安装Hadoop2.8.0
copyright: true
date: 2017-05-25 20:38:50
tags: Hadoop
---

>前几天试了一下Hadoop，搜了大量网络资料，现在发现有的网络资料太旧了，今天重新写了个，比较简单。

#安装及配置Hadoop
##1.首先安装一下Hadoop

```
brew install Hadoop
```

##2.配置Hadoop目录下的文件
###1.core-site.xml文件

```
<configuration> <property> <name>fs.defaultFS</name> <value>hdfs://localhost:9000</value> </property> </configuration>
```

###2.hdfs-site.xml

```
<configuration> <property> <name>dfs.replication</name> <value>1</value> </property> </configuration>
```

###3.mapred-site.xml

```
<configuration> <property> <name>mapreduce.framework.name</name> <value>yarn</value> </property> </configuration>
```

mapred-site.xml文件不存在，需要自己创建（可以复制一下mapred-site.xml.template文件再进行修改）

###4.yarn-site.xml

```
<configuration>
<property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
</property>
</configuration>
```

#2.运行Hadoop
##1.进入Hadoop的目录，以mac系统为例目录为

```
/usr/local/Cellar/hadoop/2.8.0/libexec
```
然后格式化文件系统:

```
$ bin/hdfs namenode -format
```

##2.启动所有进程

```
sbin/start-all.sh
```
期间输入无数次密码，在此可以设置一下ssh免密码登录。

##3.访问localhost:50070和localhost:8088测试是否正常。
