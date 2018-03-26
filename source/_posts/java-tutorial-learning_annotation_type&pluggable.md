---
title: Java 学习指南_学习Java：类型注解以及可插拔类型系统
date: 2018-03-23 12:26:59
tags: 
- java
- tutorial
- 教程
- 注解
- annotation
categories:
- java
keywords:
- java
- 教程
- tutorial
- 注解
- annotation
---

# 类型注解以及可插拔的类型系统

Java SE 8版本之前，注解只能被应用于声明或定义。Java 8中，注解可以应用于任何*type use*使用类行的地方。例如，类型实例创建表达式 (`new`),类型转换 casts,实现引用 `implements`,以及抛出异常 `throws` 引用.这种格式的注解叫做类型注解 *type annotation*。注解基础 [Annotations Basics](https://docs.oracle.com/javase/tutorial/java/annotations/basics.html)里提供了几个相关的例子.

类型注解的创建，支持提高确保java程序更强的类型检查的分析方法。Java 8 并没有提供类型检查框架。但是它允许你写或者下载一个类型检查框架，实现一个或者多个可插拔的模块，来与Java编译器结合使用。

例如，你想要确保你程序中一个特定的变量不允许为null；你想要避免触发 `NullPointerException`. 你可以写一个自定义的插件检查这个规则.你现在需要修改你的代码并给对应的变量添加注解,表明其不允许被赋值为null。变量的定义可能如下所示：

```java
@NonNull String str;
```

当你编译代码时，包含 `NonNull` 模块。编译器侦测出潜在的问题就会打印出一个警告，告知你修改代码以避免错误。当你修改代码移除所有的警告之后，这个特定的错误在程序运行时将不会发生.

你也可以使用多个类型检查模块，每个模块检查不同类型的错误。这样，你就可以在Java类型系统之上，添加任何你想要的特定的检查。

由合理的类型注解使用以及插件式类型检查的存在，你可以写出更加健壮的代码，更加不易出错。

很多种情况下，你不需要自己实现类型检查模块。已有第三方为你实现了这些工作。例如，你可能会因为华盛顿大学 University of Washington创建的检查框架而受益.这个框架包含了 `NonNull`模块，一个正则表达式 regular expression 模块, 以及一个互斥锁 mutex lock 模块.参考 [Checker Framework](http://types.cs.washington.edu/checker-framework/)获取更多信息.