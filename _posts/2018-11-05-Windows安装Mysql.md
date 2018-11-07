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


## 前言

> 之前在Windows下开发PHP都是用的WAMP集成环境,业务需要单独安装配置MySQL,记录以备忘.

> [MySQL5.7下载页](https://dev.mysql.com/downloads/mysql/5.7.html#downloads "MySQL5.7下载页")  , [MySQL57.zip](https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.24-winx64.zip "MySQL57下载")  ,[MySQL5.7 MSI安装包下载页](https://dev.mysql.com/downloads/windows/installer/5.7.html "MySQL5.7 MSI安装包下载页面")  , [MySQL5.7MSI 文件](https://cdn.mysql.com//Downloads/MySQLInstaller/mysql-installer-community-5.7.24.0.msi "MySQL5.7 MSI 文件")

## 1. 控制命令
#### 1.1 系统命令
> net start mysql57  --开启
> net stop mysql57   --关闭

#### 1.2 直接定位到bin目录
>msi安装默认目录: C:\Program Files\MySQL\MySQL Server 5.7\bin
> mysqladmin shutdown --开启
> mysqladmin start	  --关闭

## 2. 解压包配置安装
> 根据系统下载对应的32位或者64位压缩包

## 3. MSI安装
> 下载mysql-installer-community,32位安装包即可,MSI是32位的,但是会同时安装32位和64位

#### 3.1 同意协议
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_1.png)
> 勾选同意协议,点击NEXT按钮

#### 3.2 选择设置类型
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_2.png)
> MySQL会默认选择“Developer Default”类型，可根据自己的需求选择合适的类型，这里选择“Server only”后点击“next”。

* Developer Default：安装MySQL服务器以及开发MySQL应用所需的工具。工具包括开发和管理服务器的GUI工作台、访问操作数据的Excel插件、与Visual Studio集成开发的插件、通过NET/Java/C/C++/OBDC等访问数据的连接器、例子和教程、开发文档。
* Server only：仅安装MySQL服务器，适用于部署MySQL服务器。
* Client only：仅安装客户端，适用于基于已存在的MySQL服务器进行MySQL应用开发的情况。
* Full：安装MySQL所有可用组件。
* Custom：自定义需要安装的组件。

#### 3.3 检查环境要求
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_3.png)
> 这一步,安装程序检查环境要求,列出欠缺的依赖环境,选择列表中的项,点击Execute按钮进行安装

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_4.png)
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_5.png)
> 所有依赖安装完成,点击Next按钮进行下一步

#### 3.4 安装
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_6.png)
> 点击Execute按钮进行安装

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_7.png)

> 点击Next按钮进入下一步配置

#### 3.5 配置
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_8.png)
> 点击Next按钮进入下一步配置

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_9.png)
> 组复制插件选择,这里默认选择第一个就行

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_10.png)
> 配置类型和网络
点击Content Type的下拉框，显示有三种类型：

* Development Computer：开发机器，MySQL会占用最少量的内存。
* Server Computer：服务器机器，几个服务器应用会运行在机器上，适用于作为网站或应用的数据库服务器，会占用中等内存。
* Dedicated Computer：专用机器，机器专门用来运行MySQL数据库服务器，会占用机器的所有可用内存。

这里根据需要选择"Development Computer".

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_11.png)
> 常用的是TCP/IP连接，勾选该选项框，默认端口号是3306，可在输入框中更改。若数据库只在本机使用，可勾选“Open Firewall port for network access”来打开防火墙，若需要远程调用则不要勾选。
下面的“Named Pipe”和“Shared Memory”是进程间通信机制，一般不勾选。
“Show Advanced Options”用于在后续步骤配置高级选项，为尽可能多的了解MySQL的可配置项，这里勾选该选项框。点击“next”进入下一步。

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_12.png)
> 将MySQL服务配置成Windows服务后，MySQL服务会自动随着Windows操作系统的启动而启动，随着操作系统的停止而停止，这也是MySQL官方文档建议的配置

> 接下来是账户设置,我们这里只需要设置Root用户密码即可,后面需要再添加其他账号,输入两次要设置的Root账号的密码之后,点击next

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_13.png)
> 插件和扩展这里不需要用到,直接点击Next

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_14.png)
> 日志选项配置 在这里可配置各种日志文件的存储路径，它默认存储在MySQL安装目录的data目录下面，若非必须不建议改动。Slow Query Log(慢查询日志)后面有一个Seconds配置项，默认值为10，表示一个SQL查询在经过10s后还没有查询出结果就会将此次查询记录到Slow Query Log中，方便DBA快速找到低效的操作。Bin Log可用于主从数据同步。最下面的Server Id用于Master-Slave配置。这些都将在后续课程中讲到，这里保持默认配置即可。点击“next”。

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_15.png)
> 高级选项,这里默认配置即可,点击Next

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_16.png)
> 应用上述配置,点击Execute按钮

![](/img/blog/20181105_windows_mysql/windows_mysql_msi_17.png)
> 配置完成点击Finish

#### 3.6 收尾
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_18.png)
![](/img/blog/20181105_windows_mysql/windows_mysql_msi_19.png)
> 最后点击Finish后安装成功,至此,mysql会随着系统启动而启动,我们也可以通过命令控制

* net start mysql57  --开启
* net stop mysql57   --关闭



