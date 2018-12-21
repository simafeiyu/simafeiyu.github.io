---
layout:     post
title:      Nginx配置proxy_pass
subtitle:   
date:       2018-12-21
author:     simafeiyu
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Nginx
    
---


# 前言
> 　最近业务有一个需求，访问a.com的时候，需要实际访问b.com,并且域名不能发生变化。达成这个需求有两种做法：
	* 第一种就是301跳转，使用rewrite来跳转域名，不过这样域名就会发生变化，与需求不符。
　　* 第二种就是用proxy_pass跳转，只要指定跳转目的域名，就可以在访问的时候自动跳转访问目的域名，而且域名也不会发生变化。所以这里需要使用第二种方法。



## 示例
> 访问oem.simafeiyu.xyz的时候,实际访问demo.abcd.com

---

server {
	listen 80; 
	server_name oem.simafeiyu.xyz;
	
    # 正常代理，不修改后端url的
    location / {
        proxy_pass http://demo.abcd.com/;
	    proxy_redirect          off;
		proxy_set_header        X-Real-IP       $remote_addr;
		proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_cookie_domain .abcd.com .simafeiyu.xyz;
		proxy_cookie_path  / /;
    }
	
}




















