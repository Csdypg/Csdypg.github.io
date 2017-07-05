---
title: Java 学习指南_学习Java：基础—基本数据类型Primitive Data Types
date: 2017-07-05 01:56:59
tags: 
- java
- tutorial
- 教程
categories:
- java	
keywords:
- java
- 教程
- tutorial
---

# 基本数据类型Primitive Data Types

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

Java编程语言是静态数据类型，意味着你在使用某一个变量之前必须先声明它，就像你之前看到的，包含了变量的名字和类型：

```java
int gear = 1;
```

这么做的目的是告诉程序一个命名为“gear",保存着数字类型的数据，初始值为1的实例变量。一个变量的数据类型决定了他可以存储什么样的值，以及可以对他进行什么样的操作。除了`int`,Java还支持其他七种基本数据类型。基本数据类型是编程语言预定义并用保留关键字命名的。基本数据类型不能用其他基本数据类型共享状态。八种基本数据类型分别如下：

* **byte：**`byte`数据类型是一种带符号的8位二进制整数。它的最小值是-128，最大值为127.`byte`数据类型在大型的数组中使用可以用来节省内存，有时候节省内存很重要。`byte`同样可以用来代替`int`，因为`byte`数据的有限范围可你使你的代码更清晰。事实上有限的变量序列可以作为文档的一种组织形式。

- **short**:`short`数据类型是一种16位的带符号二进制整数。最小值为-32,768最大值为32767.就像`byte`一样，之前的说明同样适用。当节省内存很有必要的时候，你也可以在大型数组中适用`short`来节省内存。

- **int**: 默认情况下`int`是一种32位的带符号二进制整数。最小值为
  $$
  -2^{31}
  $$
  最大值为
  $$
  2^{31}-1
  $$
  在Java SE8和更新的版本中，你可以适用`int`作为无符号的32位整数，最小值为0，最大值为
  $$
  2^{32}-1
  $$
  通过`Integer`类来将`int`作为一个无符号的整数使用。`compareUnsigned，``divideUnsigned`等静态方法已经添加到`Integer`类来支持无符号整数的算术操作。

  ​

- **long**: `long` 是一种64位的带符号二进制整数。最小值为
  $$
  -2^{63}
  $$
  最大值为
  $$
  2^{63}-1
  $$
  在Java SE8和更新的版本中，你可以适用`long `作为无符号的64位整数，最小值为0，最大值为
  $$
  2^{64}-1
  $$
  通过`Long`类来将`long`作为一个无符号的整数使用。当`int`提供的数据范围不足的时候你可以使用这种数据类型。`compareUnsigned，``divideUnsigned`等静态方法已经添加到`Long`类来支持无符号整数的算术操作。

