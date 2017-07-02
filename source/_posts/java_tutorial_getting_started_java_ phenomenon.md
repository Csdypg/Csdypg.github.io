---
title: JAVA 学习指南_开始：Java技术现象
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

# 课程：Java技术现象

好像到处都在谈论Java ，那么到底什么是Java？接下来的几个章节将介绍为什么Java即使编程语言又是开发平台，并简单介绍Java可以为你带来什么。

* [关于Java]()
* [Java可以做什么]()
* [Java将为我的生活带来什么改变]()

<!--more-->

## 关于Java

Java不仅仅是一本编程语言，更是一个开发平台。

### Java 编程语言

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

### Java平台

平台是指程序运行的硬件与软件环境。我们已经提到过一些流行的平台包括微软Windows,Linux,Solaris OS以及Mac OS。大部分平台可以描述为操作系统与底层硬件的结合。Java平台区别与其他大多数平台的地方在于它是一个运行再其他基于硬件的平台之上的纯软件平台。

Java平台包括两部分组件：

* **JVM**(Java 虚拟机)
* **Java Application Programming Interface**(**API** 应用编程接口)

我们已经介绍了**JVM**，**JVM**是**Java**平台的基础，平且可以很方便的运行在不同的基于硬件的平台之上。

API 是预先准备好的软件组件的巨大集合，提供各种各样便利的功能。由相关联的类和接口分为不通的类库;这些类库就是我们熟知的**包**。下一章节，[Java可以做什么？]()将特别说明**API**提供的部分功能。

![Java API 和JVM隔离了程序与底层硬件](http://docs.oracle.com/javase/tutorial/figures/getStarted/getStarted-jvm.gif)

作为一个独立的平台环境，Java平台可能比机器码要慢一点。不过，编译与虚拟机技术的发展将带来接近机器码的性能表现而不影响其便利性（多平台）。



## Java可以做什么

基本用途，高级的Java编程语言是一个强大的软件平台。安装启用Java平台可以为你带来以下特性。

* 开发工具包：开发工具包提供了你编译，运行，监控 ，调试应用程序，以及编写文档所需要的所有工具。作为一个初级开发者，你主要用到的工具是 **javac**编译器，**java**启动器，和**javadoc**文档工具。
* 应用程序编程接口(**API**): API提供了Java编程语言的核心功能。提供了大量的可用类供你再应用程序中使用。从最基本的对象(objects)，到网络编程(networking)以及curity)，到XML文件生成以及数据库接入。核心的**API**非常巨大；如果需要了解全部内容，请参考[Java8文档](https://docs.oracle.com/javase/8/docs/index.html)。
* 部署技术：JDK软件提供了规范机制将你的应用向最终用户发布。例如Java Web Start软件和Java插件软件。
* 用户交互工具包：JavaFX，Swing，Java 2D工具包可以创建复杂的GUI（图形用户界面）。
* 整合类库：众多的整合类库(jar包),例如Java IDL API，JDBC API，JNDI API，Java RMI-IIOP 技术提供了数据库接入以及远程对象操作的功能。

## Java能为我的生活带来什么改变

如果你学习Java编程语言，我们不能保证为你带来名望与财富，甚至是一份工作。:( 但是它仍然可以是你更好的编程，比其他编程语言付出得更少。我们相信Java编程语言可以帮你做到以下几点：

* **快速入门**： 虽然Java是一门非常强大的面向对象编程语言，但是它易于学习，特别是对于已经熟悉了C与C++的开发者。
* **写得少**：程序数量统计(类，方法等的数量统计)比较显示同样的项目用Java编写只需要C++四分之一的代码。
* **写得好**：Java鼓励好的代码规范，并且垃圾回收机制可以帮你避免内存泄漏。Java的面向对象，JavaBeans构造以及广泛，可扩展的API可以帮你重用已有的测试过的代码，减少bug。
* **写的快**：Java比C++更简单，因此你可以节省一般的开发时间，你的应用程序可以用更少的代码实现。
* **避免平台依赖**：避免使用其他语言编写的类库可以是你的项目保持很好的移植性。
* **一次编写处处运行**：Java程序便以为JVM机器码，因此可以方便的运行在任何java平台上。
* **易于发布**：通过Java Web Start 软件，用户可以通过一次点击启动应用。另外启动是的自动版本检查功能可以保证用户总是跟随你应用的最新版本。如果由新的版本可用，Java Web Start软件将会自动安装更新。