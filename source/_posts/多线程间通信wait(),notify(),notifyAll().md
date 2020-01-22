
---
title: 多线程间通信wait(),notify(),notifyAll()
date: 2018-08-28 16:12:49
updated: 2018-08-28 16:12:49
comments: true
tags: 线程通信
//excerpt: 
categories: 并发编程
---

# 多线程间通信wait(),notify(),notifyAll()

通过一个简单的例子实现多线程间通讯的demo

<!--more-->

# 简单介绍

线程间互相通讯使用的是对象的wait()，notify()方法，为保证每个消费者都能够得到消费的对象，所以需要用到同步锁synchronized配合wait(),notify
()来实现。

1.首先有一个生产者，来生产消费者所需的元素。

```java
public class Provider extends Thread {

    @Override
    public void run() {

        while (true) {
            synchronized (queue) {
                try {
                    addFood(queue);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}
```


2.接下来是消费者，在测试中使用了3个消费者来消费

```java
public class Consumer extends Thread {

    @Override
    public void run() {
        while (true) {
            try {
                eatFood(foodQueue);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

3.当生产数大于5个的时候通知消费者消费。

部分打印结果。

```
库吃咔，生产出来一个，现在有1个食物了。
库吃咔，生产出来一个，现在有2个食物了。
库吃咔，生产出来一个，现在有3个食物了。
库吃咔，生产出来一个，现在有4个食物了。
库吃咔，生产出来一个，现在有5个食物了。
已经够多了，大家可以吃了,生产者进入等待
王五拿到了食物，正在吃。。。代号为 9495 的食物
李四拿到了食物，正在吃。。。代号为 5380 的食物
张三拿到了食物，正在吃。。。代号为 4289 的食物
库吃咔，生产出来一个，现在有3个食物了。
库吃咔，生产出来一个，现在有4个食物了。
库吃咔，生产出来一个，现在有5个食物了。
已经够多了，大家可以吃了,生产者进入等待
王五拿到了食物，正在吃。。。代号为 5527 的食物
李四拿到了食物，正在吃。。。代号为 8295 的食物
库吃咔，生产出来一个，现在有4个食物了。
库吃咔，生产出来一个，现在有5个食物了。
已经够多了，大家可以吃了,生产者进入等待
王五拿到了食物，正在吃。。。代号为 1175 的食物
库吃咔，生产出来一个，现在有5个食物了。
已经够多了，大家可以吃了,生产者进入等待
李四拿到了食物，正在吃。。。代号为 2581 的食物
张三拿到了食物，正在吃。。。代号为 1598 的食物
库吃咔，生产出来一个，现在有4个食物了。
库吃咔，生产出来一个，现在有5个食物了。
已经够多了，大家可以吃了,生产者进入等待
李四拿到了食物，正在吃。。。代号为 49 的食物
王五拿到了食物，正在吃。。。代号为 603 的食物
库吃咔，生产出来一个，现在有4个食物了。
```

[完整代码地址](https://gitee.com/lvgo/lvgo-blog-code/tree/master/concurrency/src/main/java/cc/lvgo/concurrency/communaction)