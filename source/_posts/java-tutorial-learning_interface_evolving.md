---
title: Java 学习指南_学习Java：进化接口
date: 2018-03-27 16:40:59
tags: 
- java
- tutorial
- 教程
- interface
- 接口
categories:
- java
keywords:
- java
- 教程
- tutorial
- interface
- 接口
---

# 进化接口 Interfaces

考虑一下你之前开发的一个名为 `DoIt`的接口:

```java
public interface DoIt {
   void doSomething(int i, double x);
   int doSomethingElse(String s);
}
```

假设，过了一段时间以后，你想要在接口中添加一个方法，那么接口会变成下面的样子:

```java
public interface DoIt {

   void doSomething(int i, double x);
   int doSomethingElse(String s);
   boolean didItWork(int i, double x, String s);
   
}
```

如果要做这个改变，那么所有实现了旧的`DoIt`接口的类都不能再使用了，因为他们没有实现接口的所有方法。依赖这个接口的开发者将会大声抗议。

试着在开始就预见你的借口的所有用处并做完整的定义。如果你想要在接口中添加额外的方法，可以有几种选择。你可以创建一个 `DoItPlus` 接口来扩展 `DoIt`:

```java
public interface DoItPlus extends DoIt {

   boolean didItWork(int i, double x, String s);
   
}
```

现在你代码的用户可以选择继续使用旧的接口，或者升级到新的接口。

同样，也可以定义新的方法为默认方法 [default methods](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html). 下面的列子定义了一个名为`didItWork`:

```java
public interface DoIt {

   void doSomething(int i, double x);
   int doSomethingElse(String s);
   default boolean didItWork(int i, double x, String s) {
       // Method body 
   }
   
}
```

注意，你必须为默认方法提供一个实现。你也可以在现存从接口中定义一个新的静态方法 [static methods](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html#static)。实现了这个接口的用户可以通过默认方法或者静态方法类增强他们的功能，而不需要为适应新增的方法修改和重新编译所有的类。