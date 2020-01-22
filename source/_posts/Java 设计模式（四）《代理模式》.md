
---
title: Java 设计模式（四）《代理模式》
date: 2018-08-23 10:38:26
updated: 2018-08-23 10:38:26
comments: true
tags: 设计模式
//excerpt: 
categories: 设计模式
---


#代理模式

更多设计模式小故事案例代码详解 >>[点我！点我！点我！](https://gitee.com/lvgo/java-design-patterns-cn)<< 设计模式，如此简单～

---

<!--more-->

所属类型: 结构型

标签:
 - Java
 - Gang Of Four
 - Difficulty-Beginner (入门级难度)

---


注：
>``什么是 GOF（四人帮，全拼 Gang of Four）？``
>在 1994 年，由 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides 四人合著出版了一本名为 Design Patterns - Elements of Reusable Object-Oriented Software（中文译名：设计模式 - 可复用的面向对象软件元素） 的书，该书首次提到了软件开发中设计模式的概念。
>四位作者合称 GOF（四人帮，全拼 Gang of Four）。他们所提出的设计模式主要是基于以下的面向对象设计原则。
>对接口编程而不是对实现编程。
>优先使用对象组合而不是继承。

---

## 意图

为一个类提供替代或者控制其来访问目标类

---


## 说明

生活中的例子

> 周末小朋友们要去游乐园玩耍，但是游乐园需要买票，所以只能通过检票口（游乐园代理）之后才能进入，因为今天日子比较特殊，所以只有前5名小朋友才能进入，所以我们需要在检票口对我们的游乐园做访问限制。

通俗来说

> 通过代理模式，我们可以使用一个类来表示另一个类的功能

[维基百科这样讲](https://zh.wikipedia.org/wiki/%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F)

> 所谓的代理者是指一个类别可以作为其它东西的接口。代理者可以作任何东西的接口：网络连接、存储器中的大对象、文件或其它昂贵或无法复制的资源。

---

**代码实操**

我们的游乐园有一个统一的大门接口(检票口),那有一个进入的方法,小朋友可以通过这个入口进入游乐园

```java
public interface TicketCheck {

  void enter(Children children);
}

public class AmusementPark implements TicketCheck {

     @Override
     public void enter(Children children) {
         System.out.println(children.getName() + "小朋友进入到了游乐园,开始了玩耍");
     }
}
```

这是一个只有名字的简单的小朋友类

```java
public class Children {

    private String name;

    public Children(String name) {
        this.name = name;
    }
}
```

然后我们通过游乐园的代理类,来对访问做限制

```java
public class AmusementParkProxy implements TicketCheck {

    private static int MAX_ENTER_NUM = 5;
    
    private TicketCheck ticketCheck;
    
    private int current;

    public AmusementParkProxy(TicketCheck ticketCheck) {
        this.ticketCheck = ticketCheck;
    }

    /**
     * 定义一个进入游乐园的方法
     *
     * @param children 小朋友
     */
    @Override
    public void enter(Children children) {
        if (current < MAX_ENTER_NUM) {
            ticketCheck.enter(children);
            current++;
        } else {
            System.out.println("抱歉,今天" + children.getName() + "不能够再进去了,游乐园要爆炸了");
        }
    }
}

```

模拟进入游乐园情况

```java
AmusementParkProxy amusementParkProxy = new AmusementParkProxy(new AmusementPark());
ArrayList<Children> children = new ArrayList<>();
children.add(new Children("小明"));
children.add(new Children("张三"));
children.add(new Children("卿尚师"));
children.add(new Children("司元慈"));
children.add(new Children("马青峰"));
children.add(new Children("小鬼"));
children.add(new Children("铭三"));
children.add(new Children("轻柳"));
children.add(new Children("尚元慈"));
children.add(new Children("嗯哼仓"));
children.forEach(amusementParkProxy::enter);

// 打印信息

小明小朋友进入到了游乐园,开始了玩耍
张三小朋友进入到了游乐园,开始了玩耍
卿尚师小朋友进入到了游乐园,开始了玩耍
司元慈小朋友进入到了游乐园,开始了玩耍
马青峰小朋友进入到了游乐园,开始了玩耍
抱歉,今天小鬼不能够再进去了,游乐园要爆炸了
抱歉,今天铭三不能够再进去了,游乐园要爆炸了
抱歉,今天轻柳不能够再进去了,游乐园要爆炸了
抱歉,今天尚元慈不能够再进去了,游乐园要爆炸了
抱歉,今天嗯哼仓不能够再进去了,游乐园要爆炸了

```

[详细代码点我查看](https://gitee.com/lvgo/java-design-patterns-cn/tree/master/proxy)

---

## 适用场景

* 保护代理控制对原始对象的访问。当对象具有不同的访问权限时，保护代理是有用的。
* 目标对象,创建复杂或消耗大量资源.
* 目标对象不在本地.

1. 远程代理。 
2. 虚拟代理。 
3. Copy-on-Write 代理。 
4. 保护（Protect or Access）代理。 
5. Cache代理。 
6. 防火墙（Firewall）代理。
7. 同步化（Synchronization）代理。 
8. 智能引用（Smart Reference）代理。

---


## 注意

1. 和适配器模式的区别：适配器模式主要改变所考虑对象的接口，而代理模式不能改变所代理类的接口。 
2. 和装饰器模式的区别：装饰器模式为了增强功能，而代理模式是为了加以控制。

---

## 优缺点

优点： 

1. 职责清晰。 
2. 高扩展性。 
3. 智能化。

缺点： 

1. 由于在客户端和真实主题之间增加了代理对象，因此有些类型的代理模式可能会造成请求的处理速度变慢。 
2. 实现代理模式需要额外的工作，有些代理模式的实现非常复杂。

---


## 相关教程
* [Controlling Access With Proxy Pattern](http://java-design-patterns.com/blog/controlling-access-with-proxy-pattern/)


---

## 实际应用

* [java.lang.reflect.Proxy](http://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Proxy.html)
* [Apache Commons Proxy](https://commons.apache.org/proper/commons-proxy/)
* Mocking frameworks Mockito, Powermock, EasyMock
* Spring AOP

---

## 参考文献

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)