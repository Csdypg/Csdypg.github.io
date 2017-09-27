---
title: Java 学习指南_学习Java：基础-控制流程-for
date: 2017-09-26 10:00:59
tags: 
- java
- tutorial
- 教程
- for
categories:
- java
keywords:
- java
- 教程
- tutorial
- for
---

# for 语句

`for`语句为迭代一个范围内的值提供了一种简介的方法。开发者经常称之为'for 循环',因为它重复循环直到满足一个特定条件的方式。`for`循环的一般形式展示如下:

```java
for (initialization; termination;//初始化，终止条件
     increment) {//增加
    statement(s)
}
```

当你使用这种版本的`for`语句时，注意以下几点:

- 初始化表达式初始化整个循环；它只随着循环开始执行一次.
- 当终止条件的表达式球的`false`时，循环终止。
- 增加表达式在循环的每一次迭代之后被调用，表达式的只增加或减少都时支持的。

下面的程序, [`ForDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ForDemo.java), 使用常规的`for`语句输出了1到10：

```java
class ForDemo {
    public static void main(String[] args){
         for(int i=1; i<11; i++){
              System.out.println("Count is: " + i);
         }
    }
}
```

程序 输出如下:

```java
Count is: 1
Count is: 2
Count is: 3
Count is: 4
Count is: 5
Count is: 6
Count is: 7
Count is: 8
Count is: 9
Count is: 10
```

注意代码时如何在初始化表达式中声明一个变量的。变量的使用范围包含从它声明的地方起到`for`语句掌控的代码块结尾，因此它也可以在终止条件以及增减表达式中使用。如果控制`for`语句的变量没有必要出现在循环之外，最好在初始化表达式中声明它。变量名 `i` `j` `k`都是经常用来控制`for`循环的；在初始化条件中声明控制变量可以限制它的使用范围并减少错误。

`for`循环的三个表达式时可选的；如下代码可以创建一个死循环:

```java
// infinite loop
for ( ; ; ) {
    
    // your code goes here
}
```

`for`循环还有另外一种设计，用来迭代集合 [Collections](http://docs.oracle.com/javase/tutorial/collections/index.html) 与数组 [arrays](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html) 。这种形式有时候也被成为增强for循环，可以用来使循环更加简洁和易读。为了展示，关注如下的数组，持有1到10十个数字：

```java
int[] numbers = {1,2,3,4,5,6,7,8,9,10};
```

下面的程序 [`EnhancedForDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/EnhancedForDemo.java), 使用增强`for`循环迭代并输出以上数组:

```
class EnhancedForDemo {
    public static void main(String[] args){
         int[] numbers = 
             {1,2,3,4,5,6,7,8,9,10};
         for (int item : numbers) {
             System.out.println("Count is: " + item);
         }
    }
}
```

在这个例子中，变量`item`持有数字数组中的当前值，代码的输出与之前的程序使一致的:

```
Count is: 1
Count is: 2
Count is: 3
Count is: 4
Count is: 5
Count is: 6
Count is: 7
Count is: 8
Count is: 9
Count is: 10

```

我们推荐在可能的情况下使用这种形式的`for`循环代替普通`for`循环。