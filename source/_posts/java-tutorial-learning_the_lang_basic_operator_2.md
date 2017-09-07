---
title: Java 学习指南_学习Java：相等，关系，条件运算符
date: 2017-09-07 11:58:59
tags: 
- java
- tutorial
- 教程
- Operator
- 相等
- 关系
- 条件运算符
categories:
- java	
keywords:
- java
- 教程
- tutorial
- Operator
- 相等
- 关系
- 条件运算符
---

# 相等，关系，条件运算符

## 相等以及关系运算符

相等以及关系运算符确定一个运算银子是大于，小于，等于，或者不等于另一个。这些操作符大多数你可能都看起来很熟悉。注意判断两个原始值是否相等的时候一定要使用 "`==`", 而不是 "`=`".

```java
==      equal to
!=      not equal to
>       greater than
>=      greater than or equal to
<       less than
<=      less than or equal to
```

下面的程序 [`ComparisonDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ComparisonDemo.java),测试了比较操作符:

```java
class ComparisonDemo {

    public static void main(String[] args){
        int value1 = 1;
        int value2 = 2;
        if(value1 == value2)
            System.out.println("value1 == value2");
        if(value1 != value2)
            System.out.println("value1 != value2");
        if(value1 > value2)
            System.out.println("value1 > value2");
        if(value1 < value2)
            System.out.println("value1 < value2");
        if(value1 <= value2)
            System.out.println("value1 <= value2");
    }
}
```

输出结果:

```java
value1 != value2
value1 <  value2
value1 <= value2
```

## 条件运算符

运算符 `&&` 和 `||` 代表了两个布尔表达式的*逻辑与*和*逻辑或*运算。这两个操作符都表现"短路"行为，意味着第二个操作因子仅在试用的时候才进行计算。

```java
&& Conditional-AND
|| Conditional-OR
```

下面程序, [`ConditionalDemo1`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ConditionalDemo1.java), 测试了操作因子:

```java
class ConditionalDemo1 {

    public static void main(String[] args){
        int value1 = 1;
        int value2 = 2;
        if((value1 == 1) && (value2 == 2))
            System.out.println("value1 is 1 AND value2 is 2");
        if((value1 == 1) || (value2 == 1))
            System.out.println("value1 is 1 OR value2 is 1");
    }
}
```

另外一个条件运算符 `?:`, 可以看作是 `if-then-else` (在控制流程部分讨论 )语句块的简写 .该操作符也被称为三元运算符因为他使用了三个操作因子。下面的例子中，该操作符可以读作: "如果 `someCondition` 是 `true`, 将 `value1` 的值赋给`result`. 否则的话，将 `value2` 的值赋值给 `result`."

下面的程序, [`ConditionalDemo2`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ConditionalDemo2.java),  测试了三元运算符`?:` :

```java
class ConditionalDemo2 {

    public static void main(String[] args){
        int value1 = 1;
        int value2 = 2;
        int result;
        boolean someCondition = true;
        result = someCondition ? value1 : value2;

        System.out.println(result);
    }
}
```

因为 `someCondition` 是 true,这个程序打印了  "1" . 使用 `?:` 运算符代替 `if-then-else` 语块可以使你的代码可读性更高; 例如当表达式比较紧凑又没有附加结果（赋值的时候）.

## 类型对照运算符instanceof

 `instanceof`运算符那一个对象与具体的类进行对比。你可以使用它来测试对象是否是某个类的实例，是否是子类的实例，或者是否为实现了某个结构的类的实例。

下面的程序 [`InstanceofDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/InstanceofDemo.java),定义了一个父类 (类名 `Parent`),一个简单的接口 (接口名 `MyInterface`), 以及一个继承了父类并实现了接口的子类 (类名 `Child`) .

```java
class InstanceofDemo {
    public static void main(String[] args) {

        Parent obj1 = new Parent();
        Parent obj2 = new Child();

        System.out.println("obj1 instanceof Parent: "
            + (obj1 instanceof Parent));
        System.out.println("obj1 instanceof Child: "
            + (obj1 instanceof Child));
        System.out.println("obj1 instanceof MyInterface: "
            + (obj1 instanceof MyInterface));
        System.out.println("obj2 instanceof Parent: "
            + (obj2 instanceof Parent));
        System.out.println("obj2 instanceof Child: "
            + (obj2 instanceof Child));
        System.out.println("obj2 instanceof MyInterface: "
            + (obj2 instanceof MyInterface));
    }
}

class Parent {}
class Child extends Parent implements MyInterface {}
interface MyInterface {}
```

输出结果:

```
obj1 instanceof Parent: true
obj1 instanceof Child: false
obj1 instanceof MyInterface: false
obj2 instanceof Parent: true
obj2 instanceof Child: true
obj2 instanceof MyInterface: true
```

使用的 `instanceof` 运算符的时候, 注意 `null`不是任何类的实例.