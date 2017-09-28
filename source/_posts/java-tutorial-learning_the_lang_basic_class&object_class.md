---
title: Java 学习指南_学习Java：基础-类
date: 2017-09-27 12:00:59
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

# 类

在标题为 [面向对象编程概念 ](http://docs.oracle.com/javase/tutorial/java/concepts/index.html)的课程中介绍面向对象编程概念时使用了一个bicycle自行车类作为例子，包含赛车，山地车作为子类。这里有一个简单的代码示例作为`Bicycle`类的一种可能实现，让你对类的定义有一个大致的了解。接下来的课程中将会一步一步的复习和解释类的定义，现在先不要关注太多的细节。

```java
public class Bicycle {
        
    // the Bicycle class has
    // three fields
    public int cadence;
    public int gear;
    public int speed;
        
    // the Bicycle class has
    // one constructor
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;
    }
        
    // the Bicycle class has
    // four methods
    public void setCadence(int newValue) {
        cadence = newValue;
    }
        
    public void setGear(int newValue) {
        gear = newValue;
    }
        
    public void applyBrake(int decrement) {
        speed -= decrement;
    }
        
    public void speedUp(int increment) {
        speed += increment;
    }
        
}
```

定义一i个`Bicycle`类的子类`MountainBike`l类可能如下所示：

```java
public class MountainBike extends Bicycle {
        
    // the MountainBike subclass has
    // one field
    public int seatHeight;

    // the MountainBike subclass has
    // one constructor
    public MountainBike(int startHeight, int startCadence,
                        int startSpeed, int startGear) {
        super(startCadence, startSpeed, startGear);
        seatHeight = startHeight;
    }   
        
    // the MountainBike subclass has
    // one method
    public void setHeight(int newValue) {
        seatHeight = newValue;
    }   

}
```

`MountainBike` 类继承了自行车类的所有fields字段/域 以及方法，并且添加了field `seatHeight`，以及一个设置它的方法（山地车拥有可以根据地形调整高度的座位）。 