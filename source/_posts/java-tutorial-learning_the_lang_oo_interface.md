---
title: Java 学习指南_学习Java：O_O什么是Interface接口？
date: 2017-07-03 10:38:59
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

# 什么是Interface接口？

就像你之前学到的，对象通过暴露的方法定义与外界的交互。方法构成了对象与外部世界的*interface*接口；你电视机前面的按钮，是你和电视塑料盒子背后电子线路的交互接口。当按下“电源”按钮来打开和关闭电视机。

同样的方式，接口是一组相关的空方法。一个自行车的行为，如果总结为一个接口，其表现形式如下:

<!--more-->

```java
interface Bicycle {

    //  wheel revolutions per minute
    void changeCadence(int newValue);

    void changeGear(int newValue);

    void speedUp(int increment);

    void applyBrakes(int decrement);
}
```

实现这个接口，你的类名需要改变（某一特殊类型的自行车，例如`ACMEBicycle`），并且你需要在定义类的时候适用`implements`关键字:

```java
class ACMEBicycle implements Bicycle {

    int cadence = 0;
    int speed = 0;
    int gear = 1;

   // The compiler will now require that methods
   // changeCadence, changeGear, speedUp, and applyBrakes
   // all be implemented. Compilation will fail if those
   // methods are missing from this class.

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

实现一个接口可以使一个类对于其应该提供的行为方法更加规范。接口规定了类与外部世界交互的约定，并且这个约定在编译器是强制执行的。如果你的类声明实现了某一个接口，所有在接口中定义的方法都必须出现在这个类的源代码中，否则就无法编译成功。

------

注意:

事实上，为了成功编译上述`ACMEBicycle`类，你必须在所有的实现方法添加`public`关键字。原因将在随后的课程[类与对象]()，[接口与继承]()中讲到。

------