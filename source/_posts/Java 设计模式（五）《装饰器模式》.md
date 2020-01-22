
---
title: Java 设计模式（五）《装饰器模式》
date: 2018-08-23 13:02:06
updated: 2018-08-23 13:02:06
comments: true
tags: 设计模式
//excerpt: 
categories: 设计模式
---


# 装饰器模式

>装饰器模式（Decorator Pattern）允许向一个现有的对象添加新的功能，同时又不改变其结构。这种类型的设计模式属于结构型模式，它是作为现有的类的一个包装。

这种模式创建了一个装饰类，用来包装原有的类，并在保持类方法签名完整性的前提下，提供了额外的功能。

更多设计模式小故事案例代码详解 >>[点我！点我！点我！](https://gitee.com/lvgo/java-design-patterns-cn)<< 设计模式，如此简单～

<!--more-->

---

所属类型: 结构型

标签:
 - Java
 - Gang Of Four
 - Difficulty-Beginner(入门级难度)

---



注：
>``什么是 GOF（四人帮，全拼 Gang of Four）？``
>在 1994 年，由 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides 四人合著出版了一本名为 Design Patterns - Elements of Reusable Object-Oriented Software（中文译名：设计模式 - 可复用的面向对象软件元素） 的书，该书首次提到了软件开发中设计模式的概念。
>四位作者合称 GOF（四人帮，全拼 Gang of Four）。他们所提出
>对接口编程而不是对实现编程。
>优先使用对象组合而不是继承。



## 别名
Wrapper(包装器) （适配器模式（Adapter Pattern）和装饰器模式（Decorator Pattern）的统称）


## 意图

动态地给一个对象添加一些额外的职责。就增加功能来说，装饰器模式相比生成子类更为灵活。(看完之后你会发现,装饰器模式可以替代继承)

## 释义

小故事案例

> 有一只怪兽,它平时的时候赤手空拳,攻击力有10.如果要攻击力到20需要一把武器,现在我们不需要重新找一个有武器的怪兽,只需要给现在的怪兽增加10攻击就可以了.

简单来说

> 装饰器模式可以在装饰器类中通过装饰,来动态的改变被装饰类的行为

维基百科这样说

> 在面向对象编程中，装饰器模式是一种设计模式，它允许静态或动态地将行为添加到单个对象，而不影响来自同一类的其他对象的行为。装饰模式对于坚持单一的责任原则通常是有用的，因为它允许功能在具有独特关注区域的类之间进行划分。


---

**代码详解**

我们有一个小怪兽接口和一个简单的小怪兽

```java
public interface Troll {
  void attack();
  int getAttackPower();
  void fleeBattle();
}

public class SimpleTroll implements Troll {

  private static final Logger LOGGER = LoggerFactory.getLogger(SimpleTroll.class);

  @Override
  public void attack() {
    LOGGER.info("The troll tries to grab you!");
  }

  @Override
  public int getAttackPower() {
    return 10;
  }

  @Override
  public void fleeBattle() {
    LOGGER.info("The troll shrieks in horror and runs away!");
  }
}
```

接着我们通过一个装饰类来动态的装饰我们的小怪兽

```java
public class ClubbedTroll implements Troll {

  private static final Logger LOGGER = LoggerFactory.getLogger(ClubbedTroll.class);

  private Troll decorated;

  public ClubbedTroll(Troll decorated) {
    this.decorated = decorated;
  }

  @Override
  public void attack() {
    decorated.attack();
    LOGGER.info("The troll swings at you with a club!");
  }

  @Override
  public int getAttackPower() {
    return decorated.getAttackPower() + 10;
  }

  @Override
  public void fleeBattle() {
    decorated.fleeBattle();
  }
}
```

装饰前后

```java
// simple troll
Troll troll = new SimpleTroll();
troll.attack(); // The troll tries to grab you!
troll.fleeBattle(); // The troll shrieks in horror and runs away!

// change the behavior of the simple troll by adding a decorator
troll = new ClubbedTroll(troll);
troll.attack(); // The troll tries to grab you! The troll swings at you with a club!
troll.fleeBattle(); // The troll shrieks in horror and runs away!
```

[更多完整代码点此查看](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/decorator)

---

## 适用契机


* 扩展一个类的功能。 
* 动态增加功能，动态撤销。
* 通过子类的扩展是不切实际的。有时，大量的独立扩展是可能的，并且会产生大量子类来支持每个组合。或者类定义可以隐藏或不可用于子类化。

## 优缺点

优点：装饰类和被装饰类可以独立发展，不会相互耦合，装饰模式是继承的一个替代模式，装饰模式可以动态扩展一个实现类的功能。

缺点：多层装饰比较复杂。
注意事项：可代替继承。注意事项：可代替继承。
## 相关教程

* [Decorator Pattern Tutorial](https://www.journaldev.com/1540/decorator-design-pattern-in-java-example)

---

## 实际应用

 * [java.io.InputStream](http://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html), [java.io.OutputStream](http://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html),
 [java.io.Reader](http://docs.oracle.com/javase/8/docs/api/java/io/Reader.html) and [java.io.Writer](http://docs.oracle.com/javase/8/docs/api/java/io/Writer.html)
 * [java.util.Collections#synchronizedXXX()](http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#synchronizedCollection-java.util.Collection-)
 * [java.util.Collections#unmodifiableXXX()](http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#unmodifiableCollection-java.util.Collection-)
 * [java.util.Collections#checkedXXX()](http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#checkedCollection-java.util.Collection-java.lang.Class-)


## 参考文献

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Functional Programming in Java: Harnessing the Power of Java 8 Lambda Expressions](http://www.amazon.com/Functional-Programming-Java-Harnessing-Expressions/dp/1937785467/ref=sr_1_1)
* [J2EE Design Patterns](http://www.amazon.com/J2EE-Design-Patterns-William-Crawford/dp/0596004273/ref=sr_1_2)