---
title: 设计模式简介
top: false
cover: false
toc: true
mathjax: true
date: 2020-09-25 20:28:29
password:
summary:
tags:
- 设计模式
categories:
- 笔记
---

# 设计模式

## 1. 单例模式

属于创建型模式，它提供了一种创建对象的最佳方式。

这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

单例模式的几种实现方式

### 1.懒汉式，线程不安全

**是否 Lazy 初始化：**是
**是否多线程安全：**否
**实现难度：**易

**描述：**这种方式是最基本的实现方式，这种实现最大的问题就是不支持多线程。因为没有加锁 synchronized，所以严格意义上它并不算单例模式。
这种方式 lazy loading 很明显，不要求线程安全，在多线程不能正常工作。

```java
public class Singleton {      
    private static Singleton instance;      
    private Singleton (){}//构造器私有        
    public static Singleton getInstance() {      
        if (instance == null) {          
            instance = new Singleton();      
        }      
        return instance;      
    }   
}
```

**接下来介绍的几种实现方式都支持多线程，但是在性能上有所差异**

### 2.懒汉式，线程安全

**是否 azy 初始化：**是
**是否多线程安全：**是
**实现难度：**易

**描述：**这种方式具备很好的 lazy loading，能够在多线程中很好的工作，但是效率很低，99% 情况下不需要同步。
优点：第一次调用才初始化，避免内存浪费。
缺点：必须加锁 synchronized 才能保证单例，但加锁会影响效率。
getInstance() 的性能对应用程序不是很关键（该方法使用不太频繁）。

```java
public class Singleton {  
    private static Singleton instance;  
    
    private Singleton (){}  
    
    public static synchronized Singleton getInstance() {  
    if (instance == null) {  
        instance = new Singleton();  
    }  
    return instance;  
    }  
}
```

### 3.饿汉式

**是否 Lazy 初始化：**否
**是否多线程安全：**是
**实现难度：**易

**描述：**这种方式比较常用，**但容易产生垃圾对象。**
优点：没有加锁，执行效率会提高。
缺点：类加载时就初始化，浪费内存。
它基于 classloader 机制避免了多线程的同步问题，不过，instance 在类装载时就实例化，虽然导致类装载的原因有很多种，在单例模式中大多数都是调用 getInstance 方法， 但是也不能确定有其他的方式（或者其他的静态方法）导致类装载，这时候初始化 instance 显然没有达到 lazy loading 的效果。

```java
public class Singleton {  
    private static Singleton instance = new Singleton();  
    private Singleton (){}  
    public static Singleton getInstance() {  
    return instance;  
    }  
}
```

### 4.双检锁/双重校验锁

（DCL，即 double-checked locking）JDK 版本：**JDK1.5 起**

**是否 Lazy 初始化：**是
**是否多线程安全：**是
**实现难度：**较复杂

**描述：**这种方式采用双锁机制，安全且在多线程情况下能保持高性能。
getInstance() 的性能对应用程序很关键。

```java
public class Singleton {  
    private volatile static Singleton singleton;  
    
    private Singleton (){} 
    
    public static Singleton getSingleton() {  
        if (singleton == null) {  
            synchronized (Singleton.class) { //加锁，锁当前对象
                if (singleton == null) {  
                    singleton = new Singleton();//不是原子性操作  
                }  
            }  
        }  
    	return singleton;  
    }  
}
//指令重排有可能导致对象未完成构造，所以加volatile
```



### 5.登记式/静态内部类

**是否 Lazy 初始化：**是
**是否多线程安全：**是
**实现难度：**一般

