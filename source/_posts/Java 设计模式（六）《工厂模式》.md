
---
title: Java 设计模式（六）《工厂模式》
date: 2018-08-24 17:31:43
updated: 2018-08-24 17:31:43
comments: true
tags: 设计模式
//excerpt: 
categories: 设计模式
---

# 工厂模式

>工厂模式（Factory Pattern）是 Java 中最常用的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

在工厂模式中，我们在创建对象时不会对客户端暴露创建逻辑，并且是通过使用一个共同的接口来指向新创建的对象。

<!--more-->

## [本文源代码及更多设计模式学习点我](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/factory)

---
所属类型: 创建型

标签:
 - Java
 - Gang Of Four
 - Difficulty-Beginner(入门级难度)


注：
>``什么是 GOF（四人帮，全拼 Gang of Four）？``
>在 1994 年，由 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides 四人合著出版了一本名为 Design Patterns - Elements of Reusable Object-Oriented Software（中文译名：设计模式 - 可复用的面向对象软件元素） 的书，该书首次提到了软件开发中设计模式的概念。
>四位作者合称 GOF（四人帮，全拼 Gang of Four）。他们所提出的设计模式主要是基于以下的面向对象设计原则。
>对接口编程而不是对实现编程。
>优先使用对象组合而不是继承。


---

## 别名

虚拟构造器

## 意图
定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行。

---

## 释义

小故事案例

> 铁匠可以打造武器,精灵需要精灵的武器,兽人需要兽人的武器.铁匠要根据不同的顾客来让对应的铁匠师傅打造不同的武器.


简单来说

> 工厂模式可以通过委托的方式对目标进行实例化

[维基百科这样说](https://zh.wikipedia.org/wiki/%E5%B7%A5%E5%8E%82%E6%96%B9%E6%B3%95#%E7%AE%80%E5%8D%95%E5%B7%A5%E5%8E%82)

> In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

 **代码实例**

根据上面的案例,首先我们有一个铁匠和一些实现方法

```java
public interface Blacksmith {
  Weapon manufactureWeapon(WeaponType weaponType);
}

public class ElfBlacksmith implements Blacksmith {
  public Weapon manufactureWeapon(WeaponType weaponType) {
    return new ElfWeapon(weaponType);
  }
}

public class OrcBlacksmith implements Blacksmith {
  public Weapon manufactureWeapon(WeaponType weaponType) {
    return new OrcWeapon(weaponType);
  }
}
```

根据不同的需求打造不同的武器

```java
Blacksmith blacksmith = new ElfBlacksmith();
blacksmith.manufactureWeapon(WeaponType.SPEAR);
blacksmith.manufactureWeapon(WeaponType.AXE);
// Elvish weapons are created
```

[案例源码点我](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/factory)

---

## 适用性

* 创建对象需要大量重复的代码。
* 创建对象需要访问某些信息，而这些信息不应该包含在复合类中。
* 创建对象的生命周期必须集中管理，以保证在整个程序中具有一致的行为。


## 优缺点

优点： 

1. 一个调用者想创建一个对象，只要知道其名称就可以了。 
2. 扩展性高，如果想增加一个产品，只要扩展一个工厂类就可以。 
3. 屏蔽产品的具体实现，调用者只关心产品的接口。

缺点：

- 每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。这并不是什么好事。


## 注意事项
>作为一种创建类模式，在任何需要生成复杂对象的地方，都可以使用工厂方法模式。有一点需要注意的地方就是复杂对象适合使用工厂模式，而简单对象，特别是只需要通过 new 就可以完成创建的对象，无需使用工厂模式。如果使用工厂模式，就需要引入一个工厂类，会增加系统的复杂度。


## 相关教程(英文)

* [Factory Method Pattern](etc/presentation.html) 

---

## 实际的应用

* [java.util.Calendar](http://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html#getInstance--)
* [java.util.ResourceBundle](http://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html#getBundle-java.lang.String-)
* [java.text.NumberFormat](http://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getInstance--)
* [java.nio.charset.Charset](http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html#forName-java.lang.String-)
* [java.net.URLStreamHandlerFactory](http://docs.oracle.com/javase/8/docs/api/java/net/URLStreamHandlerFactory.html#createURLStreamHandler-java.lang.String-)
* [java.util.EnumSet](https://docs.oracle.com/javase/8/docs/api/java/util/EnumSet.html#of-E-)
* [javax.xml.bind.JAXBContext](https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/JAXBContext.html#createMarshaller--)

---

## 参考文献

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)