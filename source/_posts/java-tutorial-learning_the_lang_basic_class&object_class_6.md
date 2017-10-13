---
title: Java 学习指南_学习Java：基础-类-对象
date: 2017-10-13 09:00:59
tags: 
- java
- tutorial
- 教程
- 对象
- Object
- constructor
categories:
- java
keywords:
- java
- 教程
- tutorial
- 对象
- Object
---

# 对象

一个特定的Java程序创建许多对象，就像你学过的，通过方法调用进行交出。通过对象的交互，一个程序可以处理各种各样的任务，诸如实现一个GUI（用户交互界面），运行一个动画，或者通过网路发送和接受信息。一旦一个对象完成了被创建的过程，它的资源可以被其他对象循环使用。

下面有一个小程序，叫做 [`CreateObjectDemo`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/CreateObjectDemo.java), 创建了三个对下给你，一个点对象 [`Point`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/Point.java) 和两个矩形 [`Rectangle`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/Rectangle.java) 对象. 你会需要三个资源文件来完成这个程序.

```java
public class CreateObjectDemo {

    public static void main(String[] args) {
		
        // Declare and create a point object and two rectangle objects.
        Point originOne = new Point(23, 94);
        Rectangle rectOne = new Rectangle(originOne, 100, 200);
        Rectangle rectTwo = new Rectangle(50, 100);
		
        // display rectOne's width, height, and area
        System.out.println("Width of rectOne: " + rectOne.width);
        System.out.println("Height of rectOne: " + rectOne.height);
        System.out.println("Area of rectOne: " + rectOne.getArea());
		
        // set rectTwo's position
        rectTwo.origin = originOne;
		
        // display rectTwo's position
        System.out.println("X Position of rectTwo: " + rectTwo.origin.x);
        System.out.println("Y Position of rectTwo: " + rectTwo.origin.y);
		
        // move rectTwo and display its new position
        rectTwo.move(40, 72);
        System.out.println("X Position of rectTwo: " + rectTwo.origin.x);
        System.out.println("Y Position of rectTwo: " + rectTwo.origin.y);
    }
}
```

这个程序创建，操作了三个不同的随想并显示了其信息，以下为输出情况:

```java
Width of rectOne: 100
Height of rectOne: 200
Area of rectOne: 20000
X Position of rectTwo: 23
Y Position of rectTwo: 94
X Position of rectTwo: 40
Y Position of rectTwo: 72
```

接下来的三部分使用上面的例子描述了一个对象在程序中的生命周期。通过特们，你可以学习到如何在你的程序中创建和使用对象。同样可以学习到系统在对象的生命周期结束后如何清理它们。