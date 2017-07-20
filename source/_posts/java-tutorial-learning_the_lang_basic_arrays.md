---
title: Java 学习指南_学习Java：基础—数组Arrays
date: 2017-07-20 17:56:59
tags: 
- java
- tutorial
- 教程
- 数组
- Array
categories:
- java	
keywords:
- java
- 教程
- 数组
- Array
- tutorial
---

# 数组Arrays

一个*array数组*是可以持有固定数量单一数据类型的容器对象。数组的长度在数组创建的时候确定的，创建以后数组的长度就是固定不变的。在之前的“HelloWorld”项目中的`main`方法中，你已经见过简单的数组示例，本章节将更加详细的讨论数组。

![Illustration of an array as 10 boxes numbered 0 through 9; an index of 0 indicates the first element in the array](http://docs.oracle.com/javase/tutorial/figures/java/objects-tenElementArray.gif)

包含10个元素的数组。An array of 10 elements.

数组中的每一个项目叫做一个*element元素*，每一个愿元素都可以通过的数字index索引类访问。就像上面的插图展示的一样，数字索引从0开始。第9个元素将通过索引8来访问。下面的程序中，ArrayDemo，创建了一个整数数组，在数组里放入了一些值，然后在标准输出中打印了每一个值。

```java
class ArrayDemo {
    public static void main(String[] args) {
        // declares an array of integers 声明一个整数数组
        int[] anArray;

        // allocates memory for 10 integers 分配10个整数的存贮空间
        anArray = new int[10];
           
        // initialize first element 初始化第一个元素
        anArray[0] = 100;
        // initialize second element 初始化第二个元素
        anArray[1] = 200;
        // and so forth 以及之后的元素
        anArray[2] = 300;
        anArray[3] = 400;
        anArray[4] = 500;
        anArray[5] = 600;
        anArray[6] = 700;
        anArray[7] = 800;
        anArray[8] = 900;
        anArray[9] = 1000;

        System.out.println("Element at index 0: "
                           + anArray[0]);
        System.out.println("Element at index 1: "
                           + anArray[1]);
        System.out.println("Element at index 2: "
                           + anArray[2]);
        System.out.println("Element at index 3: "
                           + anArray[3]);
        System.out.println("Element at index 4: "
                           + anArray[4]);
        System.out.println("Element at index 5: "
                           + anArray[5]);
        System.out.println("Element at index 6: "
                           + anArray[6]);
        System.out.println("Element at index 7: "
                           + anArray[7]);
        System.out.println("Element at index 8: "
                           + anArray[8]);
        System.out.println("Element at index 9: "
                           + anArray[9]);
    }
} 
```

程序的输出如下：

```
Element at index 0: 100
Element at index 1: 200
Element at index 2: 300
Element at index 3: 400
Element at index 4: 500
Element at index 5: 600
Element at index 6: 700
Element at index 7: 800
Element at index 8: 900
Element at index 9: 1000
```

实际情况下，在上面的例子中，你可以使用一种数组支持的*loop constructs*循环结构来迭代数组的每一个元素，而不是一行一行的写。不过，这个例子清晰的说明了数组的语法。你将会在[控制流程]()章节学到不同种类的循环结构（`for`,`while`以及`do-while`).

## 声明一个引用数组的变量

之前的程序通过下面这一行代码声明了一个名为`anArray`的数组：

```java
// declares an array of integers
int[] anArray;
```

就像声明其它类型的变量一样，声明数组包括两部分，数组类型和数组名称。数组类型写作`*type*[]`其中`*type*`是数组内元素的数据类型，方括号是一个特殊符号表明该变量持有一个数组。数组的长度并不是类型的一部分（因此方括号是空的）.数组可以任意命名，只要你遵循[命名]()章节中介绍的规则和约定。就像其他类型变量一样，声明的时候并没有创建一个数组，只是告诉编译器该变量将持有包含 特定类型数据的数组。

同样，你也可以声明其他数据类型的数组：

```java
byte[] anArrayOfBytes;
short[] anArrayOfShorts;
long[] anArrayOfLongs;
float[] anArrayOfFloats;
double[] anArrayOfDoubles;
boolean[] anArrayOfBooleans;
char[] anArrayOfChars;
String[] anArrayOfStrings;
```

也可以把方括号置于数组名称之后：

```java
// this form is discouraged 但是不鼓励这么做
float anArrayOfFloats[];
```

不过一般情况下不推荐这么做,方括号标明了变量类型为数组，应该与指定类型一起出现。

## 创建，初始化，访问数组

创建数组的一种方法是适用`new`操作符。接下来的代码展示了为数组分配了可以容纳10个integer元素的存储空间，并将这个数组指向`anArray`变量。

```java
// create an array of integers
anArray = new int[10];
```

如果确实本行的话，编译器会打印出如下的错误，并且编译失败：

