---
title: Java 学习指南_学习Java：基础-对象-问题与练习
date: 2017-10-20 14:53:59
tags: 
- java
- tutorial
- 教程
- Object
- 对象
categories:
- java
keywords:
- java
- 教程
- tutorial
- Object
- 对象
---

# 对象-问题与练习

## 问题

1. **问题**: 下面的程序有什么问题?

   ```java
   public class SomethingIsWrong {
       public static void main(String[] args) {
           Rectangle myRect;
           myRect.width = 40;
           myRect.height = 50;
           System.out.println("myRect's area is " + myRect.area());
       }
   }
   ```

2. **问题**:  以下代码创建了一个数组对象和字符串对象。当代码实行完毕后，有多少个指向那些对象的引用?是否两个对象都将会垃圾回收器回收?

   ```java
   ...
   String[] students = new String[10];
   String studentName = "Peter Smith";
   students[0] = studentName;
   studentName = null;
   ...
   ```

3. **问题**: 程序是如何销毁一个它创建的对象的?

## 练习

1. **练习**: 修复 `SomethingIsWrong` 代码在问题1中的错误.

2. **练习**: 已知以下类 [`NumberHolder`](http://docs.oracle.com/javase/tutorial/java/javaOO/QandE/NumberHolder.java), 些以下代码创建一个该类的实例，初始化它的两个成员变量，然后显示每个成员变量的值。

   ```java
   public class NumberHolder {
       public int anInt;
       public float aFloat;
   }
   ```



# 答案

<!-- more -->

## 问题答案

1. **问题**: 下面的程序有什么问题?

   ```java
   public class SomethingIsWrong {
       public static void main(String[] args) {
           Rectangle myRect;
           myRect.width = 40;
           myRect.height = 50;
           System.out.println("myRect's area is " + myRect.area());
       }
   }
   ```

   **答案**: 代码从来没有创建一个 [`Rectangle`](http://docs.oracle.com/javase/tutorial/java/javaOO/QandE/Rectangle.java) 对象. 这个简单的程序，编译器将会产生一个错误。不过更加实际的情况是， `myRect` 可能在一个地方被实例化为 `null` ,如果说在构造器中,然后再使用.这种情况下程序可以正常编译，但是会产生一个 `NullPointerException` 运行时异常.

2. **问题**:  以下代码创建了一个数组对象和字符串对象。当代码实行完毕后，有多少个指向那些对象的引用?是否两个对象都将会垃圾回收器回收?

   ```java
   ...
   String[] students = new String[10];
   String studentName = "Peter Smith";
   students[0] = studentName;
   studentName = null;
   ...
   ```

   **答案**: 有一个指向`students`数组的引用，并且数组里有一个指向字符串 `Peter Smith`的引用.两个对象都不会被垃圾回收器回收 .数组 `students`有一个指向`studentName`的引用所以不会被回收，尽管`studentName`已经被赋值为`null`. `studentName`对象也不会被回收因为`students[0]`仍然在引用它。.

3. **问题**: 程序是如何销毁一个它创建的对象的?

   **答案**: 程序并没有显示的销毁一个对象。程序可以设置所有执行一个对象的引用为`null`,这样这个对象就符合被垃圾会少的条件。但是程序并没有销毁对象。

## 练习答案

1. **练习**: 修复 `SomethingIsWrong` 代码在问题1中的错误.

   **Answer**: 参考[`SomethingIsRight`](http://docs.oracle.com/javase/tutorial/java/javaOO/QandE/SomethingIsRight.java):

   ```java
   public class SomethingIsRight {
       public static void main(String[] args) {
           Rectangle myRect = new Rectangle();
           myRect.width = 40;
           myRect.height = 50;
           System.out.println("myRect's area is " + myRect.area());
       }
   }
   ```

2. **练习**: 已知以下类 [`NumberHolder`](http://docs.oracle.com/javase/tutorial/java/javaOO/QandE/NumberHolder.java), 些以下代码创建一个该类的实例，初始化它的两个成员变量，然后显示每个成员变量的值。

   ```java
   public class NumberHolder {
       public int anInt;
       public float aFloat;
   }
   ```

   **答案**: 参考[`NumberHolderDisplay`](http://docs.oracle.com/javase/tutorial/java/javaOO/QandE/NumberHolderDisplay.java):

   ```java
   public class NumberHolderDisplay {
       public static void main(String[] args) {
   	NumberHolder aNumberHolder = new NumberHolder();
   	aNumberHolder.anInt = 1;
   	aNumberHolder.aFloat = 2.3f;
   	System.out.println(aNumberHolder.anInt);
   	System.out.println(aNumberHolder.aFloat);
       }
   }
   ```