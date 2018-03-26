---
title: Java 学习指南_学习Java：定义接口
date: 2018-03-26 15:40:59
tags: 
- java
- tutorial
- 教程
- interface
- 接口
categories:
- java
keywords:
- java
- 教程
- tutorial
- interface
- 接口
---

# 定义一个接口Defining an Interface

接口的定义包含了锌锭修饰符，关键字`interface`，接口名称，逗号分割的父接口（如果有的话）,以及接口体,例如:

```java
public interface GroupedInterface extends Interface1, Interface2, Interface3 {

    // constant declarations
    
    // base of natural logarithms
    double E = 2.718282;
 
    // method signatures
    void doSomething (int i, double x);
    int doSomethingElse(String s);
}
```



`public`修饰符表明了接口可以被任何包中的任何类使用。如果你不加这个修饰符，接口就只能被定义在用一个包中的类作为接口实现。

接口可以扩展自其它接口，与类扩展其它的类一样。不过，区别是类值能扩展一个类，但是一个几口可以扩展任何数量的接口，接口定义中包含了他扩展的逗号分割的父接口。

## 接口体The Interface Body

接口体可以包含 [抽象方法abstract methods](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html), [默认default methods](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html), 以及 [静态static methods](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html#static). 接口中的抽象方法由分号结尾，但是不包括大括号包围的方法体（即没有方法的实现）。默认方法有`default`修饰符定义，静态方法由 `static`关键字。接口中所有的抽象方法，默认方法，静态方法 都是`public`,所以你可以省略 `public`修饰符.

另外，几口可以包含常量声明。接口中定义的所有常量都是 `public`, `static`, 并且 `final`的.所有你可以省略这些限定修饰符.