---
title: Java 学习指南_学习Java：基础-类-类的成员
date: 2017-10-20 11:21:59
tags: 
- java
- tutorial
- 教程
- class
- 类
- Class Members
- 类的成员
categories:
- java
keywords:
- java
- 教程
- tutorial
- class
- 类
- Class Members
- 类的成员
---

# 理解类的成员

在本节中，我们讨论使用`static`关键字来创建属于类的字段和方法，而不是示例的成员。

## 类变量Class Variables

当一定数量的对象按照同样的类模板创建时，它们每一个都拥有不同的*实例变量* 的副本。在自行车类`Bicycle` 中，实例变量为 `cadence`, `gear`, 和`speed`. 没一个自行车 `Bicycle` 对象的这些变量都有着不同的值，存储在不同的内存位置中。

有时候，你想要有对所有对象都相同的变量。这就要使用`static`修饰符来完成。声明时带有`static`修饰符的字段/域叫做 *静态域* 或者 *类变量*  （*static fields* or *class variables*）.

它们是域类相关联的而不是任一个对象。每一个类的实例共享类变量，存储在一个固定的内存位置。任一个对象都可以改变类变量的值，并且类变量也可以在不创建任何类的实例的情况下进行操作。

例如，假设你想创建一定数量的自行 `Bicycle`对象并且为每一个分配一个序号，第一个对象的开始值为1. 这个ID数字对域每一个对象都都是唯一的因此是一个实例变量。同时，你需要你个字段来跟踪已经创建了多少`Bicycle`对象，这样你可以直到为下一个对象分配什么ID。这么一个字段并不是域任一个单独的对象关联的，而是对于整个类。这样你就需一个类变量， `numberOfBicycles`,就像相面的例子:

```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
        
    // add an instance variable for the object ID
    private int id;
    
    // add a class variable for the
    // number of Bicycle objects instantiated
    private static int numberOfBicycles = 0;
        ...
}
```

类变量是通过它自身的类名来引用的，例如

```java
Bicycle.numberOfBicycles
```

这样就可以清晰的直到它们是类变量.

------

注意: 你同样可以使用一个对象来引用静态域如下 

```java
myBike.numberOfBicycles
```

但是并不鼓励这么做，因为这样做并不能清除的表明它们是类变量。

------

你可以使用 `Bicycle` 构造器来为每一个实例变量`id`赋值，并增加类变量 `numberOfBicycles` 的值:

```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
    private int id;
    private static int numberOfBicycles = 0;
        
    public Bicycle(int startCadence, int startSpeed, int startGear){
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;

        // increment number of Bicycles
        // and assign ID number
        id = ++numberOfBicycles;
    }

    // new method to return the ID instance variable
    public int getID() {
        return id;
    }
        ...
}
```

## 类的方法Class Methods

Java编程语言支持静态变量的同时也支持静态方法。静态方法，在定义时使用`static`修饰符，应该通过类名类直接调用，而无需创建一个类的实例，例如:

```java
ClassName.methodName(args)
```

------

注意:  你同样可以使用一个对象来引用静态方法如下 

```java
instanceName.methodName(args)
```

但是并不鼓励这么做，因为这样做并不能清除的表明它们是类的方法。

------

静态方法一个常用的地方使用来方位静态域。例如，我们可以为`Bicycle`类添加一个静态方法来访问 `numberOfBicycles` 静态域:

```java
public static int getNumberOfBicycles() {
    return numberOfBicycles;
}
```



并不是所有的静态方法，静态域 与实例变量实例方法的 结合使用都使允许的:

- 实例方法可以直接访问实例变量与实例方法。
- 实例方法可以直接调用类变量以及类方法。Instance methods can access class variables and class methods directly.
- 类方法可以直接方法类变量与类方法。Class methods can access class variables and class methods directly.
- 类方法**不能**直接访问实例变量与实例方法——它们必须通过一个对象来引用。同样，类方法不能使用`this`关键字，因为这里的`this`不能指向任何实例。

## 常量Constants

`static`修饰符，经常与`final`修饰符结合使用，用来定义常量。`final`修饰符表明这个字段的值不能改变。

例如，下面的变量声明了一个常量`PI`，值为pi（圆周率：圆的周长与直径的比值）的近似值：

```java
static final double PI = 3.141592653589793;
```

这种方式定义的常量不能重新赋值，如果你尝试这么做的话就会得到一个编译时错误。按照管理，常量的命名单词用大写字母拼写，如果名字包含了多个单词，使用下划线`_`分割.

------

注意:如果一个基本数据类型或者字符串被定义为常量并且值在编译时已经确知，编译器将所有代码中出现的所有常量名替换为它的值。这叫做 编译时常量 *compile-time constant*. 如果你使用的常量外部世界值发生改变（例如，立法确认pi的值应该为3.975）,那么你就需要重新编译所以用到这个常量的类来获取当前固定值。

------

## 自行车`Bicycle` 类

经过所有的改变之后 `Bicycle` 现在如下所示:

```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
        
    private int id;
    
    private static int numberOfBicycles = 0;

        
    public Bicycle(int startCadence,
                   int startSpeed,
                   int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;

        id = ++numberOfBicycles;
    }

    public int getID() {
        return id;
    }

    public static int getNumberOfBicycles() {
        return numberOfBicycles;
    }

    public int getCadence() {
        return cadence;
    }
        
    public void setCadence(int newValue) {
        cadence = newValue;
    }
        
    public int getGear(){
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