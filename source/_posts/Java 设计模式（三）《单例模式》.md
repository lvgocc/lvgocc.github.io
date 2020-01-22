
---
title: Java 设计模式（三）《单例模式》
date: 2018-08-22 14:38:22
updated: 2018-08-22 14:38:22
comments: true
tags: 设计模式
//excerpt: 
categories: 设计模式
---


# 单例模式

>单例模式（Singleton Pattern）是 Java 中最简单的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

_更多设计模式小故事案例代码详解 >>[点我！点我！点我！](https://gitee.com/lvgo/java-design-patterns-cn)<< 设计模式，如此简单～_

----

<!--more-->

tags:
 - Java
 - Gang Of Four
 - Difficulty-Beginner(入门级难度)

---


注：
>``什么是 GOF（四人帮，全拼 Gang of Four）？``
>在 1994 年，由 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides 四人合著出版了一本名为 Design Patterns - Elements of Reusable Object-Oriented Software（中文译名：设计模式 - 可复用的面向对象软件元素） 的书，该书首次提到了软件开发中设计模式的概念。
>四位作者合称 GOF（四人帮，全拼 Gang of Four）。他们所提出的设计模式主要是基于以下的面向对象设计原则。
>对接口编程而不是对实现编程。
>优先使用对象组合而不是继承。

----


## 所要解决的问题

保证一个类只有一个实例，并且全局可以访问它。


## 说明

身边的例子

> 中国只能同时拥有一个国家主席

通俗的讲

> 要保证始终特定的类只有一个实例

[来自维基百科的解释](https://zh.wikipedia.org/wiki/%E5%8D%95%E4%BE%8B%E6%A8%A1%E5%BC%8F)

> 单例模式，也叫单子模式，是一种常用的软件设计模式。在应用这个模式时，单例对象的类必须保证只有一个实例存在。许多时候整个系统只需要拥有一个的全局对象，这样有利于我们协调系统整体的行为。比如在某个服务器程序中，该服务器的配置信息存放在一个文件中，这些配置数据由一个单例对象统一读取，然后服务进程中的其他对象再通过这个单例对象获取这些配置信息。这种方式简化了在复杂环境下的配置管理。
  


**代码实践**

Joshua Bloch, Effective Java 2nd Edition p.18

> 单元素枚举是使用单例模式最佳的实践.

```java
public enum EnumIvoryTower {
  INSTANCE;
}
```

然后我们在使用

```java
EnumIvoryTower enumIvoryTower1 = EnumIvoryTower.INSTANCE;
EnumIvoryTower enumIvoryTower2 = EnumIvoryTower.INSTANCE;
assertEquals(enumIvoryTower1, enumIvoryTower2); // true
```

<a href="https://gitee.com/lvgo/java-design-patterns-cn/tree/master/singleton"><img src="https://gitee.com//logo-black.svg?20171024" height=30px> [↖更多代码实践传送](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/singleton) 

----


## 什么时候使用单例模式

* 要求生产唯一序列号
* 需求上必须只能存在一个对象,并且客户端能够从一个公共的地方访问它.
* 当您想控制实例数目,创建一个对象消耗过多资源,如数据库连接等,节省系统资源的时候.

----

## 优缺点

优点： 

1. 在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例（比如管理学院首页页面缓存）。 
2. 避免对资源的多重占用（比如写文件操作）。

缺点：

- 没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化。

----

## 典型应用

* 项目中记录日志的类
* 数据库连接
* 我们使用的操作系统的文件管理器

----


## 实际应用

* [java.lang.Runtime#getRuntime()](http://docs.oracle.com/javase/8/docs/api/java/lang/Runtime.html#getRuntime%28%29)
* [java.awt.Desktop#getDesktop()](http://docs.oracle.com/javase/8/docs/api/java/awt/Desktop.html#getDesktop--)
* [java.lang.System#getSecurityManager()](http://docs.oracle.com/javase/8/docs/api/java/lang/System.html#getSecurityManager--)

----



## 结论

* 有类本身控制创建和销毁,违反了单一职责原则
* 鼓励使用全局共享实例，防止该对象使用的对象和资源被解除分配。     

----

## 参考文献

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Effective Java (2nd Edition)](http://www.amazon.com/Effective-Java-Edition-Joshua-Bloch/dp/0321356683)