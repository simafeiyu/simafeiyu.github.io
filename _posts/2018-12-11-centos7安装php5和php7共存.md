---
layout:     post
title:      centos7安装php5和php7共存
subtitle:   
date:       2018-12-11
author:     simafeiyu
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - centos7
	- php
---


# 前言

> 最近项目中需要用到Swoole框架,用到了协程,所以需要swoole4.0以上版本,而swoole4.0需要php7.1以上,然而历史原因,服务器的php版本不能超过php7,所以需要多安装一个php,特此记录
> [参考](https://jonny.vip/2017/06/28/centos-7-%E5%92%8C-nginx-%E4%B8%8B%E5%AE%9E%E7%8E%B0%E5%A4%9A%E7%89%88%E6%9C%AC-php-%E7%9A%84%E5%85%B1%E5%AD%98/ "参考")



## 安装
#### 下载(7.1.19)
> wget http://hk1.php.net/distributions/php-7.1.19.tar.gz

> 也可以直接去网站上下载上次到服务器: [下载地址](http://php.net/get/php-7.1.19.tar.gz/from/a/mirror)

#### 解压
> tar zxvf php-7.1.19.tar.gz

#### 进入php目录
> cd php-7.1.19

#### 编译安装
* CFLAGS= CXXFLAGS= ./configure --prefix=/usr/local/php7 --with-config-file-path=/usr/local/php7/etc --with-fpm-user=www --with-fpm-group=www --enable-fpm --enable-opcache --disable-fileinfo --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-jpeg-dir --with-iconv-dir=/usr/local --with-freetype-dir  --with-png-dir --with-zlib --disable-rpath --with-libxml-dir=/usr --enable-xml  --enable-bcmath --enable-shmop --enable-exif --with-curl --enable-sysvsem --enable-inline-optimization  --enable-mbregex --enable-inline-optimization --enable-mbstring --with-mcrypt --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc --enable-ftp --with-gettext --enable-zip --enable-soap --disable-ipv6 --disable-debug
* make    --这里需要一些时间,耐心等候
* make install

## 配置
#### 处理php.ini
* cp php.ini-development /usr/local/php7/lib/php.ini  --在php-7.1.19目录
* vi /usr/local/php7/lib/php.ini
* 找到mysql.default_socket 和 mysqli.default_socket,
	* mysql.default_socket = /var/lib/mysql/mysql.sock
	* mysqli.default_socket = /var/lib/mysql/mysql.sock

#### 处理php-fpm.conf
* cp /usr/local/php7/etc/php-fpm.conf.default /usr/local/php7/etc/php-fpm.conf
* vi /usr/local/php7/etc/php-fpm.conf
---

	;include=/usr/local/php7/etc/php-fpm.d/*.conf
    [nginx]
    	user = nginx
    	group = nginx
    	listen = 127.0.0.1:9001
    	pm = dynamic
    	pm.max_children = 5
		
#### 配置PHP7-FPM 服务
* cp sapi/fpm/php-fpm.service /usr/lib/systemd/system/php7-fpm.service   --在php-7.1.19目录下
* vi /usr/lib/systemd/system/php7-fpm.service
* 修改两行: 
	* PIDFile=/usr/local/php7/var/run/php-fpm.pid
	* ExecStart=/usr/local/php7/sbin/php-fpm --nodaemonize --fpm-config /usr/local/php7/etc/php-fpm.conf

* 启动php7-fpm:
	* systemctl daemon-reload
	* systemctl enable php7-fpm
	* systemctl start php7-fpm

#### 添加php到path
* 复制php为php7,以区别5.6版本
	* cp /usr/local/php7/bin/php /usr/local/php7/bin/php7
	* rm /usr/local/php7/bin/php

* 添加到PATH
	* vi /etc/profile
	* export PATH= $PATH:/usr/local/php7/bin/
	* source /etc/profile # 让环境变量立即生效
* 查看
	* echo $PATH

#### 验证
* php7 --version
* netstat -tnlp 查看9001的php-fpm有没有启动
























