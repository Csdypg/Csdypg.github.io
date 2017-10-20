---
title: Java 学习指南_学习Java：基础-类-问题域练习
date: 2017-10-20 15:39:59
tags: 
- java
- tutorial
- 教程
- class
- 类
categories:
- java
keywords:
- java
- 教程
- tutorial
- class
- 类
---

# 类：问题与练习

## 问题

1. 观察下面的类:

   ```java
   public class IdentifyMyParts {
       public static int x = 7;
       public int y = 3;
   } 
   ```

   1. **问题**: 哪一个是类变量?

   2. **问题**:哪一个是实例变量?

   3. **问题**: 以下代码的输出内容是什么:

      ```
      IdentifyMyParts a = new IdentifyMyParts(); 
      IdentifyMyParts b = new IdentifyMyParts(); 
      a.y = 5; 
      b.y = 6; 
      a.x = 1; 
      b.x = 2; 
      System.out.println("a.y = " + a.y); 
      System.out.println("b.y = " + b.y); 
      System.out.println("a.x = " + a.x); 
      System.out.println("b.x = " + b.x); 
      System.out.println("IdentifyMyParts.x = " + IdentifyMyParts.x);
      ```

      ​

## 练习

1. **练习**: 写一个类，类的每一个实例代表了一副牌中的一张。没一张牌有两个属性：点数与花色。保留你的解决方案，在 [Enum Types](http://docs.oracle.com/javase/tutorial/java/javaOO/QandE/enum-questions.html) 枚举类一节中会要求你重写这个类.
2. **练习**: 写一个类，类的每一个实例代表**一整副**扑克。同样保留这个类。
3. **练习**：写一个小程序来测试你的单长牌与扑克类。可以简单的创建一副扑克并展示它其中的每一张牌。



# 答案

<!-- more -->

## 问题答案

1. 观察下面的类:

   ```java
   public class IdentifyMyParts {
       public static int x = 7;
       public int y = 3;
   } 
   ```

   1. **问题**: 哪一个是类变量?

      **答案**: x

   2. **问题**:哪一个是实例变量?

      **答案**: y

   3. **问题**: 以下代码的输出内容是什么:

      ```
      IdentifyMyParts a = new IdentifyMyParts(); 
      IdentifyMyParts b = new IdentifyMyParts(); 
      a.y = 5; 
      b.y = 6; 
      a.x = 1; 
      b.x = 2; 
      System.out.println("a.y = " + a.y); 
      System.out.println("b.y = " + b.y); 
      System.out.println("a.x = " + a.x); 
      System.out.println("b.x = " + b.x); 
      System.out.println("IdentifyMyParts.x = " + IdentifyMyParts.x);
      ```

      **答案**: 输出如下:

      ```
       a.y = 5 
       b.y = 6 
       a.x = 2 
       b.x = 2
       IdentifyMyParts.x = 2

      ```

      因为 `x`的在类`IdentifyMyParts`中的定义为 `public static int` 。每一个指向`x`的引用都有最后赋给`x`的值，因为`x`是一个静态变量（或者说类变量），为所有类的实例所共享。也就是说只有一个`x`: 当`x`的值在任何实例中发生改变就会影响所有 `IdentifyMyParts`类的实例的`x`值.

      在理解类与实例的成员一节中包含了这些内容 [Understanding Instance and Class Members]().

## 练习答案

1. **练习**: 写一个类，类的每一个实例代表了一副牌中的一张。没一张牌有两个属性：点数与花色。保留你的解决方案，在 [Enum Types](http://docs.oracle.com/javase/tutorial/java/javaOO/QandE/enum-questions.html) 枚举类一节中会要求你重写这个类.

   **答案**: [`Card.java`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/Card.java)![(in a .java source file)](http://docs.oracle.com/javase/tutorial/images/sourceIcon.gif).

2. **练习**: 写一个类，类的每一个实例代表**一整副**扑克。同样保留这个类。

   **答案**:  [`Deck.java`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/Deck.java)![(in a .java source file)](http://docs.oracle.com/javase/tutorial/images/sourceIcon.gif).

3. **练习**：写一个小程序来测试你的单长牌与扑克类。可以简单的创建一副扑克并展示它其中的每一张牌。

   **答案**:  [`DisplayDeck.java`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/DisplayDeck.java)![(in a .java source file)](http://docs.oracle.com/javase/tutorial/images/sourceIcon.gif).