---
title: Java 学习指南_学习Java：基础-枚举类问题与练习
date: 2018-03-21 18:51:59
tags: 
- java
- tutorial
- 教程
- 类
- enum
- 枚举类
categories:
- java
keywords:
- java
- 教程
- tutorial
- enum
- 枚举类
---

# 枚举类问题与练习

## 问题

1. 问题: True or false: 枚举类可以是 java.lang.String类的子类.

## 练习

1. 练习: 重写 [Questions and Exercises: Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/creating-questions.html) 中 `Card` 类，使用枚举类来表示扑克中的花色和点数。
2. 练习: 重写 `Deck` 类.



# 答案



<!--more -->

## 问题答案

1. 问题: True or false: 枚举类可以是 java.lang.String类的子类.

   答案: False. 所有的枚举类都继承自 `java.lang.Enum`.因为一个类只能继承字一个父类，Java语言不支持多重继承，因此枚举类不可能是任何其他类的子类.

## 练习答案

1. 练习: 重写 [Questions and Exercises: Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/creating-questions.html) 中 `Card` 类，使用枚举类来表示扑克中的花色和点数。

   答案: 参考 [`Card3.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/Card3.java), [`Suit.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/Suit.java), 和 [`Rank.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/Rank.java).

2. 练习: 重写 `Deck` 类.

   答案: 参考 [`Deck3.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/Deck3.java).