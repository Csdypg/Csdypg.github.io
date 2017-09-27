---
title: Java 学习指南_学习Java：基础-控制流程-if-then&if-then-else
date: 2017-09-20 15:36:59
tags: 
- java
- tutorial
- 教程
- if-else
- if-then-else
categories:
- java
keywords:
- java
- 教程
- tutorial
- if-else
- if-then-else	
---

#  if-then以及if-then-else 语句

##  `if-then` 语句

 `if-then`语句是最基本的控制流程语句。它可以告诉程序只有某个特定的测试运算结果为`true`时执行确定的某部分代码。例如，在`Bicycle`类中只有自行车在运行的过程中时，才允许刹车减小自行车的速度。`applyBrakes`（使用刹车)方法的一种实现代码如下：

```java
void applyBrakes() {
    // the "if" clause: bicycle must be moving
    if (isMoving){ 
        // the "then" clause: decrease current speed
        currentSpeed--;
    }
}
```

如果这个测试`isMoving`j结果为false(意味着自行车并没有在刹车状态),控制跳至 `if-then` 语句结尾.

说明一下，当`if-then` then代码块中只有一句代码的时候，可以省略保卫代码块的花括号:

```java
void applyBrakes() {
    // same as above, but without braces 
    if (isMoving)
        currentSpeed--;
}
```

可以平个人喜好来决定在只有一句代码的情况下是否使用花括号。不适用的话可能不会比较容易犯错，因为如果有第二句代码被加入到then代码块中时，会经常出现忘记添加花括号，编译器不会识别这样的手误；程序就会得到错误的结果。

##  `if-then-else`语句

 `if-then-else`语句 当if 字句运算结果为`false`时提供第二条执行路径。在`applyBrakes`方法中 可以使用`if-then-else`语句，如果自行车没有在运行状态下时使用的刹车也可以采取一些措施。这里简单的打印出错误信息声明自行车已经停止了。

```java
void applyBrakes() {
    if (isMoving) {
        currentSpeed--;
    } else {
        System.err.println("The bicycle has already stopped!");
    } 
}
```

下面的程序中, [`IfElseDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/IfElseDemo.java), 根据score分数的测试结果为grade级别赋值：大于等于90为A，大于等于80为B，等等.

```java
class IfElseDemo {
    public static void main(String[] args) {

        int testscore = 76;
        char grade;

        if (testscore >= 90) {
            grade = 'A';
        } else if (testscore >= 80) {
            grade = 'B';
        } else if (testscore >= 70) {
            grade = 'C';
        } else if (testscore >= 60) {
            grade = 'D';
        } else {
            grade = 'F';
        }
        System.out.println("Grade = " + grade);
    }
}
```

输出结果如下:

```
    Grade = C
```

你可能注意到`testScore`可以满足不止一个条件：`76>=70`,`76>=60`.不过，一旦一个条件满足了，相应的语句就会执行 `(grade = 'C';)` ，剩下的条件不在运算。