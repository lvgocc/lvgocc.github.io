
---
title: Java 设计模式（七）《抽象工厂模式》
date: 2018-08-31 09:55:29
updated: 2018-08-31 09:55:29
comments: true
tags: [设计模式,抽象工厂模式]
//excerpt: 
categories: 设计模式
---

# 抽象工厂模式

>抽象工厂模式（Abstract Factory Pattern）是围绕一个超级工厂创建其他工厂。该超级工厂又称为其他工厂的工厂。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

在抽象工厂模式中，接口是负责创建一个相关对象的工厂，不需要显式指定它们的类。每个生成的工厂都能按照工厂模式提供对象。

<!--more-->

---

类型: 创建型

标签:
 - Java
 - Gang Of Four
 - Difficulty-Intermediate（中级难度）

---

## 也称为

Kit

## 意图
提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。

---

## 释义
小案例

> 为了创建一个王国，我们需要具有共同主题的对象。精灵王国需要一个精灵国王，精灵城堡和精灵军队，而兽人王国需要一个兽人国王，兽人城堡和兽人军队。王国中的对象之间存在依赖关系。

简单来说

> 一个工厂的工厂，将一个类别的工厂，组合在一起，而不需要在去指定具体的类型。

[维基百科的解释](https://zh.wikipedia.org/wiki/%E6%8A%BD%E8%B1%A1%E5%B7%A5%E5%8E%82)

> 抽象工厂模式的实质是“提供接口，创建一系列相关或独立的对象，而不指定这些对象的具体类。”

---

**代码实例**

根据上面的例子来讲,我们首先对这个王国的对象有一些抽象的接口.

```java
public interface Castle {
  String getDescription();
}
public interface King {
  String getDescription();
}
public interface Army {
  String getDescription();
}

// Elven implementations ->
public class ElfCastle implements Castle {
  static final String DESCRIPTION = "This is the Elven castle!";
  @Override
  public String getDescription() {
    return DESCRIPTION;
  }
}
public class ElfKing implements King {
  static final String DESCRIPTION = "This is the Elven king!";
  @Override
  public String getDescription() {
    return DESCRIPTION;
  }
}
public class ElfArmy implements Army {
  static final String DESCRIPTION = "This is the Elven Army!";
  @Override
  public String getDescription() {
    return DESCRIPTION;
  }
}

// Orcish implementations similarly...

```

然后我们对王国进行抽象的实现.

```java
public interface KingdomFactory {
  Castle createCastle();
  King createKing();
  Army createArmy();
}

public class ElfKingdomFactory implements KingdomFactory {
  public Castle createCastle() {
    return new ElfCastle();
  }
  public King createKing() {
    return new ElfKing();
  }
  public Army createArmy() {
    return new ElfArmy();
  }
}

public class OrcKingdomFactory implements KingdomFactory {
  public Castle createCastle() {
    return new OrcCastle();
  }
  public King createKing() {
    return new OrcKing();
  }
  public Army createArmy() {
    return new OrcArmy();
  }
}
```

现在我们有了抽象工厂，可以让我们制作一系列相关的物品，如精灵王国工厂创建精灵城堡、国王和军队等。

```java
KingdomFactory factory = new ElfKingdomFactory();
Castle castle = factory.createCastle();
King king = factory.createKing();
Army army = factory.createArmy();

castle.getDescription();  // Output: This is the Elven castle!
king.getDescription(); // Output: This is the Elven king!
army.getDescription(); // Output: This is the Elven Army!
```

现在，我们可以为我们不同的王国工厂设计一个工厂。在这个例子中，我们创建了FactoryMaker，负责返回Elf或Orc厂子的实例。

客户机可以使用FactoryMaker来创建所需对象的工厂，然后该工厂将生成不同的对象（陆军、国王、城堡）。

在这个例子中，我们还使用枚举(Enum)来参数化客户端所请求的王国工厂类型。
```java
public static class FactoryMaker {

  public enum KingdomType {
    ELF, ORC
  }

  public static KingdomFactory makeFactory(KingdomType type) {
    switch (type) {
      case ELF:
        return new ElfKingdomFactory();
      case ORC:
        return new OrcKingdomFactory();
      default:
        throw new IllegalArgumentException("KingdomType not supported.");
    }
  }
}

public static void main(String[] args) {
  App app = new App();

  app.createKingdom(FactoryMaker.makeFactory(KingdomType.ELF));

  app.createKingdom(FactoryMaker.makeFactory(KingdomType.ORC));
  -- similar use of the orc factory
}
```

[更多相关完整详细代码](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/abstract-factory)

---

## 优缺点

优点：当一个产品族中的多个对象被设计成一起工作时，它能保证客户端始终只使用同一个产品族中的对象。

缺点：产品族扩展非常困难，要增加一个系列的某一产品，既要在抽象的 Creator 里加代码，又要在具体的里面加代码。

## 使用契机

* 系统的产品有多于一个的产品族，而系统只消费其中某一族的产品。

---


## 相关教程

* [菜鸟教程](http://www.runoob.com/design-pattern/abstract-factory-pattern.html)
* [Abstract Factory Pattern Tutorial](https://www.journaldev.com/1418/abstract-factory-design-pattern-in-java) 

---


## 实际应用

* [javax.xml.parsers.DocumentBuilderFactory](http://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/DocumentBuilderFactory.html)
* [javax.xml.transform.TransformerFactory](http://docs.oracle.com/javase/8/docs/api/javax/xml/transform/TransformerFactory.html#newInstance--)
* [javax.xml.xpath.XPathFactory](http://docs.oracle.com/javase/8/docs/api/javax/xml/xpath/XPathFactory.html#newInstance--)

---

## 参考文献

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)