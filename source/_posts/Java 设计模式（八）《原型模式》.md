
---
title: Java 设计模式（八）《原型模式》
date: 2018-09-21 15:09:31
updated: 2018-09-21 15:09:31
comments: true
tags: 设计模式
categories: 设计模式
---



# 原型模式
>原型模式（Prototype Pattern）是用于创建重复的对象，同时又能保证性能。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

<!--more-->

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

# 意图

使用原型实例来指定创建对象的种类，并通过拷贝创建出新的对象

---

# 解决问题

在运行期建立或删除原型

---

```java
public class Shape implements Cloneable {

    private String name;

    public Shape(String name) {
        this.name = name;
    }
    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```
[完整代码地址](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/prototype)

---

# 何时使用

1. 当一个系统应该独立于它的产品创建，构成和表示时。 
2. 当要实例化的类是在运行时刻指定时，例如，通过动态装载。 
3. 为了避免创建一个与产品类层次平行的工厂类层次时。 
4. 当一个类的实例只能有几个不同状态组合中的一种时。建立相应数目的原型并克隆它们可能比每次用合适的状态手工实例化该类更方便一些。

---

# 使用场景

1. 资源优化场景。 
2. 类初始化需要消化非常多的资源，这个资源包括数据、硬件资源等。 
3. 性能和安全要求的场景。 
4. 通过 new 产生一个对象需要非常繁琐的数据准备或访问权限，则可以使用原型模式。 
5. 一个对象多个修改者的场景。 
6. 一个对象需要提供给其他对象访问，而且各个调用者可能都需要修改其值时，可以考虑使用原型模式拷贝多个对象供调用者使用。 
7. 在实际项目中，原型模式很少单独出现，一般是和工厂方法模式一起出现，通过 clone 的方法创建一个对象，然后由工厂方法提供给调用者。

原型模式已经与 Java 融为浑然一体，大家可以随手拿来使用。

---

# 注意事项：

与通过对一个类进行实例化来构造新对象不同的是，原型模式是通过拷贝一个现有对象生成新对象的。
浅拷贝实现 Cloneable，重写，
深拷贝是通过实现 Serializable 读取二进制流。

优点： 
1. 性能提高。 
2. 逃避构造函数的约束。

缺点： 
1. 配备克隆方法需要对类的功能进行通盘考虑，这对于全新的类不是很难，但对于已有的类不一定很容易，特别当一个类引用不支持串行化的间接对象，或者引用含有循环结构的时候。 
2. 必须实现 Cloneable 接口。

---

## 应用实例

* [java.lang.Object#clone()](http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#clone%28%29)
