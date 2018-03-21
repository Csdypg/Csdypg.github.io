---
title: Java 学习指南_学习Java：基础-类-向方法和构造函数传递信息
date: 2017-10-13 09:00:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- 构造方法
- 方法
- 参数信息
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
- 方法
- 参数信息
---

# 向方法和构造函数传递信息

方法或者构造函数的声明，定义了它所需的参数的数量和类型。例如，下面的方法用来基于单款额度，利率，贷款期数，以及未来值来计算家庭贷款每月还款额:

```java
public double computePayment(
                  double loanAmt,
                  double rate,
                  double futureValue,
                  int numPeriods) {
    double interest = rate / 100.0;
    double partial1 = Math.pow((1 + interest), 
                    - numPeriods);
    double denominator = (1 - partial1) / interest;
    double answer = (-loanAmt / denominator)
                    - ((futureValue * partial1) / denominator);
    return answer;
}
```

这个方法有四个参数：贷款金额，利率，未来值，以及带款期数。前三个参数双精度浮点数，第四个参数是一个整数，这些*参数变量*在方法体里使用，运行时将接纳传递进来的*参数*的值。

------

**注意**:*参数变量*Parameters 指的是方法定义使的变量列表. *参数Arguments*是指方法被调用时传递进来的确切的值。当以调用一个方法，传递参数必须与定义的参数列表类型和顺序一致。 

------

<!-- more -->

## 参数类型

你可以在方法或者构造函数中使用任何类型的数据。包括基本数据类型，例如doubles,floats,integers,就像你在`computePayment()`方法里看到的一样，也报过引用类型的数据，例如对象，数组。下面的列子接受一个数组作为参数，在这个例子中，方法创建了一个多边形`Polygon`对象并且根据一`Point`点对象数组在初始化（假设这些`Point`点对象代表了一个x,y坐标）:

```java
public Polygon polygonFrom(Point[] corners) {
    // method body goes here
}
```

------

**注意**:  如果你想要将一个方法传递给另一个，那么请使用lambda表达式 [lambda expression](http://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 或者是方法引用 [method reference](http://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html).

------

## 任意数量的参数

你可以使用你个叫做**可变参数**的的结构来向方法传递任意数量的参数。当你不指导到底有几个特定类型的参数需要被传递进方法时，可以时用**可变参数**.它是手动创建数组参数的一种快捷方法（上一个方法就可以用可变参数而不用数组）.

使用可变参数，在数据类型后面加上一个省略号（三个点`...`）,然后空格，然后参数名。方法传进任何数量的该类型参数都可以调用，甚至不传也可以。

```java
public Polygon polygonFrom(Point... corners) {
    int numberOfSides = corners.length;
    double squareOfSide1, lengthOfSide1;
    squareOfSide1 = (corners[1].x - corners[0].x)
                     * (corners[1].x - corners[0].x) 
                     + (corners[1].y - corners[0].y)
                     * (corners[1].y - corners[0].y);
    lengthOfSide1 = Math.sqrt(squareOfSide1);

    // more method body code follows that creates and returns a 
    // polygon connecting the Points
}
```

你会发现，在方法内，`corners`被视作一个数组。方法被调用时既可以传入一个数组，亦可传入一系列单数，不管怎样代码体里都会将其视作一个数组来处理。

你通常会在在打印方法中见到可变参数；例如，`printf`方法:

```java
public PrintStream printf(String format, Object... args)
```

允许你打印任意数量的变量，可以按照如下方法调用:

```java
System.out.printf("%s: %d, %s%n", name, idnum, address);
```

也可以这样调用

```
System.out.printf("%s: %d, %s, %s, %s%n", name, idnum, address, phone, email);

```

或者使用其他不同数量参数.

## 参数名称

当你为一个方法或者构造函数定义参数是，将提供一个名称。这个名称在参数体里使用来代表传递进来的参数。参数名称在在其作用范围内必须是唯一的。不能与方法或构造函数的其他参数同名，也不能与方法内的局部函数同名。

参数名可以与类的字段/成员变量名称相同。在这种情况下，这个参数被成为这个字段的*shadow影子变量*。影子变量将会是代码不易读并且通常知识在构造方法或者是为某个字段设置值的方法中使用，参考下面的`Circle`类以及它的`setOrigin`方法:

```java
public class Circle {
    private int x, y, radius;
    public void setOrigin(int x, int y) {
        ...
    }
}
```

 `Circle` 类有三个字段/成员变量：`x,y,radius`,`setOrigin`设置圆心方法有两个参数，每一个都与字段名一样。因此在方法体内部使用`x`, `y`指的是参数，而不是字段本身。为了访问字段本身，一必须使用一个可以辨别的名字。这将会在标题为"使用`this`关键字的"课程部分讨论。

## 传递基本数据类型的参数Passing Primitive Data Type Arguments

基本数据类型参数，如`int`,`double`,直接将值传递进方法。意味着参数的值的变化值在方法内存在。当方法结束后，参数就不存在了，它的任何变化也将丢失，一下为示例:

```java
public class PassPrimitiveByValue {

    public static void main(String[] args) {
           
        int x = 3;
           
        // invoke passMethod() with 
        // x as argument
        passMethod(x);
           
        // print x to see if its 
        // value has changed
        System.out.println("After invoking passMethod, x = " + x);
           
    }
        
    // change parameter in passMethod()
    public static void passMethod(int p) {
        p = 10;
    }
}
```

运行代码，输出如下:

```java
After invoking passMethod, x = 3
```

## 传递引用类型的参数Passing Reference Data Type Arguments

引用类型的参数，例如对象，同样是将其值传入方法，意味这方法一旦结束，被传递进来的引用仍然指向之前的对象。**然而**，如果用对应的访问权限，对象的字段值可能被改变。

例如，考虑在任意一个类中建立一个移动`Circle`对象的方法:

```java
public void moveCircle(Circle circle, int deltaX, int deltaY) {
    // code to move origin of circle to x+deltaX, y+deltaY
    circle.setX(circle.getX() + deltaX);
    circle.setY(circle.getY() + deltaY);
        
    // code to assign a new reference to circle
    circle = new Circle(0, 0);
}
```

用以下参数调用这个方法:

```
moveCircle(myCircle, 23, 56)

```

在方法内, `circle` 初始化时指向 `myCircle`. 方法改变了circle应用的对象（这里指，`myCircle`）的坐标值，分别增加23，和56,当方法返回后这些改变将持久化。

然后将circle的引用指向一个新的`Circle`对象，该对象`x=y=0`，这次重新赋值并没有保存，因为传递进来的参数`myCircle`的引用不会改变。在方法内，`circle`指向的对象发生了改变，但是当发发结束后，`myCircle`仍人指向方法调用前的对象。