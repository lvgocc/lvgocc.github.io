
---
title: Intellij IDEA配置tomcat 远程调试 debug模式
date: 2018-07-20 21:44:40
updated: 2018-07-20 21:44:40
comments: true
tags: 调试
//excerpt: 
categories: 随笔
---


### 一.配置服务器

在catalina.sh 中添加 address 调试端口 9999  **catalina.sh的位置在tocmat下的bin目录**

> 以下方法任选其一

第一种方法

<!--more-->

```
JAVA_OPTS="-agentlib:jdwp=transport=dt_socket,address=9999,suspend=n,server=y"
```
第二种方法
```
CATALINA_OPTS="-server -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=9999" 
```

### 二.配置IDE

![这里写图片描述](https://img-blog.csdn.net/20180720213720867?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQ0MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
点击编辑启动配置

![这里写图片描述](https://img-blog.csdn.net/2018072021380811?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQ0MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
点击+号,选择remote
![这里写图片描述](https://img-blog.csdn.net/20180720213902702?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQ0MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
将host改成服务器的ip地址,port改成刚配置好的端口.

----
以debug模式运行

当控制台出现“Connected to the target VM, address: ‘xx.xx.xx.xx:9999’, transport: ‘socket’”的字样即可,记得加入要调试的断点.

----
#end