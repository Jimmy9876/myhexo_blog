---
title: 阿里云ECS部署：nginx+MySQL+Laravel+PHP7+Redis+Node.js
date: 2017-05-25 17:59:11
tags: 阿里云ECS
copyright: true
top: true
thumbnail: http://img.sccnn.com/bimg/338/39305.jpg
---

版本：ubuntu 14.04（64位）

# 1.安装
Nginx（version：1.9）

## 1、首先添加nginx_signing.key


```
wget http://nginx.org/keys/nginx_signing.key

sudo apt-key add nginx_signing.key
```

## 2、添加Nginx官方提供的源


```
echo "deb http://nginx.org/packages/mainline/ubuntu/ trusty nginx">> /etc/apt/sources.list

echo "deb-src http://nginx.org/packages/mainline/ubuntu/ trusty nginx">> /etc/apt/sources.list
```

## 3、更新源并安装Nginx

```
sudo apt-get update

sudo apt-get install nginx
```

## 4、Nginx配置

打开配置文件。

```
vim /etc/nginx/nginx.conf
```

修改user：

```
user  www-data;
```

增加server：

```
server {

    listen 80 default_server;

    listen [::]:80 default_server ipv6only=on;

    root /var/www/laravel/public;

    index index.php index.html index.htm;

    server_name server_domain_or_IP;

    location / {

        try_files $uri $uri/ /index.php?$query_string;

    }

    location ~ \.php$ {

        try_files $uri /index.php =404;

        fastcgi_split_path_info ^(.+\.php)(/.+)$;

        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;

        fastcgi_index index.php;

        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

        include fastcgi_params;

    }

}
```

注意：root中的laravel应为你的项目名称，server_name应为你的服务器公网IP。

配置完之后重启Nginx，使上面的配置项生效。

```
sudo service nginx restart
```

# 2.安装PHP（version：7.0x）

## 1、添加PPA，添加过程中需要按一次回车（Enter）键

```
sudo apt-get install python-software-properties software-properties-common

sudo add-apt-repository ppa:ondrej/php

sudo apt-get update
```

## 2、安装PHP7以及所需的一些扩展

```
sudo apt-get install php7.0-fpm php7.0-mysql php7.0-common php7.0-curl php7.0-cli php7.0-mcrypt php7.0-mbstring php7.0-dom php7.0-gd
```

## 3、配置PHP7

打开php.ini配置文件:

```
sudo vim /etc/php/7.0/fpm/php.ini
```

找到cgi.fix_pathinfo选项，去掉注释;，然后将值设置为0  **（这个操作是为了避免PHP7的一个漏洞，PS：vim使用“/”进入查找模式）**

```
cgi.fix_pathinfo=0
```

启用php7.0-mcrypt

```
sudo phpenmod mcrypt
```

重启php7.0-fpm

```
sudo service php7.0-fpm restart
```

# 3.安装Mysql（version：5.6）

```
sudo apt-get install mysql-server-5.6 mysql-client-5.6
```

途中会提示设置MySQL的密码，安装好后：

```
mysql -uroot -p
```

然后输入刚刚设置的密码，能成功进入即成功安装。

# 4.安装Laravel（version：latest）

## 1、安装composer，分别执行以下语句

```
sudo apt-get install curl

cd ~

curl -sS https://getcomposer.org/installer| php

sudo mv composer.phar /usr/local/bin/composer
```

## 2、安装压缩、解压缩程序

```
sudo apt-get install zip unzip
```

## 3、安装git

```
sudo apt-get install git
```

然后在Coding上创建一个私有项目laravel，里面包含所有该Laravel项目所需代码。

## 4、使用git将代码clone到服务器上

```
cd /var

mkdir www

cd www

git clone your-project-git-link
```

注意：git clone 的地址应是你自己Coding仓库中的项目SSL链接地址

## 5、修改laravel项目的访问权限

```
sudo chown -R :www-data /var/www/laravel

sudo chmod -R 775 /var/www/laravel/storage
```

## 6、导入laravel 的vendor目录

```
cd /var/www/laravel

composer install
```

注意：5，6两部操作中的“laravel” 应该是你自己项目的的名称。

# 5.安装Redis（version：3.0.7）

最新版地址：http://redis.io/download

```
cd ~

wget http://download.redis.io/releases/redis-3.0.7.tar.gz

tar xzf redis-3.0.7.tar.gz
```

配置并启动Redis

```
cd redis-3.0.7

vi redis.conf
```

搜索bind，将# bind 127.0.0.1的注释去掉后保存（这样做后只有本地服务可以访问Redis，不然就有安全隐患）

```
make

src/redis-server
```

看到redis的运行提示即完成。

# 6.安装nodeJS

添加下面链接中的源，然后安装

```
https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions
```


# 番外：安装ZSH shell

```
github：sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

sudo apt-get install zsh

chsh -s $(which zsh)

sh -c"$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### 如果已经下了5.0想升级成7.0的朋友可执行以下代码

    sudo apt-get install python-software-properties software-properties-common 
    sudo LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php 
    sudo apt-get update

#### 把之前的PHP5.0remove掉

    sudo apt-get remove php5-common -y
    sudo apt-get purge php5-common -y

#### 安装现在的7.0

    sudo apt-get install php7.0 php7.0-fpm php7.0-mysql -y
    sudo apt-get --purge autoremove -y
