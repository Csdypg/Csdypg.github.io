---
title: Java 学习指南_学习Java：表达式，语句，代码块
date: 2017-09-15 10:00:59
tags: 
- java
- tutorial
- 教程
- Operator
- 运算符
categories:
- java	
keywords:
- java
- 教程
- tutorial
- Expressions
- Statements
- Blocks
- 表达式
- 语句
- 代码块
---

# 表达式，语句，代码块 

现在你已经理解了变量和运算符，是时候表现真正的技术了，哦不是时候学习*表达式，语句，代码块* *expressions*, *statements*, and *blocks*了.运算符可以用来构成表达式，计算值；表达式时语句的核心部件；语句可以被组织为代码块。

## 表达式Expressions

*表达式* 是由变量，运算符，以及方法调用按照Java语言的语法组成的结构，最终球的一个单独的值。已经见到过表达式的例子，参考下面的代码:

```java
int cadence = 0;
anArray[0] = 100;
System.out.println("Element 1 at index 0: " + anArray[0]);

int result = 1 + 2; // result is now 3
if (value1 == value2) 
    System.out.println("value1 == value2");
```

表达式返回值的数据类型取决于表达式使用的元素。表达式 `cadence = 0` 返回 `int` 因为赋值运算符返回其左边的操作因子相同的数据类型；再本例中, `cadence` 是一个`int`. 就像你看到的其他表达式一样，表达式也可以返回其他数据类型的值，例如 `boolean` 或者 `String`.

Java编程语言允许你使用各种各样的小表达式作为一小部分来构建混合表达式，只要数据类型取其他部分匹配。下面是一个混合表达式的例子：

```java
1 * 2 * 3
```

在这个特定的例子里，表达式计算的顺序并不重要，以为乘法计算的结果不依赖计算顺序，结果始终一致，不管你如何计算。然而，并不是所有的表达式都不需要考虑顺序。例如，以下表达式，你先计算加法或者除法得到的结果时不一样的:

```java
x + y / 100    // ambiguous有歧义
```

你可以使用小括号(和)来严格区分表达式的执行顺序。例如：想要让上面的表达式无歧义，你可以这样写：

```java
(x + y) / 100  // unambiguous, recommended无歧义，推荐
```

如果你没有明确的指示运算符的运算顺序,则运算顺序由运算符默认的优先级来确定。拥有更高优先级的运算符，将会有限运算。例如：除法比加法拥有更高的优先级。因此以下两个表达式的运算结果时一样的：

```java
x + y / 100 
x + (y / 100) // unambiguous, recommended
```

当书写复合表达式时，用小括号明确指示那一个运算符先进行计算。这么做可以时代码更加易读和易于管理。

## 语句Statements

语句可以大致理解为自然语言中的句子。一个语句勾构成了一个完整的执行单元。以下类型的表达式以 (`;`)分号结束可以组成语句。

- 赋值表达式Assignment expressions
- 自增自减符号的运用Any use of `++` or `--`
- 方法的调用Method invocations
- 创建对象表达式Object creation expressions

这些语句被成为表达式语句*expression statements*. 以下时一些表达式语句的例子。

```java
// assignment statement 赋值语句
aValue = 8933.234;
// increment statement 自增语句
aValue++;
// method invocation statement 方法调用语句
System.out.println("Hello World!");
// object creation statement 创建对象语句
Bicycle myBike = new Bicycle();
```

除了表达式语句之外，还有另外两种语句：声明语句，和控制流程语句（ *declaration statements* and *control flow statements*）. 声明语句声明一个变量，你已经见过很多例子:

```java
// declaration statement
double aValue = 8933.234;
```

最后，控制流程语句控制语句被执行的规则。下一章节你将会学到更多控制流程相关的内容[Control Flow Statements](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/flow.html).

## 代码块Blocks

代码块是包含在花括号内的一组空语句或者多个语句，可以出现在任何允许出现单独代码块的地方。以下是代码块的示例代码, [`BlockDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/BlockDemo.java):

```java
class BlockDemo {
     public static void main(String[] args) {
          boolean condition = true;
          if (condition) { // begin block 1
               System.out.println("Condition is true.");
          } // end block one
          else { // begin block 2
               System.out.println("Condition is false.");
          } // end block 2
     }
}
```