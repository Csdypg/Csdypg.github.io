---
title: JAVA 学习指南_开始：深入了解”Hello World“应用程序
date: 2017-07-01 00:19:59
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
- hello world
---

# 课程:深入了解”Hello World“应用程序

现在你已经看到了Hello World应用程序，或许也已经编译运行了，或许你会疑惑它是怎么工作的.再看一遍它的代码:

```java
class HelloWorldApp {
    public static void main(String[] args) {
        System.out.println("Hello World!"); // Display the string.
    }
}
```

HelloWorld 应用有三个关键的部分组成：源码注释，HelloWorldApp类定义，以及main方法。通过以下内容你将对这段代码有一个基本的理解，但是更深层的含义只有你完成了教程剩余部分才会理解透彻。

<!--more-->

## [源码注释]()

[以下棕色部分的代码部分为代码注释]()

```java
/**
 * The HelloWorldApp class implements an application that
 * simply prints "Hello World!" to standard output.
 */
class HelloWorldApp {
    public static void main(String[] args) {
        System.out.println("Hello World!"); // Display the string.
    }
}
```

注释会被编译器忽略但是对其他开发人员有很有用。Java支持三种注释形式。

Comments are ignored by the compiler but are useful to other programmers. The Java programming language supports three kinds of comments:

- `/* *text* */`

  多行注释，编译器会忽略从`/*` 到 `*/`之间的内容.

- `/** *documentation* */`

  文档注释，该内容表示文档注释，编译器会忽略该注释，就像多行注释一样。**javadoc**工具可以利用文档注释自动生成文档。关于**javadoc**的更多内容可以参考 [Javadoc™ 工具文档](https://docs.oracle.com/javase/8/docs/technotes/guides/javadoc/index.html) .


- `// *text*`

  单行注释，编译器会忽略`//`以后到本行结束的内容。

## [ `HelloWorldApp` 类定义]()

[以下内容为类定义块]()

最基本的类定义形式如下:

```java
class name {
    . . .
}
```

The keyword `class` begins the class definition for a class named `name`, and the code for each class appears between the opening and closing curly braces marked in bold above. Chapter 2 provides an overview of classes in general, and Chapter 4 discusses classes in detail. For now it is enough to know that every application begins with a class definition.

## [`main` 方法]()

[以下内容为`main`方法定义:]()

```java
    public static void main(String[] args) {
        System.out.println("Hello World!"); //Display the string.
    }
```

在Java中，每一个应用程序都必须包含一个`main`方法，特征如下：

```java
public static void main(String[] args)
```

修饰词`public`和`static`顺序可以为`public static`或者`static public`,但是按照惯例都写做`public static`.你也可以将参数名字明明为任何你想要的名字，但是大多数程序猿都选择`args`或者`argv`.

`main`方法与C和C++中的`main`方法非常类似，是你程序的入口程序，并调用你程序需要的后续所有其他方法。

`main`方法接受一个单独的参数:一个`String`类型的**Array**数组。

```java
public static void main(String[] args)
```

通过这个设置的数组，系统向应用程序传递运行参数。例如：

```shell
java MyApp arg1 arg2
```

数组里的每一个字符串叫做command-lin argument命令行参数。命令行参数可以是用户不重新编译的情况下改变程序的运行方式。例如，一个排序程序允许用户输入命令行参数让数据按照降序排列：

```
-descending
```

Hello World应用忽略了命令行参数，但是你应该意识到这些参数存在的事实。

最终，这一行:

```
System.out.println("Hello World!");
```

使用用核心包中System类向终端输出"Hello world!"信息。核心类库(也叫做API)的各个部分将在本教程的剩余所有内容中讨论到。