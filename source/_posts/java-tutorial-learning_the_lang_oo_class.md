---
title: Java 学习指南_Java语言基础：O_O什么是Class类？
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

# 什么是Class类？

在现实世界中，你会发现许多同一种类物体的许多不同个体。出于同样的构造和模型可能由上千种自行车存在。每一辆自行车都通过同样的设置或者设计图制造因此也包含同样的组件。在面向对象中，我们说你的自行车是*class of the objects* 对象类 bicycles的一个*instance*实例。类就是用来创建不同对象实例的蓝图/模板。

<!--more-->

下面的Bicycle类是自行车的一种可能实现类:

```java
   class Bicycle {

       int cadence = 0;
       int speed = 0;
       int gear = 1;

       void changeCadence(int newValue) {
            cadence = newValue;
       }

       void changeGear(int newValue) {
            gear = newValue;
       }

       void speedUp(int increment) {
            speed = speed + increment;   
       }

       void applyBrakes(int decrement) {
            speed = speed - decrement;
       }

       void printStates() {
            System.out.println("cadence:" +
                cadence + " speed:" + 
                speed + " gear:" + gear);
       }
   }
```



对你来说Java编程语言的语法看起来可能比较陌生，但是这个类的设计是基于之前讨论的自行车对象。字段/属性`cadence`，`speed`以及`gear`代表了对象的状态，方法`changeCadence`,`chageGear`,`speedUp` 规定了它与外界的交互。

你可能注意到`Bicycle` 类不包含`main` 方法，那是因为这并不是一个完整的应用。他只是一个可能用于应用的自行车的模板。创建以及使用自行车对象的责任属于你应用程序的其他部分。

以下`BicycleDemo`类创建了两个独立的`Bicycle`对象并且调用了他们的方法：

   ```java
   class BicycleDemo {
       public static void main(String[] args) {

           // Create two different 
           // Bicycle objects
           Bicycle bike1 = new Bicycle();
           Bicycle bike2 = new Bicycle();

           // Invoke methods on 
           // those objects
           bike1.changeCadence(50);
           bike1.speedUp(10);
           bike1.changeGear(2);
           bike1.printStates();

           bike2.changeCadence(50);
           bike2.speedUp(10);
           bike2.changeGear(2);
           bike2.changeCadence(40);
           bike2.speedUp(10);
           bike2.changeGear(3);
           bike2.printStates();
       }
   }
   ```

   这个测试的输出打印出了两个自行车最终的踏板节奏，速度，挡位：

   ```
   cadence:50 speed:10 gear:2
   cadence:40 speed:20 gear:3
   ```