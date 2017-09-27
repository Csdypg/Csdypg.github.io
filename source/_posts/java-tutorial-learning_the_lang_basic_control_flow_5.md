---
title: Java 学习指南_学习Java：基础-控制流程-分支语句
date: 2017-09-26 10:00:59
tags: 
- java
- tutorial
- 教程
- 分支语句
- Branching
categories:
- java
keywords:
- java
- 教程
- tutorial
- 分支语句
- Branching
---

# 分支语句

##  `break` 语句



`break` 语句有两种形式，带标签以及不带标签，你之前在`switch`语句的讨论中已经见到国不带标签的`break`语句。你同样可以使用不带标签`break`语句来终止一个 `for`, `while`, 或者 `do-while` 循环,就像下面示例程序展示的一样 [`BreakDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/BreakDemo.java) :

```java
class BreakDemo {
    public static void main(String[] args) {

        int[] arrayOfInts = 
            { 32, 87, 3, 589,
              12, 1076, 2000,
              8, 622, 127 };
        int searchfor = 12;

        int i;
        boolean foundIt = false;

        for (i = 0; i < arrayOfInts.length; i++) {
            if (arrayOfInts[i] == searchfor) {
                foundIt = true;
                break;
            }
        }

        if (foundIt) {
            System.out.println("Found " + searchfor + " at index " + i);
        } else {
            System.out.println(searchfor + " not in the array");
        }
    }
}
```

这个程序在一个数组中搜索数字12。`break`语句，当找到这个值时终止循环。控制流程跳转至for循环结束以后的语句。程序的输出如下:

```java
Found 12 at index 4
```

一个无标签的`break`语句终止最内层的 `switch`, `for`, `while`, 或者 `do-while` 语句,但是一个带标签的 `break` 语句可以终止外部的语句。下面的程序, [`BreakWithLabelDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/BreakWithLabelDemo.java),和前一个程序相似,但是使用了嵌套`for`循环在二维数组中搜索一个值.当找到这个值时，一个带标签的`break`语句终止外部的循环（标签'search'）:

```java
class BreakWithLabelDemo {
    public static void main(String[] args) {

        int[][] arrayOfInts = { 
            { 32, 87, 3, 589 },
            { 12, 1076, 2000, 8 },
            { 622, 127, 77, 955 }
        };
        int searchfor = 12;

        int i;
        int j = 0;
        boolean foundIt = false;

    search:
        for (i = 0; i < arrayOfInts.length; i++) {
            for (j = 0; j < arrayOfInts[i].length;
                 j++) {
                if (arrayOfInts[i][j] == searchfor) {
                    foundIt = true;
                    break search;
                }
            }
        }

        if (foundIt) {
            System.out.println("Found " + searchfor + " at " + i + ", " + j);
        } else {
            System.out.println(searchfor + " not in the array");
        }
    }
}
```

输出如下.

```
Found 12 at 1, 0
```

`break`语句终止标记的语句；并不是控制流程跳转至标签，而是跳转至标签语句（块）之后的语句。

## `continue` 语句

 `continue`跳过一个 `for`, `while` , 或者 `do-while` 循环的当前迭代.无标签的`continue`语句跳至最内层循环体的结尾，然后球的控制循环`boolean`表达式的值。下面的程序, [`ContinueDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ContinueDemo.java) , 检查字符串`String`的每一个字符，统计遇到的字母"p"的数量。如果遇到的字符不是''p",`continue`语句控制流程掠过剩下的循环直接进行下一个字符的检测。如果该字符是"p",程序为基数增加1.

```java
class ContinueDemo {
    public static void main(String[] args) {

        String searchMe = "peter piper picked a " + "peck of pickled peppers";
        int max = searchMe.length();
        int numPs = 0;

        for (int i = 0; i < max; i++) {
            // interested only in p's
            if (searchMe.charAt(i) != 'p')
                continue;

            // process p's
            numPs++;
        }
        System.out.println("Found " + numPs + " p's in the string.");
    }
}
```

以下为程序的输出：

```java
Found 9 p's in the string.
```

为了是效果更加明显，试着删掉`continue`语句然后重新编译运行，计数就会出错，输出35而不是9。

一个带标签的`continue`语句掠过一个有对应标签的外部循环的当前一次迭代。下面的示例程序，, `ContinueWithLabelDemo`, 使用嵌套循环搜索一个子字符串在另一个字符串中出现的位置。使用两个嵌套循环是必要的：一个用来遍历子字符串，另一个用来遍历被搜索的字符串。以下程序，[`ContinueWithLabelDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ContinueWithLabelDemo.java), 使用带标签的`continue`语句来掠过外部循环的迭代。

```java
class ContinueWithLabelDemo {
    public static void main(String[] args) {

        String searchMe = "Look for a substring in me";
        String substring = "sub";
        boolean foundIt = false;

        int max = searchMe.length() - 
                  substring.length();

    test:
        for (int i = 0; i <= max; i++) {
            int n = substring.length();
            int j = i;
            int k = 0;
            while (n-- != 0) {
                if (searchMe.charAt(j++) != substring.charAt(k++)) {
                    continue test;
                }
            }
            foundIt = true;
                break test;
        }
        System.out.println(foundIt ? "Found it" : "Didn't find it");
    }
}
```

以下为程序的输出：

```java
Found it
```

##  `return` 语句

最后一个分支语句是`return`语句。`return`语句存在与当前的方法中，控制流程返回到方法被调用的地方。`return`语句有两种形式：一种返回一个值，一种不返回。返回值的时候只需要把返回的值（或者是用来计算返回值的表达式）放在`return`关键字之后。

```java
return ++count;
```

返回值的数据类型必须有方法声明的返回值的数据类型匹配。当方法的声明为`void`时，需要使用不带返回值的`return`形式。

```java
return;
```

类与对象 [Classes and Objects](http://docs.oracle.com/javase/tutorial/java/javaOO/methods.html) 课程将会覆盖所有你需要知道的写方法的知识。