**描述：**这种方式能达到双检锁方式一样的功效，但实现更简单。对静态域使用延迟初始化，应使用这种方式而不是双检锁方式。这种方式只适用于静态域的情况，双检锁方式可在实例域需要延迟初始化时使用。
这种方式同样利用了 classloader 机制来保证初始化 instance 时只有一个线程，它跟第 3 种方式不同的是：第 3 种方式只要 Singleton 类被装载了，那么 instance 就会被实例化（没有达到 lazy loading 效果），而这种方式是 Singleton 类被装载了，instance 不一定被初始化。因为 SingletonHolder 类没有被主动使用，只有通过显式调用 getInstance 方法时，才会显式装载 SingletonHolder 类，从而实例化 instance。想象一下，如果实例化 instance 很消耗资源，所以想让它延迟加载，另外一方面，又不希望在 Singleton 类加载时就实例化，因为不能确保 Singleton 类还可能在其他的地方被主动使用从而被加载，那么这个时候实例化 instance 显然是不合适的。这个时候，这种方式相比第 3 种方式就显得很合理。

```java
public class Singleton {  
    private Singleton (){} 
    
    private static class SingletonHolder {  
    	private static final Singleton INSTANCE = new Singleton();  
    }  
     
    public static final Singleton getInstance() {  
    	return SingletonHolder.INSTANCE;  
    }  
}
```


### 6、枚举

**JDK 版本：**JDK1.5 起

**是否 Lazy 初始化：**否
**是否多线程安全：**是
**实现难度：**易

**描述：**这种实现方式还没有被广泛采用，但这是实现单例模式的最佳方法。它更简洁，自动支持序列化机制，绝对防止多次实例化。
这种方式是 Effective Java 作者 Josh Bloch 提倡的方式，它不仅能避免多线程同步问题，而且还自动支持序列化机制，防止反序列化重新创建新的对象，绝对防止多次实例化。不过，由于 JDK1.5 之后才加入 enum 特性，用这种方式写不免让人感觉生疏。
不能通过 reflection attack 来调用私有构造方法。

```java
public enum Singleton {  
    INSTANCE;  
    public void whateverMethod() {  
    }  
}
```

### **经验之谈：**

一般情况下，不建议使用第 1 种和第 2 种懒汉方式，建议使用第 3 种饿汉方式。

只有在要明确实现 lazy loading 效果时，才会使用第 5 种登记方式。

如果涉及到反序列化创建对象时，可以尝试使用第 6 种枚举方式。如果有其他特殊的需求，可以考虑使用第 4 种双检锁方式。



## 2. 策略模式

在策略模式中，一个类的行为或其算法可以在运行时更改。这种类型的设计模式属于行为型模式。

在策略模式中，我们创建表示各种策略的对象和一个行为随着策略对象改变而改变的 context 对象。策略对象改变 context 对象的执行算法。

**意图：定义一系列的算法,把它们一个个封装起来, 并且使它们可相互替换。**
**主要解决：**在有多种算法相似的情况下，使用 if...else 所带来的复杂和难以维护。
**何时使用：**一个系统有许多许多类，而区分它们的只是他们直接的行为。
**如何解决：**将这些算法封装成一个一个的类，任意地替换。
**关键代码：**实现同一个接口。

**优点：** 1、算法可以自由切换。 2、避免使用多重条件判断。 3、扩展性良好。
**缺点：** 1、策略类会增多。 2、所有策略类都需要对外暴露。

**使用场景：** 1、如果在一个系统里面有许多类，它们之间的区别仅在于它们的行为，那么使用策略模式可以动态地让一个对象在许多行为中选择一种行为。 2、一个系统需要动态地在几种算法中选择一种。 3、如果一个对象有很多的行为，如果不用恰当的模式，这些行为就只好使用多重的条件选择语句来实现。

**注意事项：**如果一个系统的策略多于四个，就需要考虑使用混合模式，解决策略类膨胀的问题。

## 实现

我们将创建一个定义活动的 *Strategy* 接口和实现了 *Strategy* 接口的实体策略类。*Context* 是一个使用了某种策略的类。

*StrategyPatternDemo*，我们的演示类使用 *Context* 和策略对象来演示 Context 在它所配置或使用的策略改变时的行为变化。

![策略模式的UML图](strategy_pattern_uml_diagram.jpg)

