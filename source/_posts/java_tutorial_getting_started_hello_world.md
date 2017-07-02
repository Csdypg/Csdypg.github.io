---
title: JAVA 学习指南-HelloWorld应用
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

# 课程：”Hello World"应用

以下列出的章节提共不同平台创建“Hello World”应用的详细指导。第一部分提供了利用NetBeans IDE创建应用的教程，NetBeans IDE是一个极大简化程序开发过程的集成开发环境，可以运行在以下任一个平台。剩余部分提供了针对不同平台命令行工具开发知道。如果运行出现问题，可以在参考常见问题章节，入门者碰到的大部分问题都可以找到解决方法。

* [适用NetBeans 开发Hello World ](http://docs.oracle.com/javase/tutorial/getStarted/cupojava/netbeans.html) 本教程针对NetBeans IDE使用者。NetBeans IDE运行在Java 平台上，意味这只要你的操作系统支持 JDK7，就可以使用NetBeans。Windows, Solaris OS, Linux, and Mac OS X都是支持的。如果可以请尽量适用IDE代替命令行开发。
* [Microsoft Windows 开发 Hello World]()  本命令行开发教程适用于Windows XP Professional, Windows XP Home, Windows Server 2003, Windows 2000 Professional, and Windows Vista等用户。
* ["Solaris OS ,Linux 开发 Hello World!" ](http://docs.oracle.com/javase/tutorial/getStarted/cupojava/unix.html) 本命令行开发教程适用于 Solaris OS and Linux用户.编译及与运行过程中碰到任何问题都可以参考 [常见问题及解决方法](http://docs.oracle.com/javase/tutorial/getStarted/problems/index.html) 。
  <!--more-->
  由于篇幅问题，本文将只翻译Windows部分。

# Windows开发"Hello World"应用

是时候见识真正的实力了。 哦不，是时候开发你的第一个应用程序了。接下来的教程适用于Windows系统用户，其他操作系统用户请参考另外两部分教程。

在本教程中遇到任何问题，请参考 [常见问题及解决方法](http://docs.oracle.com/javase/tutorial/getStarted/problems/index.html) 。

## 检查清单  ![a checkmark](http://docs.oracle.com/javase/tutorial/figures/getStarted/check.gif)

你需要准备以下内容:

1.  JDK8，如果没有，请[下载](http://www.oracle.com/technetwork/java/javase/downloads/index.html)及[安装](https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)。

2. 一个文本编辑器

   在本实例中，我们适用了记事本，Windows平台自带的文本编辑器。如果你适用其他的文本编辑器也是可以的。

------

## 创建你的第一个应用程序

你的第一个应用程序，将简单的显示出一句问候"Hello world!",创建该应用你需要做以下事情：

* 创建一个文件
  一个包含代码以.java为后缀的源文件，用你和其他开发者可以阅读和理解的Java语言编写。你可以适用任何文本编辑器创建和编辑.java文件。
* 将源文件编译为.class文件
  Java编译器（javac）获取你.java源文件并且翻译为JVM可以理解的指令。包含这些指令的文件叫做bytecodes(字节码).
* 运行程序
  Java应用启动工具 java 适用JVM运行你的应用程序。

### 创建一个.java源文件

首先，启动你的文本编辑器。创建一个文件，输入以下代码。

```java
/**
 * The HelloWorldApp class implements an application that
 * simply prints "Hello World!" to standard output.
 * 实现在控制台/终端输出"Hello world!"简单功能的类.
 */
class HelloWorldApp {
    public static void main(String[] args) {
        System.out.println("Hello World!"); // 输出字符串.
    }
}
```

**注意输入的字母要区分大小写** ![uppercase letter A](http://docs.oracle.com/javase/tutorial/figures/getStarted/typeA.gif)   ![lowercase letter A](http://docs.oracle.com/javase/tutorial/figures/getStarted/typea2.gif)

------

注意:
`javac`和`java`命令以及Jav代码都是大小写敏感的，所以大小写一定要保持一致。
`HelloWorldApp`不是`helloworldapp`

------

将写好的代码保存并命名为HelloWorldApp.java.在记事本里做这件事情，首先选在文件>另存为菜单项。

然后在另存为对话框如下:

1. 在Save in 保存位置选择框，选择你要保存的文件位置。本例中选在C盘下的myapplication文件夹。
2. 在文件名选择框，输入”HelloWorldApp.java",不包含括号。
3. 在文件类型选择框，选择Text Documents(*.txt)文件。
4. 在Encoding(编码)选择框，选择”ANSI“编码。

当你完成以后对话框如下显示：

![TEXT The Save As dialog, as described in the text.](http://docs.oracle.com/javase/tutorial/figures/getStarted/saveas.png)

你点击**Save**保存以前的对话框。

现在点击保存，退出记事本。

### 编译.java源文件为.class文件

打开一个Shell或者Command窗口。你可以在Start开始菜单选择Run运行然后输入`cmd`。命令窗口看起来如下图所示。

![a window where you can enter DOS commands](http://docs.oracle.com/javase/tutorial/figures/getStarted/dos.png)命令窗口.

提示显示你当前的文件夹路径。一般当你打开一个命令窗口，你的当前路径一般是你的home目录，Windows系统一般如上图所示的目录。

为了编译你的Java源文件，需要改变当前目录为HelloWorldApp.java所在的目录，在命令窗口输入如下命令：

```
cd C:\myapplication
```

現在提示信息应该变为`C:\myapplication`

---

​	注意：

如果目录在不同的磁盘分区上，你必须输入另外的命令。例如你的文件在D盘下myapplication文件夹下，你需要输入如下命令

```
C:\> D:

D:\> cd myapplication

D:\myapplication>
```

------

如果你输入`dir`命令，应.该看到你的.java源文件，如下：

```
C:\>cd myapplication

C:\myapplication>dir
 Volume in drive C is System
 Volume Serial Number is F2E8-C8CC

 Directory of C:\myapplication

2014-04-24  01:34 PM    <DIR>          .
2014-04-24  01:34 PM    <DIR>          ..
2014-04-24  01:34 PM               267 HelloWorldApp.java
               1 File(s)            267 bytes
               2 Dir(s)  93,297,991,680 bytes free

C:\myapplication>
```

现在你已经准备好编译了。在提示信息后输入如下命令并按下**Enter**.

```
javac HelloWorldApp.java
```

编译器已经生成了一个字节码文件，HelloWorldApp.class.在提示信息中输入`dir`查看新生生的文件如下：

```
C:\myapplication>javac HelloWorldApp.java

C:\myapplication>dir
 Volume in drive C is System
 Volume Serial Number is F2E8-C8CC

 Directory of C:\myapplication

2014-04-24  02:07 PM    <DIR>          .
2014-04-24  02:07 PM    <DIR>          ..
2014-04-24  02:07 PM               432 HelloWorldApp.class
2014-04-24  01:34 PM               267 HelloWorldApp.java
               2 File(s)            699 bytes
               2 Dir(s)  93,298,032,640 bytes free

C:\myapplication>
```

现在你已经拥有一个.calss文件，你可以运行你的程序。

如果你在本教程的步骤中遇到问题，参考 [常见问题及解决方法](http://docs.oracle.com/javase/tutorial/getStarted/problems/index.html) 

### 运行程序

在同样的当前目录下，在提示信息后输入以下命令:

```
java -cp . HelloWorldApp
```

你应该在屏幕上看到如下信息:

```
C:\myapplication>java -cp . HelloWorldApp
Hello World!

C:\myapplication>
```

恭喜！你完成第一个Java程序！

如果你在本教程的步骤中遇到问题，参考 [常见问题及解决方法](http://docs.oracle.com/javase/tutorial/getStarted/problems/index.html) 