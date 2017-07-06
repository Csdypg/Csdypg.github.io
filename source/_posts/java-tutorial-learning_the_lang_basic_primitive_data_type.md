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

如果整数的字面值以`L`或者 `l`结尾则是`long`类型；否则即使`int`类型的。建议使用大写的`L`字母，因为小写的`l`很难与阿拉伯数字`1`区分。

`byte`,`short`,`int`和`long`整数类型的值可以用`int`字面值创建。超过`int`范围的`long`类型值可以作用的`long`的字面值创建。整数的字面值可以用以下数字系统表达：

* 十进制：基于10，包含了0到9十个数字，也是你每天都用的到的数字系统。
* 十六进制：基于16，包含了0到9十个数字以及A到F六个字母
* 二进制：基于2，包含了0，1（Java SE7及更新版本可以使用二进制字面值创建整数）

在一般的编程过程中，十进制系统可能是你唯一使用过的，但是如果你要使用其他的数字系统，下面的例子展示了正确的使用语法。前缀`0x`代表了十六进制， `0b`代表了二进制:

```java
// The number 26, in decimal
int decVal = 26;
//  The number 26, in hexadecimal
int hexVal = 0x1a;
// The number 26, in binary
int binVal = 0b11010;
```

## 浮点类型的字面值

如果浮点类型的字面值以`F`或者`f`结尾则表示`float`的数据，否则及表示`double`类型的，是否以字母`D`或则 `d`结尾是可选的。

浮点数（`float`和`double`）也可以用`E`或者`e`(科学记数法)，`F`或者`f`(32位字面值)，`D`或者`d`（64位字面值，默认情况下是`double`类型，一般不用写出来）.

```java
double d1 = 123.4;
// same value as d1, but in scientific notation
double d2 = 1.234e2;
float f1  = 123.4f;
```

## 字符与字符串类型的字面值

`char`与`String`类型数据的字面值可以包含任意的Unicode（UTF-16）字符。如果你的编辑器和文件系统支持Unicode，你可以直接在代码中使用。如果不支持，你可以用“Unicode转义"字符如`\u0108`(标有音符的大写C)，或者 `"S\u00ED Se\u00F1or"` (西班牙语中的Sí Señor ).一般用单引号表示`char`字符类型数据字面值，用双引号表示`String`字符串类型数据。Unicode转义字符不仅可以用于`char`或者`String`数据的字面值，同样可以用于程序的其他地方，譬如用于*field*属性的命名等。

Java同样位`char`和`String`字面值提供了以下其他特殊字符的转义: `\b` (backspace退格), `\t` (tab制表符), `\n`(line feed换行符), `\f` (form feed换页符), `\r` (carriage return回车), `\"` (double quote双引号), `\'` (single quote单引号), and `\\` (backslash反斜杠).

还有一个特殊的字面值`null`可以用作任意引用类型数据的值。`null`可以赋值给任意类型的变量除了基本数据类型。除了测试`null`的存在你几乎不能对它做其他事情。不过`null`在程序中经常用来表明某个对象是不可用的。

最后，还有一个特殊类型的字面值叫做*class*字面值，由一个类名加上`.class`构成。例如: `String.class`.它指向了代表这个类本身的对象（Class类型的对象）。

## 在数字类字面值中使用下划线 *_*

在 Java SE 7 及以后的版本中，在数字类型的字面值数字中间可以加入任意数量的下划线`_`.例如用来将数字字面值中的数字分组，以提高你代码的可读性。

例如，如果你的代码包含了许多的数字，你可以用下划将它分割为三个一组，就像你使用逗号和空格等标点符号一样。

以下例子展示了你可以在树子字面值中使用下划线的其他方式：

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

你仅可以将下划线置于数字之间，不能放在以下几种地方：

* 数字的开头或者结尾
* 在浮点数中挨着小数点
* 在`F`或者`L`后缀之前
* 只能出现数字或者字母的地方

以下例子展示了数字字面值中正确和不正确的下划线位置：

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