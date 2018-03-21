---
title: Java 学习指南_学习Java：基础-类-使用对象
date: 2017-10-13 15:00:59
tags: 
- java
- tutorial
- 教程
- 对象
- Object
- 垃圾回收
- gc
- Garbage Collector
categories:
- java
keywords:
- java
- 教程
- tutorial
- 对象
- Object
- 垃圾回收
- gc
- Garbage Collector
---

# 使用对象

一旦你创建了一个对象，你可能想要用它做一些事情。你可能需要使用这个对象的字段/成员变量中的一个，改变它，或者调用的方法来执行某些行为。

## 引用对象的字段/属性/成员变量

对象的字段通过它的名称来访问。你必须使用一个无歧义的名称。

你可能会在一个类中使用简单的名称。例如，我们可以在`Rectangle`类中加上一个语句。来打印它的 `width` 和 `height`:

```java
System.out.println("Width and height are: " + width + ", " + height);
```

在这种情况下，`width` 和 `height`是简单的名称.在对象的类之外的代码中必须使用一个对象的引用或者表达式，紧接着一个点`.`操作符，紧接着字段的名称来引用，例如

```java
objectReference.fieldName
```

例如， `CreateObjectDemo` 类中的代码是 `Rectangle` 类之外的代码.所以`Rectangle` 对象 `rectOne`的字段 `origin`, `width`, `height`的引用必须分别使用 `rectOne.origin`, `rectOne.width`, 以及 `rectOne.height`这样的名字.以下代码使用了两个这样的名称来展示`rectOne`的 `width`以及`height`字段:

```java
System.out.println("Width of rectOne: "  + rectOne.width);
System.out.println("Height of rectOne: " + rectOne.height);
```

如果在以上代码中尝试使用简单的名字如 `width` ， `height` 并不会起作用，这两字段只存在于一个对象之中——并且会导致编译错误。

接着，程序使用相似的代码展示了`rectTwo`对象的信息。同类型的对象有他们自己的实例变量的副本。这样的话，每一个`Rectangle`对象都有名为 `origin`, `width`, 和 `height`等字段.当你通过一个引用变量访问其实例变量时，你引用的时那个特定的对象的字段。两个对象 `rectOne` 和 `rectTwo` ，在 `CreateObjectDemo` 有着不同的 `origin`, `width`, 和 `height` 字段.

为了方位一个实例变量，你可以使用命名的引用对象，就像之前的例子一样，或者你也可以使用任何返回该对象引用的表达式。重申一下，`new`操作符返回一个对象的引用。因此使用new的返回值来访问其实例变量:

```java
int height = new Rectangle().height;
```

这个语句使用new创建 `Rectangle` 对象并且直接获取了他的高度。实质上，这个语句运算出一个`Rectangle`的默认高度。注意这个语句过后，程序中不在持有已经创建的`Rectangle`的对象引用，因为程序没有将这个引用存储在任何地方。这个对象没有别引用，并且它的资源时空间的将被Java虚拟机回收。

## 调用一个对象的方法

你也会用一个对象引用调用一个对象的方法。在对象应用的名称后面加上方法名，中间使用一个`.`操作符链接。同样，在闭合的`()`提供方法所需的参数，如果方法不需要参数，使用空的`()`.

```
objectReference.methodName(argumentList);
```

或者:

```
objectReference.methodName();
```

 `Rectangle` 类有两个方法: `getArea()`用来计算矩形的面积， `move()` 方法来盖面正方形的源点。下面是程序调用这两个方法的代码:

```java
System.out.println("Area of rectOne: " + rectOne.getArea());
...
rectTwo.move(40, 72);
```

第一行语句，调用了 `rectOne`的 `getArea()` 方法并且显示了结果。第二行移动了 `rectTwo` 因为 `move()` 方法为对象的 `origin.x` 和 `origin.y`赋了新的值.

对于实例变量，对象引用必须时一个指向对象的引用。你可以使用一个变量名，同样可以使用一个返回对象引用的表达式。`new`操作符返回一个对象引用，因此你可以直接使用这个表达式的返回值来调用对象的方法:

```java
new Rectangle(100, 50).getArea()
```

表达式 `new Rectangle(100, 50)`返回一个 `Rectangle` 对象的引用。正如展示的一样，可以使用`.`符号来调用这个新的`Rectangle`的`getArea()`方法。

有些方法，例如 `getArea()`,返回一个值。对于返回值的方法，你在在表达式中使用方法调用。你可以将返回值赋值给变量，可以用来做决定，或者控制循环语句。这段代码将 `getArea()` 的返回值赋值给变量 `areaOfRectangle`:

```java
int areaOfRectangle = new Rectangle(100, 50).getArea();
```

记住，调用一个特定对象的方法就好像向这个对象发送信息。本例中，调用的`getArea()`方法构造器返回的rectangle对象的方法。

## 垃圾回收The Garbage Collector

有些面向对象的编程语言要求你持续跟踪你创建的所有对象，并且在不需要的时候明确的销毁它们。明确的管理内存是及其乏味并且容易出错的过程。Java编程语言允许你创建任意数量你想要的对象（当然受限与你的系统处理能力），并且无需担心何时销毁。Java 运行时环境确定对象不会再被使用的时候会删除对象。这个过程叫做`垃圾回收`*garbage collection*.

当一个对象没有引用指向它的时候，是符合垃圾回收条件的。或者，你可以通过将一个变量设置为特殊的值`null`，显式的清理一个对象引用。记住，一个程序可能对一个对象有非常多的引用;一个对象被垃圾回收前必须清理所有指向它的引用。

Java运行时环境有一个垃圾回收器，周期性的释放被没有引用指向的对象占用的内存。垃圾回收器确定时机正确时，会自动完成其工作。