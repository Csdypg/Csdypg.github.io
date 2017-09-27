---
title: Java 学习指南_学习Java：基础-控制流程-问答与练习
date: 2017-09-27 11:30:59
tags: 
- java
- tutorial
- 教程
- control flow
- 控制流程
categories:
- java
keywords:
- java
- 教程
- tutorial
- control flow
- 控制流程
---

# 控制流程为题与练习

## 问题

1. java编程语言支持的最基本的控制流程语句是 **？** 语句.
2. **？**语句允许一定数量的可能执行路径。
3. ？语句与`while`语句相似，但是在执行代码块的**？**计算控制表达式的布尔值.
4. 问题: 如何使用`for`语句写一个无限循环？
5. 问题:如何用`while`语句写一个无限循环？

## 练习

1. 观察以下代码片段.

   ```java
   if (aNumber >= 0)
       if (aNumber == 0)
           System.out.println("first string");
   else 
       System.out.println("second string");
   System.out.println("third string");
   ```

   1. 练习:如果`aNumber`的值为3输出的结果可能是什么？

   2. 练习:如果`aNumber`的值为3，程序的输出是什么？你的预测是什么？解释为什么输出这个结果，换句话说，代码片段的控制流程是什么? 

   3. 练习: 

      仅使用空格和换行符重新格式化代码使代码放容易理解.

   4. 练习:

      使用`{}`使代码更加清晰易读，已减少在后期维护过程中可能出现的错误.

<!-- more -->

# 控制流程为题与练习答案

## 问题答案

1. java编程语言支持的最基本的控制流程语句是 **if-then** 语句.

2. **switch**语句允许一定数量的可能执行路径。

3. **do-while**语句与`while`语句相似，但是在执行代码块的**bottom结尾**计算控制表达式的布尔值.

4. 问题: 如何使用`for`语句写一个无限循环？

   **答案:**

   ```java
   for ( ; ; ) {

   }
   ```

5. 问题:如何用`while`语句写一个无限循环？

   **答案:**

   ```java
   while (true) {

   }
   ```

## 练习答案

1. 观察以下代码片段.

   ```java
   if (aNumber >= 0)
       if (aNumber == 0)
           System.out.println("first string");
   else 
       System.out.println("second string");
   System.out.println("third string");
   ```

   1. 练习:如果`aNumber`的值为3输出的结果可能是什么？

      **答案**

      ```java
      second string
      third string
      ```

   2. 练习:如果`aNumber`的值为3，程序的输出是什么？你的预测是什么？解释为什么输出这个结果，换句话说，代码片段的控制流程是什么?

      **答案:** [`NestedIf`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/QandE/NestedIf.java)

      ```java
      second string
      third string
      ```

      3大于等于0，所以执行第二个if，因为3不等于0，所以并没有输出 `first string`控制流程执行`else。`块因为`else`与第二个`if`是绑定的，因为打印出`second string`，最后一个输出语句不包含与任何一个`if-then`语句，因此打印出`third string`。 

   3. 练习: 

      仅使用空格和换行符重新格式化代码使代码放容易理解.

      **答案:**

      ```java
      if (aNumber >= 0)
          if (aNumber == 0)
              System.out.println("first string");
          else
              System.out.println("second string");

      System.out.println("third string");
      ```

   4. 练习:

      使用`{}`使代码更加清晰易读，已减少在后期维护过程中可能出现的错误.

      **答案:**

      ```java
      if (aNumber >= 0) {
          if (aNumber == 0) {
              System.out.println("first string");
          } else {
              System.out.println("second string");
          }
      }

      System.out.println("third string");
      ```