```
ArrayDemo.java:4: Variable anArray may not have been initialized.
```

下面几行代码为数组中的各个元素赋值：

```java
anArray[0] = 100; // initialize first element
anArray[1] = 200; // initialize second element
anArray[2] = 300; // and so forth
```

每一个数组元素可以通过的数字索引来访问：

```java
System.out.println("Element 1 at index 0: " + anArray[0]);
System.out.println("Element 2 at index 1: " + anArray[1]);
System.out.println("Element 3 at index 2: " + anArray[2]);
```

同样，你也可以适用以下语法直接创建和初始化一个数组：

```java
int[] anArray = { 
    100, 200, 300,
    400, 500, 600, 
    700, 800, 900, 1000
};
```

这里，数组的长度由数组花括号中由逗号分隔的值的数量决定。你同样可以通过使用两组或者更多的方括号定义数组的数组（或者叫多维数组），例如`String[][] names`.这样的话，每一个元素必须通过级联的数字索引值来访问。 

在Java编程语言中，一个多维数组的组成部分仍然是数组，有别于C或者Fortran，这样做的其中一个结果就是允许每一行数据可以有不同 的长度，下面代码中将展示：

```java
class MultiDimArrayDemo {
    public static void main(String[] args) {
        String[][] names = {
            {"Mr. ", "Mrs. ", "Ms. "},
            {"Smith", "Jones"}
        };
        // Mr. Smith
        System.out.println(names[0][0] + names[1][0]);
        // Ms. Jones
        System.out.println(names[0][2] + names[1][1]);
    }
}
```

程序的输出如下：

```
Mr. Smith
Ms. Jones
```

最后，你可以使用数组内置的属性`length`来判定任何数组的尺寸/长度。下面代码将输出数组的长度。

```java
 System.out.println(anArray.length);
```

## 数组的复制

`System`类有一个高性能的`arraycopy`方法，你可以使用该方法高效得将数据由一个数组复制到另一个。

```java
public static void arraycopy(Object src, int srcPos,
                             Object dest, int destPos, int length)
```

两个`Object`参数分别是要考培的源数组和目标数组。三个`int`参数分别是源数组的其实位置，目标数组的起始位置和将要复制的元素个数。

接下来的程序，声明了一个`char`字符数组,单词"decaffeinated"的拼写。然后使用`System.arraycopy`方法将数组内容的部分序列复制到第二个数组:

```java
class ArrayCopyDemo {
    public static void main(String[] args) {
        char[] copyFrom = { 'd', 'e', 'c', 'a', 'f', 'f', 'e',
			    'i', 'n', 'a', 't', 'e', 'd' };
        char[] copyTo = new char[7];

        System.arraycopy(copyFrom, 2, copyTo, 0, 7);
        System.out.println(new String(copyTo));
    }
}
```

程序的输出如下：

```java
caffein
```

## 数组的操作

数组是编程中非常强大和使用的概念。Java SE 提供了诸多方法来满足与数组相关的最常用操作。以上例子中，使用`System`类的`arraycopy`方法替代了手动迭代原数组的元素然后将每一个元素置于目标数组。开发者只用一行代码调用该方法就可以在后台完成复制的操作。

为了你的便利，Java SE 在[`java.util.Arrays`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html) 类中提供了许多方法来满足数组的操作（常见工作，诸如复制，排序，搜索数组）。

之前的例子也可以修改为使用`java.util.Arrays`类中的`copyOfRange`方法，下面例子由展示,使用该方法的不同之处在于，你可以不必在调用方法之前就创建目标数组，因为目标数组将由该方法创建和返回:

```java
class ArrayCopyOfDemo {
    public static void main(String[] args) {
        
        char[] copyFrom = {'d', 'e', 'c', 'a', 'f', 'f', 'e',
            'i', 'n', 'a', 't', 'e', 'd'};
            
        char[] copyTo = java.util.Arrays.copyOfRange(copyFrom, 2, 9);
        
        System.out.println(new String(copyTo));
    }
}
```

程序的输出同样是`caffein`,尽管这样做需要更少的代码。注意，`caopyOfRange`方法的第二个参数是要复制的范围的起始索引，包含该索引，同时第三个参数是要复制范围的结束索引，不包含该索引。在本例中，复制的范围不包含在索引9位置的元素（即字符`a`).

`java.util.Arrays`类还提供了其他有用的方法，如下：

- 搜索一个特定的值在数组中的位置下标.(方法`binarySearch`)
- 比较两个数组以判定两个数组是否相等(方法`equal`)
- 填充数组，为数组的每一个位置放置一个特定的值(方法`fill`)
- 按照升序排序数组。可以使用`sort`方法进行循序排序，或者使用Java SE8引进的`parallelSort`进行并发的排序。在多处理器系统中使用平行排序较大的数组比循序的排序要快得多。