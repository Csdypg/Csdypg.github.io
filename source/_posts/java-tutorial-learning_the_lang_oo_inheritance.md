---
title: Java 学习指南_Java语言基础：O_O什么是Inheritance继承？
date: 2017-07-02 15:38:59
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

# 什么是Inheritance继承？

不同种类的对象可能催在一定的共性。例如：山地车，公路车，tandem bikes双人车都具有自行车的共有属性（当前速度，当前踏板节奏，当前挡位）。然而定义额外的特征是的特们有区别：双人车由两个座位和两个车把；有的山地车有附加的车链子，提供更低的挡位.

<!--more-->

面向对象编程允许类通过其他类*inherit*继承通用的属性和方法。在本例中，Bicycle现在变为`MountainBike`，`RoadBike`，以及`TandemBike`的*父类*。在Java编程语言中，一个类只允许有一个直接父类，每一个父类可以有无限数量的*子类*。

![A diagram of classes in a hierarchy.](http://docs.oracle.com/javase/tutorial/figures/java/concepts-bikeHierarchy.gif)

继承自自行类车的类.

创建一个子类的语法非常简单。在定义类的时候使用extends关键字后面跟着要继承的类名：

```java
class MountainBike extends Bicycle {

    // new fields and methods defining 
    // a mountain bike would go here

}
```

这样就赋予了`MountainBike`类所有`Bicycle`类的属性和方法，这样就允许你的代码只专注与那些子类特有的特性。同样使你子类的代码更加易读。然而你必须注意在父类定义中加入适当的文档注释，因为这些代码不会出现在人一个子类的源文件中。