- **float**: `float`数据类型是一种IEEE 754标准的32位单精度浮点数。它的范围不在此讨论，但是你可以在[浮点数类型，格式化，以及值](https://docs.oracle.com/javase/specs/jls/se7/html/jls-4.html#jls-4.2.3)章节去详细了解。正如`byte`和`short`一样，在大型的数组中书用`float`来节省内存。但是一定不要使用该数据类型来保存精确的值，譬如货币。如果要保存货币，建议使用[java.math.BigDecimal](https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html) 来代替。 [Numbers and Strings数字与字符串](http://docs.oracle.com/javase/tutorial/java/data/index.html) 章节包含了 `BigDecimal`类以及其他非常有用的类。 

- **double**:`float`数据类型是一种IEEE 754标准的64位双精度浮点数。它的范围不在此讨论，但是你可以在[浮点数类型，格式化，以及值](https://docs.oracle.com/javase/specs/jls/se7/html/jls-4.html#jls-4.2.3)章节去详细了解。对于小数类型的数据`double`通常是默认类型。正如之前说的，不要使用该数据类型来保存货币等精确的值。

- **boolean**: `boolean`类型数据只有两个可能的值`true`和`false`。使用这种数据类型来简单的标记真/假两种情况。这种数据类型标识了一位信息，但是他的“size”并不是明确定义的。

- **char**:  `char` 类型是一个16为Unicode字符。有一个最小值 `'\u0000'` ( 0) 和最大值 `'\uffff'` (65,535 包含)。

除了上述的八种基本数据类型之外，Java还通过 [java.lang.String](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)类对字符串类型提供了特别支持。通过双引号包括你的字符将自动创建一个`String`对象。例如`String s = "this is a string";`. `String`对象是 *immutable*不可变对象，意味着已经创建就不能更改。从技术上说`String`类并不是基本数据类型，不过考虑到Java对它的特殊支持，你可能会倾向于这样想。关于`String` 类的更多知识可以在 [简单数据对象Simple Data Objects](http://docs.oracle.com/javase/tutorial/java/data/index.html)中学到。



## 默认值Default Values

有时候没有必要在生命field属性时就赋值。生命但是为初始化的field将会被编译器设置一个合理的默认值。一般来说这个默认值就是0或者`null`，根据数据类型不同而不同。但是依赖默认值被认为是一种不好的变成习惯。

下面的表格列出了以上数据类型的默认初始化值：

| **Data Type**          | **Default Value (for fields)** |
| ---------------------- | ------------------------------ |
| byte                   | 0                              |
| short                  | 0                              |
| int                    | 0                              |
| long                   | 0L                             |
| float                  | 0.0f                           |
| double                 | 0.0d                           |
| char                   | '\u0000'                       |
| String (or any object) | null                           |
| boolean                | false                          |

局部变量稍微有些区别，编译器不会为局部变量赋默认值。所以如果你不能在生命的时候初始化局部变量，确保在调用它之前为其赋值。访问未初始化的局部变量将会导致编译时错误。

## 字面值

你可能注意到`new`关键字在定义基本数据类型的时候并没有使用。基本数据类型是语言内建的特殊数据类型；并不是由类创建的对象。在代码中一个`literal`字面值代表一个固定的值，字面值可以直接体现在你的源代码中而不需要计算。如下所示：可以直接使用字面值未基本数据类型赋值:

```java
boolean result = true;
char capitalC = 'C';
byte b = 100;
short s = 10000;
int i = 100000;
```

## 整数类型的字面值

An integer literal is of type `long` if it ends with the letter `L` or `l`; otherwise it is of type `int`. It is recommended that you use the upper case letter `L` because the lower case letter `l` is hard to distinguish from the digit `1`.

Values of the integral types `byte`, `short`, `int`, and `long` can be created from `int` literals. Values of type `long` that exceed the range of `int` can be created from `long` literals. Integer literals can be expressed by these number systems:

- Decimal: Base 10, whose digits consists of the numbers 0 through 9; this is the number system you use every day
- Hexadecimal: Base 16, whose digits consist of the numbers 0 through 9 and the letters A through F
- Binary: Base 2, whose digits consists of the numbers 0 and 1 (you can create binary literals in Java SE 7 and later)

For general-purpose programming, the decimal system is likely to be the only number system you'll ever use. However, if you need to use another number system, the following example shows the correct syntax. The prefix `0x` indicates hexadecimal and `0b` indicates binary:

```
// The number 26, in decimal
int decVal = 26;
//  The number 26, in hexadecimal
int hexVal = 0x1a;
// The number 26, in binary
int binVal = 0b11010;

```

## 浮点类型的字面值

A floating-point literal is of type `float` if it ends with the letter `F` or `f`; otherwise its type is `double` and it can optionally end with the letter `D`or `d`.

The floating point types (`float` and `double`) can also be expressed using E or e (for scientific notation), F or f (32-bit float literal) and D or d (64-bit double literal; this is the default and by convention is omitted).

```
double d1 = 123.4;
// same value as d1, but in scientific notation
double d2 = 1.234e2;
float f1  = 123.4f;
```

## 字符与字符串类型的字面值

Literals of types `char` and `String` may contain any Unicode (UTF-16) characters. If your editor and file system allow it, you can use such characters directly in your code. If not, you can use a "Unicode escape" such as `'\u0108'` (capital C with circumflex), or `"S\u00ED Se\u00F1or"` (Sí Señor in Spanish). Always use 'single quotes' for `char` literals and "double quotes" for `String` literals. Unicode escape sequences may be used elsewhere in a program (such as in field names, for example), not just in `char` or `String` literals.

The Java programming language also supports a few special escape sequences for `char` and `String` literals: `\b` (backspace), `\t` (tab), `\n`(line feed), `\f` (form feed), `\r` (carriage return), `\"` (double quote), `\'` (single quote), and `\\` (backslash).

There's also a special `null` literal that can be used as a value for any reference type. `null` may be assigned to any variable, except variables of primitive types. There's little you can do with a `null` value beyond testing for its presence. Therefore, `null` is often used in programs as a marker to indicate that some object is unavailable.

Finally, there's also a special kind of literal called a *class literal*, formed by taking a type name and appending "`.class"`; for example, `String.class`. This refers to the object (of type `Class`) that represents the type itself.

## 在数字类字面值中使用下划线 *_*

In Java SE 7 and later, any number of underscore characters (`_`) can appear anywhere between digits in a numerical literal. This feature enables you, for example. to separate groups of digits in numeric literals, which can improve the readability of your code.

For instance, if your code contains numbers with many digits, you can use an underscore character to separate digits in groups of three, similar to how you would use a punctuation mark like a comma, or a space, as a separator.

The following example shows other ways you can use the underscore in numeric literals:

```java
long creditCardNumber = 1234_5678_9012_3456L;
long socialSecurityNumber = 999_99_9999L;
float pi =  3.14_15F;
long hexBytes = 0xFF_EC_DE_5E;
long hexWords = 0xCAFE_BABE;
long maxLong = 0x7fff_ffff_ffff_ffffL;
byte nybbles = 0b0010_0101;
long bytes = 0b11010010_01101001_10010100_10010010;
```

You can place underscores only between digits; you cannot place underscores in the following places:

- At the beginning or end of a number
- Adjacent to a decimal point in a floating point literal
- Prior to an `F` or `L` suffix
- In positions where a string of digits is expected

The following examples demonstrate valid and invalid underscore placements (which are highlighted) in numeric literals:

```java
// Invalid: cannot put underscores
// adjacent to a decimal point
float pi1 = 3_.1415F;
// Invalid: cannot put underscores 
// adjacent to a decimal point
float pi2 = 3._1415F;
// Invalid: cannot put underscores 
// prior to an L suffix
long socialSecurityNumber1 = 999_99_9999_L;

// OK (decimal literal)
int x1 = 5_2;
// Invalid: cannot put underscores
// At the end of a literal
int x2 = 52_;
// OK (decimal literal)
int x3 = 5_______2;

// Invalid: cannot put underscores
// in the 0x radix prefix
int x4 = 0_x52;
// Invalid: cannot put underscores
// at the beginning of a number
int x5 = 0x_52;
// OK (hexadecimal literal)
int x6 = 0x5_2; 
// Invalid: cannot put underscores
// at the end of a number
int x7 = 0x52_;
```