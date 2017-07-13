---
title: Java 学习指南_学习Java：基础—数组Arrays
date: 2017-07-11 01:56:59
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



However, convention discourages this form; the brackets identify the array type and should appear with the type designation.

## Creating, Initializing, and Accessing an Array

One way to create an array is with the `new` operator. The next statement in the `ArrayDemo` program allocates an array with enough memory for 10 integer elements and assigns the array to the `anArray` variable.

```java
// create an array of integers
anArray = new int[10];
```

If this statement is missing, then the compiler prints an error like the following, and compilation fails:

```
ArrayDemo.java:4: Variable anArray may not have been initialized.
```

The next few lines assign values to each element of the array:

```java
anArray[0] = 100; // initialize first element
anArray[1] = 200; // initialize second element
anArray[2] = 300; // and so forth
```

Each array element is accessed by its numerical index:

```java
System.out.println("Element 1 at index 0: " + anArray[0]);
System.out.println("Element 2 at index 1: " + anArray[1]);
System.out.println("Element 3 at index 2: " + anArray[2]);
```

Alternatively, you can use the shortcut syntax to create and initialize an array:

```java
int[] anArray = { 
    100, 200, 300,
    400, 500, 600, 
    700, 800, 900, 1000
};
```

Here the length of the array is determined by the number of values provided between braces and separated by commas.

You can also declare an array of arrays (also known as a *multidimensional* array) by using two or more sets of brackets, such as `String[][] names`. Each element, therefore, must be accessed by a corresponding number of index values.

In the Java programming language, a multidimensional array is an array whose components are themselves arrays. This is unlike arrays in C or Fortran. A consequence of this is that the rows are allowed to vary in length, as shown in the following [`MultiDimArrayDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/MultiDimArrayDemo.java) program:

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

The output from this program is:

```
Mr. Smith
Ms. Jones
```

Finally, you can use the built-in `length` property to determine the size of any array. The following code prints the array's size to standard output:

```java
 System.out.println(anArray.length);
```

## Copying Arrays

The `System` class has an `arraycopy` method that you can use to efficiently copy data from one array into another:

```java
public static void arraycopy(Object src, int srcPos,
                             Object dest, int destPos, int length)
```

The two `Object` arguments specify the array to copy *from* and the array to copy *to*. The three `int` arguments specify the starting position in the source array, the starting position in the destination array, and the number of array elements to copy.

The following program, [`ArrayCopyDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ArrayCopyDemo.java), declares an array of `char` elements, spelling the word "decaffeinated." It uses the `System.arraycopy` method to copy a subsequence of array components into a second array:

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

The output from this program is:

```java
caffein
```

## Array Manipulations

Arrays are a powerful and useful concept used in programming. Java SE provides methods to perform some of the most common manipulations related to arrays. For instance, the[`ArrayCopyDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ArrayCopyDemo.java) example uses the `arraycopy` method of the `System` class instead of manually iterating through the elements of the source array and placing each one into the destination array. This is performed behind the scenes, enabling the developer to use just one line of code to call the method.

For your convenience, Java SE provides several methods for performing array manipulations (common tasks, such as copying, sorting and searching arrays) in the[`java.util.Arrays`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html) class. For instance, the previous example can be modified to use the `copyOfRange` method of the `java.util.Arrays` class, as you can see in the[`ArrayCopyOfDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/ArrayCopyOfDemo.java) example. The difference is that using the `copyOfRange` method does not require you to create the destination array before calling the method, because the destination array is returned by the method:

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

As you can see, the output from this program is the same (`caffein`), although it requires fewer lines of code. Note that the second parameter of the `copyOfRange` method is the initial index of the range to be copied, inclusively, while the third parameter is the final index of the range to be copied, *exclusively*. In this example, the range to be copied does not include the array element at index 9 (which contains the character `a`).

Some other useful operations provided by methods in the `java.util.Arrays` class, are:

- Searching an array for a specific value to get the index at which it is placed (the `binarySearch` method).
- Comparing two arrays to determine if they are equal or not (the `equals` method).
- Filling an array to place a specific value at each index (the `fill` method).
- Sorting an array into ascending order. This can be done either sequentially, using the `sort` method, or concurrently, using the `parallelSort` method introduced in Java SE 8. Parallel sorting of large arrays on multiprocessor systems is faster than sequential array sorting.