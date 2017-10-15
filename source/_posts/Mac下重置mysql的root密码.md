---
title: Mac下重置mysql的root密码
date: 2017-05-25 17:57:05
tags: mysql
copyright: true
---

>我的mysql版本 MYSQL V5.7.9，旧版本请使用：


```
UPDATE mysql.user SET Password=PASSWORD('新密码') WHERE User='root';
```

###Mac OS X - 重置 MySQL Root密码
密码太多记不住？？你是否忘记了Mac OS 的MySQL的root密码? 通过以下4步就可重新设置新密码：
#####1.  停止 mysql server. 
 通常是在 '系统偏好设置' > MySQL > 'Stop MySQL Server'
#####2.  打开终端，输入：
```
 sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables
```
#####3.  打开另一个新终端，输入:

```
   sudo /usr/local/mysql/bin/mysql -u root

     UPDATE mysql.user SET authentication_string=PASSWORD('你的新密码') WHERE User='root';

     FLUSH PRIVILEGES;

     exit
```

#####4.  重启MySQL.
好了，这样就完成了