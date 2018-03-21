---
title: Java 学习指南_学习Java：基础-嵌套类问题与联系
date: 2018-03-19 17:51:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- 嵌套类
- 局部类
- 匿名类
- Lambda
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- 嵌套类
- 局部类
- 匿名类
- Lambda
---

# 嵌套类：问题与练习

## 问题

1. **问题**: 程序 [`Problem.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/Problem.java) 不能编译，你需要怎么做才能让它成功编译?为什么?

2. 使用 [`Box`](https://docs.oracle.com/javase/8/docs/api/javax/swing/Box.html) 类(在 `javax.swing` 包中)的Java API文档 帮助你问答如下问题 .

   1. **问题**: `Box` 定义了什么静态嵌套类?

   2. **问题**:  `Box` 定义了什么内部类?

   3. **问题**:  `Box`的内部类的父类是什么?

   4. **问题**:  `Box`的哪一个嵌套类你可以在任何一个类中使用?

   5. **问题**: 如何创建一个 `Box`的`Filler嵌套类的实例?

## 练习

1. **练习**: 获取文件 [`Class1.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/Class1.java). 编译并运行 `Class1`. 输出是什么?

2. **练习**: 下面的联系涉及到修改 [`DataStructure.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/DataStructure.java)类, 该类在 [Inner Class Example](https://docs.oracle.com/javase/tutorial/java/javaOO/innerclasses.html) 中有讨论.

   1. 定义一个名为 `print(DataStructureIterator iterator)`的方法.用一个类`EvenIterator`类的实例调用这个方法实现`printEven`方法的功能。


   2. 调用方法 `print(DataStructureIterator iterator)` 来打印奇数索引的元素.使用一个匿名类作为方法的参数，代替接口 `DataStructureIterator`的实例.


   3. 定义一个方法 `print(java.util.Function<Integer, Boolean> iterator)` 实现 `print(DataStructureIterator iterator)`相同的功能.通过一个lambda表达式参数调用该方法实现打印出偶数下标的元素，重新用lambda表达式参数调用并实现打印出奇数下标的元素。


4.    定义两个方法可以是如下语句分别打印偶数下标对应的值和技术下标对应的值:

      ```java
      DataStructure ds = new DataStructure()
      // ...
      ds.print(DataStructure::isEvenIndex);
      ds.print(DataStructure::isOddIndex);
      ```



# 嵌套类：问题与练习答案


<!-- more -->
## 问题答案

1. **问题**: 程序 [`Problem.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/Problem.java) 不能编译，你需要怎么做才能让它成功编译?为什么?

   **答案**: 删除`Inner`类的`static`关键字修饰。静态嵌套类不能访问外部类的实例成员参考 [`ProblemSolved.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/ProblemSolved.java).

2. 使用 [`Box`](https://docs.oracle.com/javase/8/docs/api/javax/swing/Box.html) 类(在 `javax.swing` 包中)的Java API文档 帮助你问答如下问题 .

   1. **问题**: `Box` 定义了什么静态嵌套类?

      **答案**: `Box.Filler`

   2. **问题**:  `Box` 定义了什么内部类?

      **答案**: `Box.AccessibleBox`

   3. **问题**:  `Box`的内部类的父类是什么?

      **答案**: `[java.awt.]Container.AccessibleAWTContainer`

   4. **问题**:  `Box`的哪一个嵌套类你可以在任何一个类中使用?

      **答案**: `Box.Filler`

   5. **问题**: 如何创建一个 `Box`的`Filler嵌套类的实例?

      **答案**: `new Box.Filler(minDimension, prefDimension, maxDimension)`

## 练习答案

1. **练习**: 获取文件 [`Class1.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/Class1.java). 编译并运行 `Class1`. 输出是什么?

   **答案**: `InnerClass1: getString invoked.InnerClass1: getAnotherString invoked.`

2. **练习**: 下面的联系涉及到修改 [`DataStructure.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/DataStructure.java)类, 该类在 [Inner Class Example](https://docs.oracle.com/javase/tutorial/java/javaOO/innerclasses.html) 中有讨论.

   1. 定义一个名为 `print(DataStructureIterator iterator)`的方法.用一个类`EvenIterator`类的实例调用这个方法实现`printEven`方法的功能。

      **提示**: 一下语句在`main`方法中奖不能通过编译:

      ```java
      DataStructure ds = new DataStructure();
      ds.print(new EvenIterator());
      ```

      编译器产生错误信息 "non-static variable this cannot be referenced from a static context—非京台的变量不能再静态上下文中引用"，表达式 `new EvenIterator()`会产生这个错误. 类 `EvenIterator` 是一个内部类，非静态.意味着你必须在外部类的一个实例中创建它的实例, `DataStructure`数据结构.

      你尅定义一个方法 `DataStructure` 来创建和返回`EvenIterator`的实例.

   2. 调用方法 `print(DataStructureIterator iterator)` 来打印奇数索引的元素.使用一个匿名类作为方法的参数，代替接口 `DataStructureIterator`的实例.

      **提示**:你无法访问 `DataStructure`之外的私有成员 `SIZE` 和 `arrayOfInts` ，意味着你不能从匿名类访问定义在其之外的私用成员.

   3. 定义一个方法 `print(java.util.Function<Integer, Boolean> iterator)` 实现 `print(DataStructureIterator iterator)`相同的功能.通过一个lambda表达式参数调用该方法实现打印出偶数下标的元素，重新用lambda表达式参数调用并实现打印出奇数下标的元素。

      **提示**: 在 `print` 方法中,你可以通过`for`语句遍历`arrayOfInts`.对于每一个下标志，调用`function.apply`方法。如果方法返回`True`，打印出下表对应的元素值。

      为了实现打印偶数下标的值,你可以定义特定的Lambda表达式实现 `Boolean Function.apply(Integer t)`方法.表达式接受一个 `Integer` 参数 (下标)并且返回一个布尔值 (`Boolean.TRUE` 如果下标是偶数, 否则返回`Boolean.FALSE` ).

   4. 定义两个方法可以是如下语句分别打印偶数下标对应的值和技术下标对应的值:

      ```java
      DataStructure ds = new DataStructure()
      // ...
      ds.print(DataStructure::isEvenIndex);
      ds.print(DataStructure::isOddIndex);
      ```

      **提示**: 在类中 `DataStructure` 创建两个名为 `isEvenIndex` 和 `isOddIndex` 的方法，两个方法拥有同样的参数列和且返回类型，同抽象方法 `Boolean Function<Integer, Boolean>.apply(Integer t)`一致. 这两个方法同样接受 `Integer` 参数 (下标志) 并且返回 `Boolean` 值.

   **答案**: 参考文件[`DataStructure.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/DataStructure.java).