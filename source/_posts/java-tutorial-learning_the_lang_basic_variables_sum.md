---
title: Java 学习指南_学习Java：基础—变量总结
date: 2017-07-26 15:23:59
tags: 
- java
- tutorial
- 教程
- 变量
categories:
- java	
keywords:
- java
- 教程
- 变量
- tutorial
---

# 变量总结

​	Java编程语言同时使用'fields/域'和'variables/变量'作为其术语的一部分。实例变量(非静态fields)对于每一个类的实例都是都独一无二的。类变量(静态fields)是声明时使用`static`修饰符修饰的fields;类变量只有一份副本，无论类被实例化多少次。局部变量local variables存储方法中的临时状态。参数是为方法提供额为的信息的变量；局部变量和参数一般归类为variables(而不是fields).当命名fields和variables的时候，必须遵守相关的规则和约定。

​	八种基本数据类型：byte, short, int, long, float, double, boolean, 和 char. [`java.lang.String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 类代表字符串.编译器会为以上数据类型的fields分配适当的默认值；对于局部变量，则从不分配默认值。字面值是代表一个固定值的源代码。数组是可以持有固定数量的单一类型值的容器对象。数据的长度是在数据创建的时候确定的，并且它的长度是固定的。

