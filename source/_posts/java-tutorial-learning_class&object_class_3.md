---
title: Java 学习指南_学习Java：基础-类-定义成员变量
date: 2017-09-28 11:30:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- 方法
- method
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- 方法
- method
---

# 定义方法

下面时一个典型的定义方法的例子:

```java
public double calculateAnswer(double wingSpan, int numberOfEngines,
                              double length, double grossTons) {
    //do the calculation here
}
```

定义方法必须的元素只有方法返回类型，方法名，已对小括号`()`以及`{}`包围的方法体。

更加常见的方法定义包含六个部分，按照顺序依次是:

1. 限定修饰符—例如`public`,`private`以及后面会学到的其他修饰符。
2. 返回类型—定义方法返回的数据类型，如果方法不返回值标记为`void`.
3. 方法名—定义字段名的规则同样适用用方法名，约定稍有不同，方法名的第一个词一般动词等。
4. 在小括号内的参数列表—由小括号包围，逗号分割，参数前标明其数据类型，如果没有参数必须适用一个空的小括号。
5. 异常列表—之后的课程会讲到。
6. 方法体，由花括号`{}`包围—方法的代码，局部变量声明都包含在内。

限定修饰符，返回类型，参数在本节的后续内容中学习。异常将在之后的课程学习。

------

**定义:**方法定义的两部分内容定义为*方法签名* *method signature*—方法名以及参数类型.

------

上面声明的方法签名如下:

```java
calculateAnswer(double, int, double, double)
```

## 方法命名

尽管方法名可以是任何的合法标识符，但是按照惯例约定方法命名很严格。按照惯例，方法名应该是一个小写的动词或者以小写的动词开头的多个单词，后续单词可以是形容词名词等。在多个单词的方法命名时，第二个单词及之后的单词首字母需要大写（首字母小写驼峰命名）.以下为一些例子:

```java
run
runFast
getBackground
getFinalData
compareTo
setX
isEmpty
```

通常，在同一类中的方法命名是位移的。不过，因为*方法重载*，方法名可以重复。

## 方法重载

Java编程语言支持方法重载，Java可以本剧方法的不同*方法签名*method signatures辨别同名的不同方法。以为这同一个类中可以有不同参数列表（接口与继承课程中将会介绍一些限定条件）的同名方法。

假设你的类可以适用书写不同类型的数据(字符串，整数等等)并且包含了一个可以画出不同数据类型的方法。为每一种数据画法起一个新的方法名将会非常麻烦—例如`drawString`,`drawInteger`,`drawFloat`等等。在Java编程语言中，你可以对这些方法适用同样的名称，只需要为每个方法传入不同的参数别表。这样，画出数据类可以定义四个名为`draw`的类，每一个都有不同的参数列表。

```java
public class DataArtist {
    ...
    public void draw(String s) {
        ...
    }
    public void draw(int i) {
        ...
    }
    public void draw(double f) {
        ...
    }
    public void draw(int i, double f) {
        ...
    }
}
```

重载的方法因传入参数的数量及数据类型而不同。在上面的示例代码中 `draw(String s)` 与 `draw(int i)` 是有区别且位移的方法因为他们需要不同的参数类型。你不能在同一个类中定义名字相同参数数量与类型都相同的方法，因为编译器无法分辨。

编译器在区分方法是并不考虑返回类型，所以不能定义两个方法签名相同但是返回类型不同的方法。

------

**注意**: 方法重载不应该滥用，因为它们会使代码的可读性变差。

------

