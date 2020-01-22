
---
title: Java 设计模式（一）《适配器模式》
date: 2018-08-21 11:30:46
updated: 2018-08-21 11:30:46
comments: true
tags: 设计模式
//excerpt: 
categories: 设计模式
---


# 适配器模式

>适配器模式（Adapter Pattern）是作为两个不兼容的接口之间的桥梁。这种类型的设计模式属于结构型模式，它结合了两个独立接口的功能。

这种模式涉及到一个单一的类，该类负责加入独立的或不兼容的接口功能。

- 类型: 结构型
- 难度：入门级

更多设计模式小故事案例代码详解 >>[点我！点我！点我！](https://gitee.com/lvgo/java-design-patterns-cn)<< 设计模式，如此简单～

<!--more-->

----

## 别名
Wrapper （包装）（适配器模式（Adapter Pattern）和装饰器模式（Decorator Pattern）的统称）


----

## 设计目的
将一个类的接口转换成客户希望的另外一个接口。适配器模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。


----

## 释义

生活中的例子


>你有一个张内存卡，有一台电脑，你现在想要看内存卡上的照片，想听内存卡上的歌，想看内存卡上的电影，但是你直接插电脑上又插不上去，所以你需要一个适配器，那就是读卡器。这样你的内存卡就可以在电脑上运行了。

>你的iphone x的手机，想要听歌，但是耳机忘记带了，所以和我来借，可是我是国产的OPPO，所以你从包里拿出来一个转换插头，让耳机插到转换插头上，再插到手机上，这个转换插头就是适配器。

>侵华的日本鬼子当年侵华无法和我们沟通，结果你猜怎么着，那个汉奸就是适配器，他把日语转成了中文，把中文转成了日语。勿忘国耻！


简单来讲

>适配器模式可以让你在适配器中包装一个与另一个对象不兼容的对象，使其兼容。

[来自维基百科的解释](https://zh.wikipedia.org/wiki/%E9%80%82%E9%85%8D%E5%99%A8%E6%A8%A1%E5%BC%8F)

>将一个类的接口转接成用户所期待的。一个适配使得因接口不兼容而不能在一起工作的类能在一起工作，做法是将类自己的接口包裹在一个已存在的类中。

----


**代码实例讲解**

有一个船长，只会使用划艇，不会使用渔船。

首先，我们有接口`RowingBoat`和`FishingBoat`

```java
public interface RowingBoat {
  void row();
}

public class FishingBoat {
  private static final Logger LOGGER = LoggerFactory.getLogger(FishingBoat.class);
  public void sail() {
    LOGGER.info("The fishing boat is sailing");
  }
}
```

并且船长本身是会划艇的，所以船长已经实现了这个接口。

```java
public class Captain implements RowingBoat {

  private RowingBoat rowingBoat;

  public Captain(RowingBoat rowingBoat) {
    this.rowingBoat = rowingBoat;
  }

  @Override
  public void row() {
    rowingBoat.row();
  }
}
```

现在来了一个海盗，并且只有渔船可以使用，我们的船长想要逃避海盗，就只能使用渔船。所以我们需要一个适配器来帮助船长来用他操作划艇的技术来操作渔船。


```java
public class FishingBoatAdapter implements RowingBoat {

  private static final Logger LOGGER = LoggerFactory.getLogger(FishingBoatAdapter.class);

  private FishingBoat boat;

  public FishingBoatAdapter() {
    boat = new FishingBoat();
  }

  @Override
  public void row() {
    boat.sail();
  }
}
```

现在，船长既可以开着渔船逃避海盗了。

```java
Captain captain = new Captain(new FishingBoatAdapter());
captain.row();
```

### [完整代码传送 >>>](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/adapter)

----



## 使用契机

什么时候使用适配器模式？

* 你想使用现有的类，但是这个类的接口不符合你所需要的。
* 你现在想要创建一个类，用在一些彼此之间没有太大关联的类，包括一些以后将来引进的类一起工作。这些类不一定有一致的接口。
* 通过接口转换，将一个类插入另一个类系中。（比如老虎和飞禽，现在多了一个飞虎，在不增加实体的需求下，增加一个适配器，在里面包容一个虎对象，实现飞的接口。）
* 大多数使用第三方库的应用程序使用适配器作为应用程序和第三方库之间的中间层，以将应用程序与库解耦。如果必须使用另一个库，则只需要为新库添加适配器，而不必更改应用程序代码。


----

## 结论:

类适配器和对象适配器的区别

类适配器

*	通过提交到具体的需要适配的类来使适配器来适应目标类。 因此，当我们想要调整类及其所有子类时，类适配器将不起作用。
*	让适配器覆盖一些适配者的行为， 因为适配器是适配者的子类。
*	只需要引入一个对象，不需要其他的指针来间接的指向适配器。
*  适配器Adapter继承我们的被适配者Adaptee，并实现目标接口。由于Java中是单继承，所以这个适配器仅仅只能服务于所继承的被适配者Adaptee


对象适配器

*  适配器实现我们的目标接口，但是并不继承需要被适配的类。而是通过在适配器的构造函数中将需要被适配的类传递进来从而进行适配
*	让一个适配器与许多适配者一起工作 - 即适配者本身及其所有子类（如果有的话）。 适配器还可以立即向所有适配者添加功能。
*	覆盖适配者Adaptee的方法复杂困难，需要适配器使用一个适配者的子类，不能直接引用适配者。

----

## 优缺点

优点： 

1. 可以让任何两个没有关联的类一起运行。
2. 提高了类的复用。
3. 增加了类的透明度。 
4. 灵活性好。

缺点： 

1. 过多地使用适配器，会让系统非常零乱，不易整体进行把握。比如，明明看到调用的是 A 接口，其实内部被适配成了 B 接口的实现，一个系统如果太多出现这种情况，无异于一场灾难。因此如果不是很有必要，可以不使用适配器，而是直接对系统进行重构。 
2. 由于 JAVA 至多继承一个类，所以至多只能适配一个适配者类，而且目标类必须是抽象类。

----


## jdk中使用到此模式的地方

[JDK 1.9 中英文 chm 文档下载](https://download.csdn.net/download/sinat_34344123/10177790)

* [java.util.Arrays#asList()](http://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#asList%28T...%29)
* [java.util.Collections#list()](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#list-java.util.Enumeration-)
* [java.util.Collections#enumeration()](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#enumeration-java.util.Collection-)
* [javax.xml.bind.annotation.adapters.XMLAdapter](http://docs.oracle.com/javase/8/docs/api/javax/xml/bind/annotation/adapters/XmlAdapter.html#marshal-BoundType-)

----

## 参考文献

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [J2EE Design Patterns](http://www.amazon.com/J2EE-Design-Patterns-William-Crawford/dp/0596004273/ref=sr_1_2)