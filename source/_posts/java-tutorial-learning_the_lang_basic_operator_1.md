---
title: Java 学习指南_学习Java：赋值，算术，一元运算
date: 2017-08-21 11:58:59
tags: 
- java
- tutorial
- 教程
- Operator
- 赋值
- 算术
- 一元运算
categories:
- java	
keywords:
- java
- 教程
- tutorial
- Operator
- 赋值
- 算术
- 一元运算
---

# 赋值，算术，一元运算Assignment, Arithmetic, and Unary Operators

## 简单的赋值操作The Simple Assignment Operator

你会碰到最常用的赋值运算符之一是"`=`".你再Bicycle类中看到过；它将右边的值分配给左边的运算对象:

```java
 int cadence = 0;
 int speed = 0;
 int gear = 1;
```

该运算符同样适用于对象来指定*对象引用*,[创建对象]()章节中中会讨论到。

## 算术运算符The Arithmetic Operators

Java编程语言提供了加减乘除运算符。你可以通过基础数学运算中对应的运算符号来识别他们。唯一一个新符号是"`%`",用来一个数除以另一个数之后的余数作为它的结果。

| Operator | Description      |
| -------- | ---------------- |
| `+`      | 加法运算 (同样用于字符串连接) |
| `-`      | 减法运算             |
| `*`      | 乘法运算             |
| `/`      | 除法运算             |
| `%`      | 取模运算             |

<!--more -->

下面的程序，[`ArithmeticDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ArithmeticDemo.java),测试了算术运算符.

```java
class ArithmeticDemo {

    public static void main (String[] args) {

        int result = 1 + 2;
        // result is now 3
        System.out.println("1 + 2 = " + result);
        int original_result = result;

        result = result - 1;
        // result is now 2
        System.out.println(original_result + " - 1 = " + result);
        original_result = result;

        result = result * 2;
        // result is now 4
        System.out.println(original_result + " * 2 = " + result);
        original_result = result;

        result = result / 2;
        // result is now 2
        System.out.println(original_result + " / 2 = " + result);
        original_result = result;

        result = result + 8;
        // result is now 10
        System.out.println(original_result + " + 8 = " + result);
        original_result = result;

        result = result % 7;
        // result is now 3
        System.out.println(original_result + " % 7 = " + result);
    }
}

```

This program prints the following:

```
1 + 2 = 3
3 - 1 = 2
2 * 2 = 4
4 / 2 = 2
2 + 8 = 10
10 % 7 = 3
```

你用样可以使用算术运算符与赋值运算符结合来进行混合赋值 *compound assignments*。例如, `x+=1;` 与 `x=x+1;`都将 `x` 的值增加了 1.

 `+`运算符同样可以用于连接连个字符串，如下所示  [`ConcatDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ConcatDemo.java) :

```java
class ConcatDemo {
    public static void main(String[] args){
        String firstString = "This is";
        String secondString = " a concatenated string.";
        String thirdString = firstString+secondString;
        System.out.println(thirdString);
    }
}
```

程序结束时，变量 `thirdString`包含了 "This is a concatenated string.", 将在标准输出中打印.

## 一元运算符The Unary Operators

一元运算符只需要一个操作因子；提供多种操作，例如对一个值增加/减去1，取一个表达式的相反数，或者反转一个布尔值。

| Operator | Description            |
| -------- | ---------------------- |
| `+`      | 一元+操作符;表明正值(尽管正值并没有带+) |
| `-`      | 一元减操作符;去表达式相反数         |
| `++`     | 自增操作;值增加1              |
| `--`     | 自减操作;值减少1              |
| `!`      | 逻辑否操作;反转一个布尔值          |

下面程序 [`UnaryDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/UnaryDemo.java),测试了一元运算符:

```
class UnaryDemo {

    public static void main(String[] args) {

        int result = +1;
        // result is now 1
        System.out.println(result);

        result--;
        // result is now 0
        System.out.println(result);

        result++;
        // result is now 1
        System.out.println(result);

        result = -result;
        // result is now -1
        System.out.println(result);

        boolean success = false;
        // false
        System.out.println(success);
        // true
        System.out.println(!success);
    }
}
```

自增自减操作符可以用于操作子之前(前缀)或之后(后缀)。代码 `result++;` 和`++result;` 都将是 `result` 增加1. 区别在于前缀版表达式 (`++result`)求得增加后的值,，后缀版表达式 (`result++`) 求得的是原值.如果你只是简单的自增或这自减，选择哪个版本都可以，但是如果作为更大的表达式的一部分时，如何选择将对结果产生重大影响。

下面的程序, [`PrePostDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/PrePostDemo.java), 举例说明了前缀/后缀自增运算符:

```java
class PrePostDemo {
    public static void main(String[] args){
        int i = 3;
        i++;
        // prints 4
        System.out.println(i);
        ++i;			   
        // prints 5
        System.out.println(i);
        // prints 6
        System.out.println(++i);
        // prints 6
        System.out.println(i++);
        // prints 7
        System.out.println(i);
    }
}
```