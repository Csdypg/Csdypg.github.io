---
title: Java 学习指南_学习Java：位运算与位移运算
date: 2017-09-07 12:58:59
tags: 
- java
- tutorial
- 教程
- Operator
- 位运算
- 关系位移运算
- Bitwise
- Bit Shift
categories:
- java	
keywords:
- java
- 教程
- tutorial
- Operator
- 位运算
- 关系位移运算
- Bitwise
- Bit Shift
---

# 位运算与位移运算Bitwise and Bit Shift Operators

Java编程语言同样提供了完整的位运算以及位移运算运算符。因为本节所讨论的运算符并不常用。因此简单介绍，目的只是为了让你意识到这些运算符的存在。

一元位运算符补码运算 "`~`" 反转一个位的形式；可以用于任意一个整形类型，将每一个“0”变为“1”，将每一个“1”变为“0”。例如，一个`byte`包含8位；将该操作符应用到形如"00000000"的值将得到 "11111111".

有符号的左位移运算符 "`<<`" 将一个位组向左移动，有符号的右位移运算付"`>>`"将一个位组向右移动。位组为运算符左边的操作因子， 移动位置的数目为运算符右边的操作因子。无符号的右位移运算符 "`>>>`" 在最左的位置上加入一个0，而 `">>"` 之后的最左位置则要取决于符号的扩展。

位运算 `&`符号表示 位与运算。

位运算 `^`符号表示位异或运算。

位运算 `|`符号表示位或运算。下面的程序, [`BitDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/BitDemo.java), 使用的位与运算并且将结果打印了出来.

```java
class BitDemo {
    public static void main(String[] args) {
        int bitmask = 0x000F;
        int val = 0x2222;
        // prints "2"
        System.out.println(val & bitmask);
    }
}
```

