---
title: Java 学习指南_学习Java：基础-类-方法返回值
date: 2017-10-18 11:00:59
tags: 
- java
- tutorial
- 教程
- class
- 类
- method
- return
categories:
- java
keywords:
- java
- 教程
- tutorial
- class
- 类
- 类
- method
- return
---

# 从方法返回值

当以下情况出现时方法会返回到调用他的代码处：

- 完成方法中的所有语句
- 执行到一个 `return`语句
- 或者抛出一个异常(稍后讨论)

哪一个先出现都会返回。

在方法声明时你会定义方法的返回类型。在方法体中，使用 `return`语句来返回值。

声明`void`返回类型的方法不会返回值，不一定要包含一个`return`语句,但是可以这么做。这种情况下，一个`return`语句可以用程序分支跳出一个控制流程块并且退出方法，使用方法如下:

```java
return;
```

如果你你视图在声明了`void`的方法里返回一个值，将会出现编译错误。

任何没有声明`void`的方法都必须包含一个`return`语句和对应的返回值,如下：

```java
return returnValue;
```

返回值的数据类型必须与方法声明的返回类型匹配;你不能在生命的`boolean`返回类型的方法里返回一个整形。

在对象一节中讨论的 `Rectangle` [`Rectangle`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/Rectangle.java) 类的 `getArea()`方法返回一个integer:

```java
    // a method for computing the area of the rectangle
    public int getArea() {
        return width * height;
    }
```

方法返回的值为表达式 `width*height`的计算结果.

 `getArea` 方法返回了一个基本数据类型. 方法同样可以返回引用类型的数据.例如 ，在一个操纵 `Bicycle` 对象的类里，我们可能会看到这样的方法:

```java
public Bicycle seeWhosFastest(Bicycle myBike, Bicycle yourBike,
                              Environment env) {
    Bicycle fastest;
    // code to calculate which bike is 
    // faster, given each bike's gear 
    // and cadence and given the 
    // environment (terrain and wind)
    return fastest;
}
```

## 返回类型为一个类或者接口Returning a Class or Interface

如果你对本章节感到费解，可以先跳过，学习完[接口与继承]()课程之后返回来学习。

当一个方法使用一个类名作为它的返回类型，例如 `whosFastest`这样,返回对象的类型必须使这个类或者这个类的子类。假设你有继承关系， `ImaginaryNumber` 是 `java.lang.Number`类的子类,  `java.lang.Number`类是`Object`的子类, 如下图所示.

![The class hierarchy for ImaginaryNumber](http://docs.oracle.com/javase/tutorial/figures/java/classes-hierarchy.gif)

 `ImaginaryNumber`类的继承关系

现在假设你有一个返回类型为`Number`的方法声明:

```java
public Number returnANumber() {
    ...
}
```

 `returnANumber` 方法可以返回 `ImaginaryNumber` 但是不能返回 `Object`. `ImaginaryNumber` 是一个 `Number` 因为他是 `Number`的子类. 但是`Object`并不一定是一个 `Number` — 它可能是一个 `String` 或者其他的类型.

你可以通过定义一个方法的返回类型为源方法返回类型的子类来覆盖一个方法，如下：

```java
public ImaginaryNumber returnANumber() {
    ...
}
```

这种技术叫做 *covariant return type协变返回类型*,意味着返回类型允许用某一个类和其子类来区分。

------

**注意**:你同样可以声明接口为返回类型。这种情况下，你返回对象的类型必须是对应接口的实现类。

------

