---
title: Java 学习指南_学习Java：基础-类-定义成员变量
date: 2017-09-28 12:00:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- 成员变量
- Member Variables
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- 成员变量
- Member Variables	
---

# 定义成员变量

变量由以下几种:

- 类的成员变量-叫做域/字段.
- 方法代码块中的变量-叫做局部变量。
- 方法定义中的变量-叫做参数。

`Bicycle`类使用以下几行定义了它的成员变量:

```java
public int cadence;
public int gear;
public int speed;
```

成员变量的定义由三部分组成，按照顺序入下:

1. 零个或更多限定修饰符，例如`public`或者`private`.
2. 字段的类型.
3. 字段个名称.

 `Bicycle`类的成员变量名字为 `cadence`, `gear`, 以及`speed` 并且都是`int` 类型的。`public`关键字表明了这些时公有，然和可以访问该类的对象都可以访问这些成员变量。

## 限定修饰符

第一个（最左边的）限定修饰符使你控制其他类可以访问成员变量的权限。现在，仅仅关注`public`和`private`。其他的限定修饰符后面会讨论.

- `public` 修饰符—本字段可以被所有类访问.
- `private` 修饰符—本字段只可以在本类中访问.

为了体现封装特性，通常设置成员变量为私有`private`。意味着它们只能在`Bicycle`类中被直接访问。然而，我们仍然需要访问这些值。这可以通过添加获取字段值的公有方法间接实现:

```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
        
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;
    }
        
    public int getCadence() {
        return cadence;
    }
        
    public void setCadence(int newValue) {
        cadence = newValue;
    }
        
    public int getGear() {
        return gear;
    }
        
    public void setGear(int newValue) {
        gear = newValue;
    }
        
    public int getSpeed() {
        return speed;
    }
        
    public void applyBrake(int decrement) {
        speed -= decrement;
    }
        
    public void speedUp(int increment) {
        speed += increment;
    }
}
```

## 类型

所有的变量都必须由一个类型。你可以使用基本数据类型例如`int`,`float`,`boolean`,等等。或者你可以使用引用类型，例如字符串，数组，对象。

## 变量名

所有的变量，无论时成员变量，局部变量或者参数，都遵循同样的命名规则与约定，这在之前的语言基础课程变量命名中讲过。[Variables—Naming](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html#naming).

在本课中，注意这些命名规则同样适用与方法名和类名，除了以下两点：

- 类名的首字母需要大写the first letter of a class name should be capitalized, and
- 方法名的首个单词应该为动词the first (or only) word in a method name should be a verb.