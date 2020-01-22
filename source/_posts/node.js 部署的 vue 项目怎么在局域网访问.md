
---
title: node.js 部署的 vue 项目怎么在局域网访问
date: 2018-07-20 21:18:06
updated: 2018-07-20 21:18:06
comments: true
tags: [Vue,Node.js]
//excerpt: 
categories: [随笔,教程]
---

#### 1.查看本机局域网ip
```
// windows系统
在cmd页面输入ipconfig命令即可查看
// linux系统
在终端输入ifconfig命令可查看
```

<!--more-->

#### 2.修改vue配置文件
```
// 进入到项目的config文件夹下,打开index.js 把host改成以上你查看到的本地ip地址

// Various Dev Server settings
host: '192.168.31.239', // can be overwritten by process.env.HOST
port: 8082
....
.
.
```
![这里写图片描述](https://img-blog.csdn.net/20180720212021564?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQ0MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

#### 3.在其他设备输入ip加端口号即可
电脑手机均可

http://192.168.31.239:8082 即可访问到我们项目