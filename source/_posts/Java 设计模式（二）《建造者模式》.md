
---
title: Java 设计模式（二）《建造者模式》
date: 2018-08-21 21:48:08
updated: 2018-08-21 21:48:08
comments: true
tags: 设计模式
//excerpt: 
categories: 设计模式
---


# 建造者模式

>建造者模式（Builder Pattern）使用多个简单的对象一步一步构建成一个复杂的对象。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

一个 Builder 类会一步一步构造最终的对象。该 Builder 类是独立于其他对象的。

- 类型: 创建型
- 难度：中级

更多设计模式小故事案例代码详解 >>[点我！点我！点我！](https://gitee.com/lvgo/java-design-patterns-cn)<< 设计模式，如此简单～

----

<!--more-->

## 解决问题
将一个复杂的构建与其表示相分离，使得同样的构建过程可以创建不同的表示。

----

## 如何实现

将变与不变分离开

----

## 释义

实际例子

> 角色扮演类的游戏，在我们创建角色的时候，可以选择性别，身高，职业，如果我们要实现更为复杂的角色时，肤色，头发颜色等。但无论你怎么选择当你点击确认的时候你的角色就诞生了。

简单来讲

> 建造者模式可以让你使用同一个建造器，构建满足你要求的东西，无论组装的顺序，以及组装的内容多少。

[百度百科的解释](https://baike.baidu.com/item/%E5%BB%BA%E9%80%A0%E8%80%85%E6%A8%A1%E5%BC%8F/3229729)

>建造者模式是设计模式的一种，将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。

维基百科的解释

> Builder模式是一个对象创建设计模式，为了寻找伸缩构造函数来解决具体问题。

让我们看一看到底是什么是伸缩构造函数

```java
public Hero(Profession profession, String name, HairType hairType, HairColor hairColor, Armor armor, Weapon weapon) {
}
```

就像你所看到的这样，这个构造函数的参数可能在不久的将来业务的增长，会越来越长，变得难以维护。

----

**代码实例讲解**

此时使用建造者模式就是一个不错的选择

```java
public final class Hero {
  private final Profession profession;
  private final String name;
  private final HairType hairType;
  private final HairColor hairColor;
  private final Armor armor;
  private final Weapon weapon;

  private Hero(Builder builder) {
    this.profession = builder.profession;
    this.name = builder.name;
    this.hairColor = builder.hairColor;
    this.hairType = builder.hairType;
    this.weapon = builder.weapon;
    this.armor = builder.armor;
  }
}
```

然后我们需要有一个建造者 Builder

```java
  public static class Builder {
    private final Profession profession;
    private final String name;
    private HairType hairType;
    private HairColor hairColor;
    private Armor armor;
    private Weapon weapon;

    public Builder(Profession profession, String name) {
      if (profession == null || name == null) {
        throw new IllegalArgumentException("profession and name can not be null");
      }
      this.profession = profession;
      this.name = name;
    }

    public Builder withHairType(HairType hairType) {
      this.hairType = hairType;
      return this;
    }

    public Builder withHairColor(HairColor hairColor) {
      this.hairColor = hairColor;
      return this;
    }

    public Builder withArmor(Armor armor) {
      this.armor = armor;
      return this;
    }

    public Builder withWeapon(Weapon weapon) {
      this.weapon = weapon;
      return this;
    }

    public Hero build() {
      return new Hero(this);
    }
  }
```

然后他可以用作构建我们的参数。

```java
Hero mage = new Hero.Builder(Profession.MAGE, "Riobard").withHairColor(HairColor.BLACK).withWeapon(Weapon.DAGGER).build();
```
[更多完整代码 ===>> 传送门](https://gitee.com/lvgo/java-design-patterns-cn)

----

## 使用契机

什么时候使用建造者模式？

* 需要生成的对象具有复杂的内部结构。
* 构造过程允许对构造的对象有不同的展示结果。

----

## 优缺点

优点

1. 建造者独立，易扩展。 
2. 于控制细节风险。

缺点

1. 产品必须有共同点，范围有限制。 
2. 如内部变化复杂，会有很多的建造类。

----

## 就在你身边的实际应用

[JDK1.9 中英文 chm 格式文档下载](https://download.csdn.net/download/sinat_34344123/10177790)

* [java.lang.StringBuilder](http://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html)
* [java.nio.ByteBuffer](http://docs.oracle.com/javase/8/docs/api/java/nio/ByteBuffer.html#put-byte-) as well as similar buffers such as FloatBuffer, IntBuffer and so on.
* [java.lang.StringBuffer](http://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#append-boolean-)
* All implementations of [java.lang.Appendable](http://docs.oracle.com/javase/8/docs/api/java/lang/Appendable.html)
* [Apache Camel builders](https://github.com/apache/camel/tree/0e195428ee04531be27a0b659005e3aa8d159d23/camel-core/src/main/java/org/apache/camel/builder)

----

## 参考文献

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Effective Java (2nd Edition)](http://www.amazon.com/Effective-Java-Edition-Joshua-Bloch/dp/0321356683)