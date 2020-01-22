
---
title: nginx 怎么通过域名访问8080端口(指定端口)
date: 2018-07-20 21:28:21
updated: 2018-07-20 21:28:21
comments: true
tags: Nginx
//excerpt: 
categories: [随笔,教程]
---
进入到nginx目录下,打开nginx.conf

<!--more-->

```
http {
    server {
		    listen 80;
            server_name example.com;
 
            location /test1 {
                    proxy_pass http://example.com:8080/test1;
            }
 
            location /test2 {
                    proxy_pass http://example.com:8081/test2;
            }
 
            location / {
                    proxy_pass http://example.com;
            }
    }
}
```
重新加载一下配置文件
```
./nginx -s reload
```
最主要的地方就是配置好location的地址
```
当我们输入域名之后加上/test1的时候,就会被nginx映射到我们域名:8080/test1路径上去做请求.
```