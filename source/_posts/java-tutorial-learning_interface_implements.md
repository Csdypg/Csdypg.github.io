---
title: Java 学习指南_学习Java：实现接口
date: 2018-03-26 16:21:59
tags: 
- java
- tutorial
- 教程
- interface
- 接口
categories:
- java
keywords:
- java
- 教程
- tutorial
- interface
- 接口
---

# 实现一个接口Implementing an Interface

定义一个实现接口的类，需要在类定义时包含 `implements` ，一个类可以事多个接口所以，`implements` 关键字后可以跟一个逗号分隔的实现接口的列表. 按照惯例, `implements` 引用跟随在 `extends` 扩展引用之后如果有的话.

## 一个简单的借口，相关联的Relatable

考虑定义一个比较对象size的借口.

```
public interface Relatable {
        
    // this (object calling isLargerThan)
    // and other must be instances of 
    // the same class returns 1, 0, -1 
    // if this is greater than, 
    // equal to, or less than other
    public int isLargerThan(Relatable other);
}
```

如果你想过要比较相似的对象的size，不管他们是什么类型的对象，可实例化类必须要实现这个接口 `Relatable`.

任何类都可以实现这个`Relatable`接口，如果有方法可以比较实例化对象的相对size.例如字符串，可以通过字符数来比较，例如书本，可以通过页数来比较，例如学生，可以通过体重类比较等。例如平面几何图形，面积会是一个好的选择。(参考，下面的 `RectanglePlus`类),立体形状，则可以通过体积来比较.所有的这些类都可以实现 `isLargerThan()`方法.

如果你知道一个类实现了 `Relatable`接口,那么你就可以比较这个类的实例化对象的size.

## 实现Relatable接口

一下是矩形类 `Rectangle`，在 [Creating Objects](https://docs.oracle.com/javase/tutorial/java/javaOO/objectcreation.html) 出现过, 重写这个类来实现 `Relatable`接口.

```java
public class RectanglePlus 
    implements Relatable {
    public int width = 0;
    public int height = 0;
    public Point origin;

    // four constructors
    public RectanglePlus() {
        origin = new Point(0, 0);
    }
    public RectanglePlus(Point p) {
        origin = p;
    }
    public RectanglePlus(int w, int h) {
        origin = new Point(0, 0);
        width = w;
        height = h;
    }
    public RectanglePlus(Point p, int w, int h) {
        origin = p;
        width = w;
        height = h;
    }

    // a method for moving the rectangle
    public void move(int x, int y) {
        origin.x = x;
        origin.y = y;
    }

    // a method for computing
    // the area of the rectangle
    public int getArea() {
        return width * height;
    }
    
    // a method required to implement
    // the Relatable interface
    public int isLargerThan(Relatable other) {
        RectanglePlus otherRect 
            = (RectanglePlus)other;
        if (this.getArea() < otherRect.getArea())
            return -1;
        else if (this.getArea() > otherRect.getArea())
            return 1;
        else
            return 0;               
    }
}
```

因为矩形类 `RectanglePlus` 实现了 `Relatable`,任一两个 `RectanglePlus` 对象的size事可以比较的.

------

**注意**:`isLargerThan`方法，是在 `Relatable`接口中定义的，接口参数类型为`Relatable`.将`other`装换为 `RectanglePlus`实例，类型转换告诉编译器`other`对象本身是什么类型，直接在`other`对象上调用`other.getArea()`方法将会编译失败。

------