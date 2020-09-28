
---
title: 解决 PL/SQL Developer 中文乱码
date: 2019-03-08 10:19:50
updated: 2019-03-08 10:19:50
comments: true
tags: [PL/SQL,乱码]
categories: [随笔,教程]
---


# 当前中文显示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101902235.png)

# 解决后
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101925588.png)

<!--more-->

### 1. 查询当前数据库编码集
```sql
select userenv('language') from dual;
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101212690.png)

### 2. 设置系统环境变量
右击计算机选择属性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101322676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQ0MTIz,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101410401.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQ0MTIz,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101523374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQ0MTIz,size_16,color_FFFFFF,t_70)

1 处填 : NLS_LANG
2 处填 : 刚刚数据库查出来的值 AMERICAN_AMERICA.ZHS16GBK
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101610281.png)

#### 检查当前数据库中文显示

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190308101849623.png)