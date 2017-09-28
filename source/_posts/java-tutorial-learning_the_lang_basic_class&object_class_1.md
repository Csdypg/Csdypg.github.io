---
title: Java 学习指南_学习Java：基础-类-声明类
date: 2017-09-28 10:00:59
tags: 
- java
- tutorial
- 教程
- 类
- class
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class	
---

# 声明类

你已经看到的类按照下面的方式定义：

```java
class MyClass {
    // field, constructor, and 
    // method declarations
}
```

这就是*类的声明*。类体class body(两个花括号之内的区域)包含了用于对象生命周期中由类创建时所需的所有代码：用于初始化一个对象的构造函数，用来提供类以及其实例对象的状态的字段/域，以及实现了类和其实例对象行为的方法。

之前是课程声明了一个最基本的类 。只包含了声明类所必须的组件。你可以为类提供更多信息，例如在开始定义类的时候声明类的父类，以及是否实现了那些接口等等。例如,

```java
class MyClass extends MySuperClass implements YourInterface {
    // field, constructor, and
    // method declarations
}
```

意味着类`MyClass`是`MySuperClass` 的子类并且它实现了`YourInterface`接口。

你同样可以在最开始的比方增加限定修饰符*public*或者`private`-因此你会发现定义类的起始行可以变得相当复杂。限定修饰符*public*和*private*定义了其他类可以访问`Myclass`的什么内容，将会在本科后续内容讨论。关于接口和继承的课程会解释如何以及为什么使用*extends*以及*implements*关键字类定义类。现在你不需要担心这些复杂的问题。

通常情况的，类的声明包含了以下部分，按照顺序排列为：

1. 限定修饰符public,private以及后续你会碰到的其他内容。
2. 类名，按照约定需要大写首字母
3. 类的父类，前置一个*extends*关键字。一个类只可以扩展自一个父类。
4. 由逗号分割的实现接口的列表，前置一个*implements*关键字。一个类可以*implement*实现多个接口。
5. 类体body，由{},花括号包围。