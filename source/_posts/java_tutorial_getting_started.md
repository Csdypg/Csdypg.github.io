---
title: JAVA 学习指南_开始
date: 2017-06-28 01:16:59
tags: 
- java
- tutorial
- 教程
categories:
- java	
keywords:
- java
- 教程
- tutorial
---

# 学习路径：开始

本学习路径提供了Java编程语言入门的所有内容。

* [Java 技术现象]() Java 技术整体概览。讨论了Java编程语言和Java 平台两部分内容，简要概括了这门技术可以做什么以及它能为你的生活带来什么便利。
* ["Hello world!"应用]() 手把手的教你如何下载安装Java开发环境，以及如创建一个简单的"Hello world!"应用。分别提供了NetBeans IDE，Windows，Solaris OS，Linux，以及Mac用户版本的教程。
* [深入了解"Hello World!"]()  详细描述了"Hello World!"应用的每一部分代码，包括代码注释，HelloWorldApp类定义代码块，以及main方法。
* [常见问题以及解决方法]() 如果你在编译几运行项目中遇到麻烦可以在这里找到问题。

<!--more-->

# 课程：Java技术现象

好像到处都在谈论Java ，那么到底什么是Java？接下来的几个章节将介绍为什么Java即使编程语言又是开发平台，并简单介绍Java可以为你带来什么。

* [关于Java]()
* [Java可以做什么]()
* [Java将为我的生活带来什么改变]()



# 关于Java

Java不仅仅是一本编程语言，更是一个开发平台。

## Java 编程语言

Java编程语言是一门高级语言，可以用一下流行词来概括Java：

| Simple简单             | Architecture neutral |
| -------------------- | -------------------- |
| Object oriented 面向对象 | Protable 轻便的         |
| Distributed 分布式      | High performance 高性能 |
| MultiThreaded 多线程的   | Robust 健壮的           |
| Dynamic 动态           | Secure 安全            |

上面提到的每一个流行特性都在 James Gosling 和Henry McGilton编写的 [The Java Language Environment](http://www.oracle.com/technetwork/java/langenv-140151.html)中*(原版的Java语言环境白皮书)*有详细的解释。

在Java编程语言中，所有的源代码首先都是在扩展名为**.java**的文本文档中编写的。这些源代码由javac编译器编译为.class文件。一个**.class**文件中并不包含可以由计算机直接运行的代码，而是包含了bytecodes--JVM*(Java Virtual Machine ,Java虚拟机)* 的机器语言。然后Java运行工具用一个JVM实例运行你的应用程序。

![软件开发简要流程](http://docs.oracle.com/javase/tutorial/figures/getStarted/getStarted-compiler.gif)

由于JVM可以运行在不同的操作系统上，所以相同的**.class**文件能够同时运行在Windows，Solaris OS，Linux， Mac OS上。一些JVM，例如 [Java SE HotSpot at a Glance](http://www.oracle.com/technetwork/java/javase/tech/index-jsp-136373.html) 提供额为的运行时功能以增强应用的性能，包括查找性能瓶颈，将频繁用到的代码片段再编译（编译为native code，机器码）等多种多样的特性。

![通过JVM，同样的应用可以运行再不同的平台上](http://docs.oracle.com/javase/tutorial/figures/getStarted/helloWorld.gif)

## Java平台

平台是指程序运行的硬件与软件环境。我们已经提到过一些流行的平台包括微软Windows,Linux,Solaris OS以及Mac OS。大部分平台可以描述为操作系统与底层硬件的结合。Java平台区别与其他大多数平台的地方在于它是一个运行再其他基于硬件的平台之上的纯软件平台。

Java平台包括两部分组件：

* **JVM**(Java 虚拟机)
* **Java Application Programming Interface**(**API** 应用编程接口)

我们已经介绍了**JVM**，**JVM**是**Java**平台的基础，平且可以很方便的运行在不同的基于硬件的平台之上。

API 是预先准备好的软件组件的巨大集合，提供各种各样便利的功能。由相关联的类和接口分为不通的类库;这些类库就是我们熟知的**包**。下一章节，[Java可以做什么？]()将特别说明**API**提供的部分功能。

![Java API 和JVM隔离了程序与底层硬件](http://docs.oracle.com/javase/tutorial/figures/getStarted/getStarted-jvm.gif)

作为一个独立的平台环境，Java平台可能比机器码要慢一点。不过，编译与虚拟机技术的发展将带来接近机器码的性能表现而不影响其便利性（多平台）。