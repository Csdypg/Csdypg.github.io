---
title: Java 学习指南_学习Java：基础-类-this关键字
date: 2017-10-18 13:54:59
tags: 
- java
- tutorial
- 教程
- class
- 类
- this
categories:
- java
keywords:
- java
- 教程
- tutorial
- class
- 类
- 类
- this
---

# 使用this关键字

在一个实例方法或者是构造器中，`this`关键字指向*当前对象**current object*—被调用了方法或者构造器的对象。你可以通过`this`关键字在实例方法或者构造器中引用当前对象的任何成员。

##  `this` 与 Field

通常使用`this`关键字的原因是field被方法或构造器的参数遮蔽.例如,  `Point`可以这样写

```java
public class Point {
    public int x = 0;
    public int y = 0;
        
    //constructor
    public Point(int a, int b) {
        x = a;
        y = b;
    }
}
```

同样也可以这样写：

```java
public class Point {
    public int x = 0;
    public int y = 0;
        
    //constructor
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

构造器的每一个参数遮蔽对象的一个filed字段/属性--方法内**x** 是构造器第一参数的一本局部副本.为了引用 `Point` 的 **x**字段, 构造器必须使用 `this.x`.

##  `this` 与构造器 Constructor

在一个构造器内，你同样可以使用`this`关键字来调用用一个类中的其他构造器。这样做叫作*explicit constructor invocation**显示的构造函数调用*.下面是一个 `Rectangle` 类,与对象一节中实现方法不同.

```java
public class Rectangle {
    private int x, y;
    private int width, height;
        
    public Rectangle() {
        this(0, 0, 1, 1);
    }
    public Rectangle(int width, int height) {
        this(0, 0, width, height);
    }
    public Rectangle(int x, int y, int width, int height) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }
    ...
}
```

这个类包含一系列的构造器.每一个构造器初始化初始化矩形的一些成员变量.构造器为没有提供初始化参数的成员变量设置一个默认值。例如。无参构造器在坐标(0,0)处创建一个1X1的矩形。这个两个参数的构造其调用了四个参数的构造器，传递里宽高参数并且使用了(0,0)坐标。就像之前一样，编译器决定去调用哪一个构造器，基于参数的数量以及类型。

如果存在这种调用，对其他构造器的调用必须出现在构造器中的第一行。