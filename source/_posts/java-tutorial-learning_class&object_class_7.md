---
title: Java 学习指南_学习Java：基础-类-创建对象
date: 2017-10-13 13:00:59
tags: 
- java
- tutorial
- 教程
- 创建对象
- Creating Object
categories:
- java
keywords:
- java
- 教程
- tutorial
- 创建对象
- Creating Object
---

# 创建对象

如你所知，类提供了对象的蓝图/模板；你可以通过类创建对象。下面的每一个语句取自 [`CreateObjectDemo`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/CreateObjectDemo.java) ，都创建了一个对象并将它赋值给一个变量:

```java
Point originOne = new Point(23, 94);
Rectangle rectOne = new Rectangle(originOne, 100, 200);
Rectangle rectTwo = new Rectangle(50, 100);
```

第一行创建了一个 [`Point`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/Point.java) 类的对象,第二行及第三行创建了 [`Rectangle`](http://docs.oracle.com/javase/tutorial/java/javaOO/examples/Rectangle.java) 类的对象.

每一行语句都包含了三部分，详情如下：

1. **声明Declaration**: 首先定义了变量对应的数据类型和变量名.
2. **实例化Instantiation**:  `new`  关键字时Java的创建（实例化）对象操作符.
3. **初始化Initialization**:  `new` 操作符接下来调用一个构造方法，构造方法初始化这个新的对象.

<!--more -->

## 定义一个引用对象的变量

首先你，学到了如何声明一个变量，这样写:

```java
type name;// 类型 名称
```

这么做就告诉了编译器你将使用`name`指向/引用类型为`type`的数据。作为基本数据变量，这个声明同样会为变量预备/分配适当数量的内存。

你同样可以定义一个引用类型的变量，例如:

```java
Point originOne;
```

如果你向这样声明 `originOne`变量,它的值时不确定的，直到你个对象确实创建并赋值给它。简单的声明一个引用类型的变量并不会创建一个对象。因此，你需要使用`new`操作符，就像上一节讲的。在你的代码中使用它之前你必须创建一个对象并赋值给它。不然的话，就会出现一个编译错误。

在现在的这种情况下，当前的变量时么有引用对象的，示例如下（变量名，`originOne`,没有指向任何东西）:

![originOne is null.](http://docs.oracle.com/javase/tutorial/figures/java/objects-null.gif)

## 实例化一个类Instantiating a Class

 `new`操作符实例化一个 类，通过为新的对象分配一块内存并返回指向这块内存的引用。`new`操作符同样调用了类的构造方法。

------

**注意**: 单词 "instantiating a class" 实例化一个类与 "creating an object."创建一个对象意思一样。当你创建你对象的时候，你创建一个类的实例，或者说实例化一个类。

------

 `new` 操作符要求一个单独的后缀参数:一个构造函数的调用.构造函数名提供了需要实例化的类名。

 `new`操作符返回一个它创建的对象的引用。这个引用通常赋值给一个对应类型的变量。就像这样:

```java
Point originOne = new Point(23, 94);
```

`new`操作符返回的引用并不一样非要复制给一个变量，它也可以直接在一个表达式中使用。例如:

```java
int height = new Rectangle().height;
```

下一节还会讨论这个语句。

## 初始化一个对象Initializing an Object

以下为`Point` 类的代码:

```java
public class Point {
    public int x = 0;
    public int y = 0;
    //constructor
    public Point(int a, int b) {
        x = a;
        y = b;
    }
}
```

这个类包含唯一的构造方法。你很容易识别构造方法，因为它的名字与类名一样并且没有返回类型。`Point`类的构造方法需要两个`integer`参数 `(int a, int b)`.下面的语句提供了23和94作为这两个参数的值：

```java
Point originOne = new Point(23, 94);
```

语句执行的结果可以用以下图例展示:

![originOne now points to a Point object.](http://docs.oracle.com/javase/tutorial/figures/java/objects-oneRef.gif)

下面是矩形`Rectangle`类的代码，包含了四个够高方法:

```java
public class Rectangle {
    public int width = 0;
    public int height = 0;
    public Point origin;

    // four constructors
    public Rectangle() {
        origin = new Point(0, 0);
    }
    public Rectangle(Point p) {
        origin = p;
    }
    public Rectangle(int w, int h) {
        origin = new Point(0, 0);
        width = w;
        height = h;
    }
    public Rectangle(Point p, int w, int h) {
        origin = p;
        width = w;
        height = h;
    }

    // a method for moving the rectangle
    public void move(int x, int y) {
        origin.x = x;
        origin.y = y;
    }

    // a method for computing the area of the rectangle
    public int getArea() {
        return width * height;
    }
}

```

每一个构造方法让你使用基本数据类型或者引用类型为矩形的定点，宽，高提供初始值。如果你个类有多个构造方法，它们必须有不同 的方法签名。Java编译器根据参数的类型和数量来区分构造函数。当Java编译其碰到虾米那的代码，它直到去调用要求`Point`,以及两个整数参数的构造方法:

```java
Rectangle rectOne = new Rectangle(originOne, 100, 200);
```

这个方法调用初始化`origin`为`originOne`,同样设置`width`为100，`height`为200。现在有两个引用指向同一个 `Point object`—一个对象可以有多个引用指向它，就像下面的图例所示:

![Now the rectangle's origin variable also points to the Point.](http://docs.oracle.com/javase/tutorial/figures/java/objects-multipleRefs.gif)

接下来的几行代码调用了要求两个`integer`整形参数的构造方法，为`width`和`height`提供了初始值。观察这个构造方法的代码，你会发现它创建了一个新的`Point`对象，其`x`,`y`的值初始化为0:

```java
Rectangle rectTwo = new Rectangle(50, 100);
```

`Rectangle` 构造方法使用了下面的语句，没有用到参数，因此叫做*无参构造器*， *no-argument constructor*:

```java
Rectangle rect = new Rectangle();
```

所有的类都至少有一个构造器。如果类没有像是的提供构造其，Java编译器为自动提供一个无参构造器，叫做*默认构造器* *default constructor*. 这个默认构造器调用父类的无参构造器，如果这个类没有其他父类则调用`Object`的构造器。如果这个父类没有构造器（`Object`有构造器），编译器将会拒绝这个程序。