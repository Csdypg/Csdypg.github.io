---
title: Java 学习指南_学习Java：基础-内部类
date: 2017-10-24 14:00:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- inner class
- 内部类
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- inner class
- 内部类
---

# 内部类

讨论内部类的使用之前，首先来观察一个数组。接下来的例子中，你创建一个数组，使用Integer指填充这个数组，然后只升序输出这个数组中下标为偶数的值。

[`DataStructure.java`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/DataStructure.java) 例子有以下几个部分组成：

- `DataStructure` 外部类，包含了一个创建`DataStructure`实例的构造函数，实例包含一个填充了连续的整数数组（0，1，2，3...）以及一个打印出数组偶数下标元素的值的方法。
- `EvenIterator`内部类，实现了`DataStructureIterator`接口，并继承了 [`Iterator`](https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html)`<` [`Integer`](https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html)`>` 迭代器接口。迭代器是用来一步步的迭代一个数据结构并且通常有一个测试是否到达最后一个元素的方法，获取当前的元素并将指针移向下一个元素。
- 一个`main`方法，实例化一个`DataStructure`对象 `ds`,调用`ds`对象的`printEven`方法来输出`arrayOfInts`数组中具有偶数下边的元素值。

```java
public class DataStructure {
    
    // Create an array
    private final static int SIZE = 15;
    private int[] arrayOfInts = new int[SIZE];
    
    public DataStructure() {
        // fill the array with ascending integer values
        for (int i = 0; i < SIZE; i++) {
            arrayOfInts[i] = i;
        }
    }
    
    public void printEven() {
        
        // Print out values of even indices of the array
        DataStructureIterator iterator = this.new EvenIterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " ");
        }
        System.out.println();
    }
    
    interface DataStructureIterator extends java.util.Iterator<Integer> { } 

    // Inner class implements the DataStructureIterator interface,
    // which extends the Iterator<Integer> interface
    
    private class EvenIterator implements DataStructureIterator {
        
        // Start stepping through the array from the beginning
        private int nextIndex = 0;
        
        public boolean hasNext() {
            
            // Check if the current element is the last in the array
            return (nextIndex <= SIZE - 1);
        }        
        
        public Integer next() {
            
            // Record a value of an even index of the array
            Integer retValue = Integer.valueOf(arrayOfInts[nextIndex]);
            
            // Get the next even element
            nextIndex += 2;
            return retValue;
        }
    }
    
    public static void main(String s[]) {
        
        // Fill the array with integer values and print out only
        // values of even indices
        DataStructure ds = new DataStructure();
        ds.printEven();
    }
}
```

输出如下:

```
0 2 4 6 8 10 12 14 
```

注意`EvenIterator`类直接引用`DataStructure`对象的实例变量`arrayOfInts`.

你可以使用内部类来实现类似以上例子中的辅助类。处理用户界面事件时，你必须直到如何使用内部类，因为事件处理机制使通过内部类来扩展其用法。

## 局部类与匿名内部类

有中附加的内部类。你可以在一个方法的内部定义一个类，这样的类叫做局部类 [local classes](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html). 。你同样可以在方法内定义一个未命名内部类，这样的类讲过匿名内部类 [anonymous classes](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html).。

## 限定修饰符

你对内部类使用同外部类其他成员一样的限定修饰符。例如，你可以使用特定的`private`,`public`,以及`protected`来显示对内部类的访问，同其他类的成员一样。