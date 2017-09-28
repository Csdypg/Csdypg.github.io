---
title: Java 学习指南_学习Java：基础-类-构造方法
date: 2017-09-28 15:00:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- 构造方法
- constructor
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- 构造方法
- constructor
---

# 为你的类提供构造方法

类包含构造方法，可以被调用而根据类的蓝本创建对象。构造方法声明同普通的方法一样—只不过命名与类名相同且没有返回类型。例如，`Bicycle`类的构造方法：

```java
public Bicycle(int startCadence, int startSpeed, int startGear) {
    gear = startGear;
    cadence = startCadence;
    speed = startSpeed;
}
```

如果要创建一个名为`myBike`的对象，适用`new`操作符调用构造方法：

```java
Bicycle myBike = new Bicycle(30, 0, 8);
```

`new Bicycle(30, 0, 8)`为对象在内存中分配空间并初始化成员变量。

 `Bicycle` 类只有一个构造方法，它也可以有其他更多构造方法，包括无参的构造方法:

```java
public Bicycle() {
    gear = 1;
    cadence = 10;
    speed = 0;
}
```

`Bicycle yourBike = new Bicycle();` 调用无惨构造方法创建一个名为`yourBike`的`Bicycle`类对象。

两个构造方法都可以在`Bicycle`类中定义因为它们有不同的参数列表。同方法一样，Java平台根据参数列表的数量以及类型区分不同的构造方法。不能定义有同样数量和类型参数列表的构造方法，因为平台无法区分它们。这么左会引起编译错误。

你可以不为类提供任何构造方法，当时这么左的时候必须小心。编译器为没有构造方法的类自动提供一个默认的无参构造函数。这个默认的构造方法会调用其父类的无参构造方法。这种情况下，如果父类没有无参构造方法编译器将会抱怨，因此你这么做之前必检查父类确实有无参构造器。如果你的类没有明确的父类，它有一个隐藏的父类`Object`,`Object`拥有无参构造方法。

你可自己调用父类的构造函数。本课开始的`MountainBike`类就这么做了，在接口与继承课程中还会详细讨论。

你可以使用限定修饰符来控制那些其他类可以访问构造方法。

------

**注意:**如果你不能调用`Myclass`的构造方法，就无法直接创建`Myclass`类的对象。

------

