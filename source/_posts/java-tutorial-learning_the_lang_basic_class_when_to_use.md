---
title: Java 学习指南_学习Java：基础-何时使用嵌套类，局部类，匿名类，Lambda
date: 2018-03-19 14:51:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- 嵌套类
- 局部类
- 匿名类
- Lambda
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- 嵌套类
- 局部类
- 匿名类
- Lambda
---

# 何时使用嵌套类，局部类，匿名类，Lambda表达式

正如在嵌套类 [Nested Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)一章节中提到的,嵌套类可以使你将只是用一次的代码符合逻辑的整理到一块，增加代码的封装性，创建更可读和易于管理的代码。局部类，匿名类以及Lambda表达式同样适用于这些优势；并且他们可以用于更加具体的场景:

- [局部类Local class](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html): 如果你需要创建类的不止一个实例，访问其构造函数，或者引入新的命名类型（因为，譬如你需要在后续条用额外的方法).
- [匿名类Anonymous class](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html): 如果你需要定义额外的字段或者方法就使用匿名类.
- [Lambda表达式Lambda expression](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html):
  - 如果你想要封装一个单独的行为床底给其他的代码就是用Lambda表达式。例如，你你需要创建一个具体的作用于集合中每个元素的操作，当一个程序完成时的处理，或者程序遇到错误的处理。
  - 当你需要你功能接口的你个简单实例并且不需要预先的条件限制。（例如，你不需要使用构造器，不需要明明类型，字段，或者额外的方法）
- [嵌套类Nested class](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html): 当你的需求与局部类相似，但是又想让类有更广的可用范围，并且你不需要访问局部变量和更多的方法参数就使用嵌套类。
  - 使用非静态的嵌套类（或者内部类）如果你需要访问闭合空间内的非公有字段或者方法。是用静态的嵌套类如果你不需要这些访问接入。