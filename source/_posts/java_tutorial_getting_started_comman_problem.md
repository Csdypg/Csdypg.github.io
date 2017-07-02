---
title: JAVA 学习指南-常见问题及解决方法
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

# 课程:常见问题及解决方法

## [编译问题]()

**Windows 常见错误** 

`**'javac' is not recognized as an internal or external command, operable program or batch file**`

如果碰到这个问题，Windows找不到编译器**javac**

有一种方法可以告诉Windows去哪找到`javac`.假设你安装了JDK8 在`C:\jdk1.8.0`目录下。在命令行提示信息后输入如下命令并按下Enter回车键。

```
C:\jdk1.8.0\bin\javac HelloWorldApp.java
```

如果你选择这么操作，那么你每次编译和运行程序都需要在`javac`和`java`命令之前添加该路径。为了避免每次都输入，你可以在参考JDK8安装教程中的[配置环境变量](https://docs.oracle.com/javase/8/docs/technotes/guides/install/windows_jdk_install.html#BABGDJFH)。

`**Class names, 'HelloWorldApp', are only accepted if annotation processing is explicitly requested**`

如果你碰到这个错误，说明你在执行`javac`的时候忘了写`.java`后缀。记住，命令应该是 `javac HelloWorldApp.java`而不是`javac HelloWorldApp`.
<!--more-->
**Unix系统常见错误**

`javac: Command not found`

如果碰到这个错误，UNIX系统找不到编译器`javac`。有一种简单的方法让UNIX找到`javac`.假设你安装了JDK在`/usr/local/jdk1.8.0`.你应该在命令行输入如下命令并按下回车：

```
/usr/local/jdk1.8.0/javac HelloWorldApp.java
```

**注意:**如果你选择这么操作，那么你每次编译和运行程序都需要在`javac`和`java`命令之前添加 `/usr/local/jdk1.8.0/`.。为了避免每次都输入，你可以将该路径添加到PATH变量。具体步骤根据你运行的不通shell终端有所区别。

`**Class names, 'HelloWorldApp', are only accepted if annotation processing is explicitly requested**`

如果你碰到这个错误，说明你在执行`javac`的时候忘了写`.java`后缀。记住，命令应该是 `javac HelloWorldApp.java`而不是`javac HelloWorldApp`.

**语法错误(全平台)Syntax Errors (All Platforms)**

如果你程序的某部份书写错误，编译器可能回抛出一个*syntax error*,语法错误。提示信息通常回显示错误的类型，错误出现的行数，该行的代码，以及该行出现错误的位置。线面的错误是因为语句结尾遗漏了一个`;`引起的。

```
testing.java:14: `;' expected.
System.out.println("Input has " + count + " chars.")
                                                     ^
1 error
```

有时候编译器猜不出的意图就会打印出定义不清晰的错误信息或者多行错误信如果错误于多行代码有关的话。例如，如下代码片段遗漏了符号`;`：

```java
while (System.in.read() != -1)
    count++
System.out.println("Input has " + count + " chars."); 
```

当处理这段代码的时候，编译器会报出两个错误信息:

```
testing.java:13: Invalid type expression.
        count++
                 ^
testing.java:14: Invalid declaration.
    System.out.println("Input has " + count + " chars.");
                      ^
2 errors
```

编译器报出两个错误信息是因为当编译器处理到`count++`时，编译器的状态显示目前正处在表达式的中间。没有`;`符号，编译器无法确定当前语句是否完成。

如果你看到任何编译错误，说明你的程序没有编译成功，没由生成.class文件。仔细的检查你的代码，修复检测到的错误，在重新试一次。

**语义错误Semantic Errors**

除了验证你程序的语法规范，编译器也能检查其他基本内容的正确性。例如，当你使用一个未初始化的变量时，编译器也会发出警告:

```
testing.java:13: Variable count may not have been initialized.
        count++
        ^
testing.java:14: Variable count may not have been initialized.
    System.out.println("Input has " + count + " chars.");
                                       ^
2 errors
```

重复一遍你的程序没有编译成功，没由生成.class文件。仔细的检查你的代码，修复检测到的错误，在重新试一次。

## [运行时错误Runtime Problems]()

**Windows常见错误**

`Exception in thread "main" java.lang.NoClassDefFoundError: HelloWorldApp`

如果碰到这个问题，`java`启动器找不到字节码文件,`HelloWorldApp.class`.`java`默认从你的当前文件家查找`.class`文件，因此如果你的`.class`文件不在当前文件加下，需要改变当前文件路径。例如你的`.class`文件在`C:\java`下，先输入如下命令并按下回车:

```shell
cd c:\java
```

提示信息显示为 `C:\java>`如果你输入 `dir`命令,你应该可以看到你的 `.java`和 `.class`文件.现在是输入 `java HelloWorldApp` 再试一次.

如果仍然有问题，你可能改变了你的CLASSPATH变量，如果有必要的话执行如下命令*clobbering*重置你的classpath变量。

```shell
set CLASSPATH=
```



重新输入 `java HelloWorldApp` . 如果你程序可以运行，你不得不重设你的CLASSPATH变量。你可以在参考JDK8安装教程中的[配置环境变量](https://docs.oracle.com/javase/8/docs/technotes/guides/install/windows_jdk_install.html#BABGDJFH).  CLASSPATH 变量也使用同样的方法来配置

`**Could not find or load main class HelloWorldApp.class**`

另一个新手常见的错误是，试图用`java`运行`.class`文件。列入用 `java HelloWorldApp.class` 代替 `java HelloWorldApp`. 记住，这里输入的参数应该是**类名**而不是`.class`文件的文件名。

`Exception in thread "main" java.lang.NoSuchMethodError: main`

JVM要求你执行的类包含一个`main`方法来启动你的应用。 [深入了解”Hello World“应用程序](http://docs.oracle.com/javase/tutorial/getStarted/application/index.html) 详细讨论了 `main` 方法.

**UNIX系统错误信息**

`Exception in thread "main" java.lang.NoClassDefFoundError: HelloWorldApp`

如果碰到这个问题，`java`启动器找不到字节码文件,`HelloWorldApp.class`.`java`默认从你的当前文件家查找`.class`文件，因此如果你的`.class`文件不在当前文件加下，需要改变当前文件路径。例如你的`.class`文件在`/home/jdoe/java`下，先输入如下命令并按下回车

```
cd /home/jdoe/java

```

如果输入 `pwd` , 你可以看到 `/home/jdoe/java`. 如果输入 `ls` 你应该能看到你的 `.java` 和 `.class` 文件。现在是输入 `java HelloWorldApp` 再试一次.

如果仍然有问题，你可能改变了你的CLASSPATH变量，如果有必要的话执行如下命令*clobbering*重置你的classpath变量。

```shell
unset CLASSPATH
```

重新输入 `java HelloWorldApp` . 如果你程序可以运行，你不得不重设你的CLASSPATH变量。你可以在参考JDK8安装教程中的[配置环境变量](https://docs.oracle.com/javase/8/docs/technotes/guides/install/windows_jdk_install.html#BABGDJFH).  CLASSPATH 变量也使用同样的方法来配置

`**Exception in thread "main" java.lang.NoClassDefFoundError: HelloWorldApp/class**`

另一个新手常见的错误是，试图用`java`运行`.class`文件。列入用 `java HelloWorldApp.class` 代替 `java HelloWorldApp`. 记住，这里输入的参数应该是**类名**而不是`.class`文件的文件名。

`Exception in thread "main" java.lang.NoSuchMethodError: main`

JVM要求你执行的类包含一个`main`方法来启动你的应用。 [深入了解”Hello World“应用程序](http://docs.oracle.com/javase/tutorial/getStarted/application/index.html) 详细讨论了 `main` 方法

**Applet or Java Web Start Application Is Blocked**

如果你通过浏览器运行一个应用，出现应用被锁定的安全警告，检查以下项目:

* 检查你的应用是否为运行环境设置了正确的JAR file manifest(JAR文件清单)。权限属性是必须的。在NetBeans项目中，你可以展开项目文件夹双击manifest.mf。
* 检查应用是否已经为有效的证书签名以及证书是否位于签名证书密钥库。
* 如果你运行的是一个本地小程序，只是通过Web服务器测试。在Java Control Panel （Java控制面板）的Security安全页面进行设置，也可以把你的应用添加到例外名单中。