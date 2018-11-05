---
layout:     post
title:      Windows安装Mysql
subtitle:
date:       2018-11-05
author:     simafeiyu
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - MySQL
    - PHP开发
---


# 前言

> 之前在Windows下开发PHP都是用的WAMP集成环境,业务需要单独安装配置MySQL,记录以备忘.

> [MySQL5.7下载页](https://dev.mysql.com/downloads/mysql/5.7.html#downloads "MySQL5.7下载页")  , [MySQL57.zip](https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.24-winx64.zip "MySQL57下载")  ,[MySQL5.7 MSI安装包下载页](https://dev.mysql.com/downloads/windows/installer/5.7.html "MySQL5.7 MSI安装包下载页面")  , [MySQL5.7MSI 文件](https://cdn.mysql.com//Downloads/MySQLInstaller/mysql-installer-community-5.7.24.0.msi "MySQL5.7 MSI 文件")

## 控制命令
### 系统命令
> net start mysql  --开启
> net stop mysql   --关闭

### 直接定位到bin目录(msi安装默认目录: C:\Program Files\MySQL\MySQL Server 5.7\bin)
> mysqladmin shutdown --开启
> mysqladmin start	  --关闭

## 解压包配置安装
> 根据系统下载对应的32位或者64位压缩包

## MSI安装--Yaokan2018
> 下载mysql-installer-community,32位安装包即可,MSI是32位的,但是会同时安装32位和64位

### 1. 同意协议
[![1](1 "同意协议")](/img/blog/20181105_windows_mysql/windows_mysql_msi_1.png "同意协议")
> 勾选同意协议,点击NEXT按钮

### 2. 选择设置类型
[![2]( )](/img/blog/\20181105_windows_mysql/windows_mysql_msi_2.png)
> MySQL会默认选择“Developer Default”类型，可根据自己的需求选择合适的类型，这里选择“Server only”后点击“next”。

* Developer Default：安装MySQL服务器以及开发MySQL应用所需的工具。工具包括开发和管理服务器的GUI工作台、访问操作数据的Excel插件、与Visual Studio集成开发的插件、通过NET/Java/C/C++/OBDC等访问数据的连接器、例子和教程、开发文档。
* Server only：仅安装MySQL服务器，适用于部署MySQL服务器。
* Client only：仅安装客户端，适用于基于已存在的MySQL服务器进行MySQL应用开发的情况。
* Full：安装MySQL所有可用组件。
* Custom：自定义需要安装的组件。

### 3. 检查环境要求
[![3]( )](/img/blog/\20181105_windows_mysql/windows_mysql_msi_3.png)
> 这一步,安装程序检查环境要求,列出欠缺的依赖环境,选择列表中的项,点击Execute按钮进行安装

[![4]( )](/img/blog/\20181105_windows_mysql/windows_mysql_msi_4.png)


### 4.
