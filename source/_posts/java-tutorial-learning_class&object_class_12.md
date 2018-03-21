---
title: Java 学习指南_学习Java：基础-类-访问控制
date: 2017-10-18 13:54:59
tags: 
- java
- tutorial
- 教程
- class
- 类
- Controlling Access
- 访问控制
categories:
- java
keywords:
- java
- 教程
- tutorial
- class
- 类
- Controlling Access
- 访问控制
---

# 类成员的访问控制

访问等级限定词确定了其他类是否可以使用一个特定的field字段或者方法.有两种访问等级的控制:

- 类的访问等级—公有`public`, 或者包级权限 *package-private* (没有显式声明).
- 成员访问等级—公有`public`,私有 `private`, 保护`protected`, or包级权限 *package-private* (没有显示声明).

一个类的声明可以不包含限定符`public`，`public`共有类对于所有类都是可见的。如果一个类没有限定修饰符(默认等级为，包级权限),只对它所在的包内可见。（包命名了一组相关联的类,后面的课程将会学习）.

对类的成员的访问等级，你同样可以使用`public`限定修饰符或者无修饰符(包级权限package-private),无限定修饰符时与类的情况一样并且意义也一样。对于成员来说，仍然有两种额外的访问限定修饰符：`private`与`protected`.`private`限定符表的名该成员私有，只能在本类之内访问。`protected`修饰符表明该成员可以被同一个包里的类访问(与默认情况，包级权限一样)，并且也可以被其他包中该类的子类所访问。

以下表格展示了不同限定修饰符所确定的成员访问权限。

| Modifier    | Class | Package | Subclass | World |
| ----------- | ----- | ------- | -------- | ----- |
| `public`    | Y     | Y       | Y        | Y     |
| `protected` | Y     | Y       | Y        | N     |
| no modifier | Y     | Y       | N        | N     |
| `private`   | Y     | N       | N        | N     |

第一列数据列展示了类对他资深成员的访问权限。如你所见，一个类总是可以访问它的成员。第二个数据列展示类同一个包内的其他类（不考虑类为其子类的情况）对本类成员的访问权限。第三个数据列展示本类所在包之外的子类对本类成员的访问权限。第四列展示了是否所有的类都对成员具有访问权限。

访问权限通过两种方式起作做。首先，当你使用来自其他资源的类时，例如Java平台的类，访问权限确定了那些类的成员你的类可以调用。第二，当你写一个类时，你需却决定你的每一个类的成员变量或者方法的访问权限。

当我们来看一系列类以及访问权限如何影响可见性。下面的图标展示了本例中的四个类以及它们之间的关系。

![Classes and Packages of the Example Used to Illustrate Access Levels](http://docs.oracle.com/javase/tutorial/figures/java/classes-access.gif)

展示访问权限的类与包的图例Classes and Packages of the Example Used to Illustrate Access Levels

以下表格展示了不同限定修饰符下`Alpha`类的成员对于其他类的可见性。

| Modifier    | Alpha | Beta | Alphasub | Gamma |
| ----------- | ----- | ---- | -------- | ----- |
| `public`    | Y     | Y    | Y        | Y     |
| `protected` | Y     | Y    | Y        | N     |
| no modifier | Y     | Y    | N        | N     |
| `private`   | Y     | N    | N        | N     |

------

选择访问权限的提示:

如果其他的程序员使用你的类，你想要确保不因滥用而出现错误。访问权限可以帮助你做这些.

- 对特定的成员使用最严格的访问权限。使用 `private` 除非你有更好的理由不这么做。
- 避免使用`public ` 除非为常量。(本教程的很多例子中都使用了public fields。这么做可以简单的解释一些知识点，但是不推荐在产品的代码中这么做)。公有字段倾向于将你链接想特定的实现并且限定了你改变代码灵活性。

------

