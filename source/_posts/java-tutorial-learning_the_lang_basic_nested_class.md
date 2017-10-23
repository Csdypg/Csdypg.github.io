---
title: Java 学习指南_学习Java：基础-嵌套类
date: 2017-10-23 17:00:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- nested class
- 嵌套类
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- nested class
- 嵌套类	
---

# 嵌套类

java编程语言允许你在一个类的内部定义类。这样的类叫做*嵌套类**nested class*,示例如下：

```java
class OuterClass {
    ...
    class NestedClass {
        ...
    }
}
```

------

**术语Terminology**: 嵌套类分为两类，静态和非静态.声明为`static`的嵌套类叫做 *static nested classes*静态嵌套类。非静态嵌套类叫做*inner classes*内部类。

------

```java
class OuterClass {
    ...
    static class StaticNestedClass {
        ...
    }
    class InnerClass {
        ...
    }
}
```

嵌套类是其所在类的成员。非静态嵌套类（内部类）具有访问所在类的其他成员的访问权限，即使是私有的成员。静态内部类没有访问其所在类的其他成员的权限。作为`OuterClass`的成员，一个嵌套类可以被声明为`private`,`public`,`protected`或者包级私有（package private 默认）。（重申以下外部类只能 被定义为`public` 或者 包级私有）。

## 为什么使用嵌套类?



驱使使用嵌套类的原因包括以下几个：

- **它是为只在一个地方使用的类的逻辑分类的一种方法It is a way of logically grouping classes that are only used in one place**: 如果一个类支只对另外一个类有用，那么把它嵌入那个类中是两者保持在一起是符合逻辑的。嵌套进这样的*辅助类* 是他们的包结构更加的合理化。
- **增加封装性It increases encapsulation**:  考虑两个顶级的类，A和B，如果B需要访问A中原本声明为`private`的成员。通过将B吟唱在A类内，A的成员可以被定义为`private`私有，并且B可以访问它们，B本身也可以对于外部世界隐藏。
- **是代码更加易读和易于管理It can lead to more readable and maintainable code**: 将小类嵌套与顶级类中是代码更接近它使用的地方。

## 静态嵌套类Static Nested Classes

与类方法和类变量一样，静态嵌套类是与其外部类相关联的。并且像静态类方法一样，一个静态嵌套类不能直接引用类中定义的实例变量和实例方法：只能通过一个对象的引用来使用。

------

**注意**:  静态嵌套类与其外部类或者其他类的实例成员交互 与它的顶级类一样。实际上，一个静态嵌套类与与顶积累表现一样，只不过可以方便的嵌入其他定义类，构建包更加便利。

static nested class interacts with the instance members of its outer class (and other classes) just like any other top-level class. In effect, a static nested class is behaviorally a top-level class that has been nested in another top-level class for packaging convenience.

------

静态嵌套类通过其所有类的类名来访问例如：

```java
OuterClass.StaticNestedClass
```

如果需要创建一个静态嵌套类的对象，使用如下的语法:

```java
OuterClass.StaticNestedClass nestedObject =
     new OuterClass.StaticNestedClass();
```

## 内部类

与实例方法和实例变量一样，一个内部类是与其所有类的实例相关联的，并且可以直接访问其实例方法和字段/域。 同样，因为内部类是域实例向关联的，所以它本身不能定义任何的静态成员。

内部类的实例对象存在与外部类实例的内部，观察下面的类:

```java
class OuterClass {
    ...
    class InnerClass {
        ...
    }
}

```

一个内部类 `InnerClass` 的实例只能存在于一个`OuterClass`类的实例内部，并且可以直接访问该实例的方法和字段/域。

实例化一个内部类，你必须现实里话外部类。然后，通过外部类的对象创建内部对象，语法如下:

```java
OuterClass.InnerClass innerObject = outerObject.new InnerClass();
```

内部类还有两种特殊情况：[局部类]() 和 [匿名内部类]().: [local classes](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html) and [anonymous classes](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html).

## 遮蔽[Shadowing]()

如果在一个特定的范围内（例如在一个内部类或者是方法顶以内）定义一个类型（例如成员变量或者是参数名称）与闭合区域内（例如外部类的闭合区域内）的另外一个声明有相同的名字，那么这个声明就会遮蔽闭合区域内的声明。你不能指通过名字引用被遮蔽的声明。下面是一个例子， [`ShadowTest`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/ShadowTest.java), 演示了这个现象:

```java
public class ShadowTest {

    public int x = 0;

    class FirstLevel {

        public int x = 1;

        void methodInFirstLevel(int x) {
            System.out.println("x = " + x);
            System.out.println("this.x = " + this.x);
            System.out.println("ShadowTest.this.x = " + ShadowTest.this.x);
        }
    }

    public static void main(String... args) {
        ShadowTest st = new ShadowTest();
        ShadowTest.FirstLevel fl = st.new FirstLevel();
        fl.methodInFirstLevel(23);
    }
}
```

以下为这个例子的输出:

```java
x = 23
this.x = 1
ShadowTest.this.x = 0
```

这个例子定义了三个变量名字都为`x`: 类`ShadowTest`的成员变量，内部类`FirstLevel`的成员变量，以及方法`methodInFirstLevel`的参数。方法`methodInFirstLevel`的参数`x`遮蔽了内部类`FirstLevel`的变量x。因此，当你在方法`methodInFirstLevel`中使用`x`时，引用的时方法的参数。为了引用内部类`FirstLevel`的成员变量，使用`this`挂件子来代表笔和空间:

```java
System.out.println("this.x = " + this.x);
```

为了引用更大的闭合范围内的成员变量，需要使用它所属于的类名。例如，下面的语句，在`methodInFirstLevel`方法中引用了`ShadowTest`类的成员变量:

```java
System.out.println("ShadowTest.this.x = " + ShadowTest.this.x);
```

## 序列化[Serialization]()

内部类的序列化，包括局部类和匿名内部类，强力不建议。当Java编译器编译确定的结构，例如内部类，会创建合成构造 *synthetic constructs*; 包括类，方法，字段，以及其他的结构，这些结构在源码中并没有对应的相应的构造。合成构造能使使Java编译器在不更换JVM的情况下实现新的Java语言特性。然而合成构造可能因为不同固定Java编译器实现而有区别，意味着`.class`文件可能因为不同的实现也有所不同。因此，如果你用不同的JRE实现序列化和反序列化一个内部类的时候可能会出现各种各样的复杂问题。

参考 [Implicit and Synthetic Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html#implcit_and_synthetic)  隐式合成参数， [Obtaining Names of Method Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html) 获取方法参数名 章节，来获取内部类编译时生成合成构造的更多信息。