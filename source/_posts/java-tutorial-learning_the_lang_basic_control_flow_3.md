---
title: Java 学习指南_学习Java：基础-控制流程-while & do-while
date: 2017-09-26 9:00:59
tags: 
- java
- tutorial
- 教程
- while
- do-while
categories:
- java
keywords:
- java
- 教程
- tutorial
- switch
- while
- do-while
---

# while 以及 do-while 语句

当一个特定的条件为`true`时，`while`语句持续的执行一段代码块.它的语法形式如下：

The `while` statement continually executes a block of statements while a particular condition is `true`. Its syntax can be expressed as:

```java
while (expression) {
     statement(s)
}	
```

`while`语句计算一个必须返回布尔值的表达式的值。如果这个表达式的结果为`true`,`while`语句，执行其代码块中的语句，`while`语句会持续验证表达式的值，并执行它的代码块直到表达式的结果返回`false`。使用`while`语句打印出1到10的值可以通过如下的示例程序 [`WhileDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/WhileDemo.java) 完成:

```java
class WhileDemo {
    public static void main(String[] args){
        int count = 1;
        while (count < 11) {
            System.out.println("Count is: " + count);
            count++;
        }
    }
}
```

你可以像下面的代码一样实现一个无限循环(死循环):

```java
while (true){
    // your code goes here
}
```

Java编程语言同样提供了`do-while`语句，形式如下:

```java
do {
     statement(s)
} while (expression);
```



 `do-while` 与 `while` 语句的区别在于 `do-while` 在代码块的底部计算表达式的布尔值结果而不是在顶部。因此，`do`代码块中的语句至少执行一次,就像下面的示例代码展示的一样 [`DoWhileDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/DoWhileDemo.java) :

```java
class DoWhileDemo {
    public static void main(String[] args){
        int count = 1;
        do {
            System.out.println("Count is: " + count);
            count++;
        } while (count < 11);
    }
}
```