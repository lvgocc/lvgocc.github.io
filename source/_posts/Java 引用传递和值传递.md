
---
title: Java 引用传递和值传递
date: 2018-05-17 15:56:44
updated: 2018-05-17 15:56:44
comments: true
tags: 
//excerpt: 
categories: Java
---

## 还是没能通俗易懂

- 引用传递就是指   将对象的地址值进行传递

- 值传递 就是把对象的值进行传递

<!--MORE-->

```

// 我有一个类    ClassA

// new 一个对象 ClassA classa =  new ClassA();

我调用一个方法 fun1
```
```
 void fun1(ClassA classa) {   // 这里面的ClassA 就是做的引用传递，他是个形参，那实际参数是什么呢？？ 这里不对，实参是对象的值

}

void  fun2(int a, String b, Long c) { // 这里的参数  a ，b ，c 是形参，他代表的是一个具体的值。所以他的传递就是值传递

} 

// ClassA classa int a, String b, Long c 都是形参

// new ClassA(); 是实参
```

看下代码 你就明白了
```
 public static void main(String args[]) {
        People people = new People();
        System.out.println("people = " + people);
        String a = "string";
        System.out.println("a = " + a);
        int i = 111;
        System.out.println("i = " + i);
        double j = 11.12223;
        System.out.println("j = " + j);
    }
```
```
people = People@5fd0d5ae  
// 这里面的 People@5fd0d5ae 就是 对象 people 在堆中的地址  他在作为参数的时候，传的就是这个东西 
// 然后你在方法里做逻辑的时候，用的就是这个地址对应的值，你去操作他，一旦你对这个值进行了修改，那么
// 源对象的值，也会被修改，就好比，我告诉你冰箱里有一瓶水，你喝了三分之一，等我回家的时候，再去看那瓶水就是被你喝过的。是的
// 这个就是引用传递  引用类型传引用，形参和实参指向同一个内存地址（同一个对象），所以对参数的修改会影响到实际的对象；
a = string
i = 111
j = 11.12223

java中的基本类型，包括string在内 都是值传递，他们的改变，不会影响源数据。
```
>值传递只会作用在方法内部，不会影响方法外的数据。

```
 public static void main(String[] args) {
        // 我们把这个param传到了方法里，方法对其进行了修改
        String param = "我是参数";
        System.out.println("\nparam = " + param);
        // 执行修改操作，引用传递的值将会被改变，值传递的值将不受影响
        change(param);
        System.out.println("\n我是方法执行过的参数 param ， 我现在的值是 = " + param);
    }

    private static void change(String param) {
        System.out.println("传入进来的参数的值 param = " + param);
        System.out.println("\n下面我的值将会被改变");
        // 方法执行过程中对值传递的变量进行修改，不会影响源数据
        param = "我把值传递的内容改了";
        System.out.println("\n我已经把 param 内容修改掉了，修改成了 ：" + param);
    }
```
```
param = 我是参数
传入进来的参数的值 param = 我是参数

下面我的值将会被改变

我已经把 param 内容修改掉了，修改成了 ：我把值传递的内容改了

我是方法执行过的参数 param ， 我现在的值是 = 我是参数
```

#### 引用传递
```
    public static void main(String[] args) {
        StringBuilder a = new StringBuilder("A");
        StringBuilder b = new StringBuilder("B");
        operate(a, b);
        System.out.println("--------------------------");
        System.out.println(a + "." + b);
    }

    static void operate(StringBuilder x, StringBuilder y) {
        x.append(y);
        System.out.println("x = " + x);
        y = x;
        System.out.println("y = " + y);
    }
-------------------------
x = AB
y = AB
--------------------------
AB.B
```
##### 说明
这个问题的关键在于  a,b,x,y 的地址指向；
y = x 与 b = a 是不等价的！！
发生改变的是 y 指向的值变成了和 x 指向的相同， 此时 y = AB（因为append方法改变的x原有的值）
而此时 b 的指向并没有发生改变。

##### 划重点
引用传递过程中，只有引用对象的值发生了改变才会影响源数据。地址的改变不会影响源数据。



-----
