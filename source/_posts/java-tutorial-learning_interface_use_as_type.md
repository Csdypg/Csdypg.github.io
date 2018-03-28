---
title: Java 学习指南_学习Java：使用接口作为一个类型
date: 2018-03-26 17:40:59
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

# 使用接口作为一个类型

当你定义一个新的接口，你定义了一个新的引用数据类型。使用其他引用类型名的地方都可以使用接口名。如果你定义的一个接口的引用类型变量，赋值必须为实现了这个接口的类的实例。

下面的例子，定义了一个找到size比较大的对象的方法，对象可以是任何实现了`Relatable`接口的类的实例：

```java
public Object findLargest(Object object1, Object object2) {
   Relatable obj1 = (Relatable)object1;
   Relatable obj2 = (Relatable)object2;
   if ((obj1).isLargerThan(obj2) > 0)
      return object1;
   else 
      return object2;
}
```

通过转换 `object1` 类型为 `Relatable` 类型, 就可以调用其 `isLargerThan` 方法.

如果你注意到很多的类都实现了 `Relatable`接口，任何这些类的实例都可以通过方法 `findLargest()`进行比较—只要他们是同一个类的对象.同样,他们都可以通过下面的方法进行比较:

```java
public Object findSmallest(Object object1, Object object2) {
   Relatable obj1 = (Relatable)object1;
   Relatable obj2 = (Relatable)object2;
   if ((obj1).isLargerThan(obj2) < 0)
      return object1;
   else 
      return object2;
}

public boolean isEqual(Object object1, Object object2) {
   Relatable obj1 = (Relatable)object1;
   Relatable obj2 = (Relatable)object2;
   if ( (obj1).isLargerThan(obj2) == 0)
      return true;
   else 
      return false;
}
```

这个方法对所有的"relatable"对象都有效,不管他们的继承成了什么，当他们实现了 `Relatable`接口,他们同时可以是谈么本身（或者其父类）的类型， 也可以是一个 `Relatable` 类型.这就给了他们多重继承的优势，他们同时可以表现出其父类和接口的行为.