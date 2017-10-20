---
title: Java 学习指南_学习Java：基础-类-初始化字段
date: 2017-10-20 12:23:59
tags: 
- java
- tutorial
- 教程
- class
- 类
- Initializing Fields
- 初始化
categories:
- java
keywords:
- java
- 教程
- tutorial
- class
- 类
- Initializing Fields
- 初始化
---

# 初始化域

就像你看到的一样，你通常可以在一个字段/域定义的时候提供一个初始值:

```java
public class BedAndBreakfast {

    // initialize to 10
    public static int capacity = 10;

    // initialize to false
    private boolean full = false;
}
```

当初始化的值可用并且初始化可以在一行内完成时这么做都没有问题。不过，这样的初始化形式有一些使用限制因为它过于简单。如果初始化需要一些逻辑（例如，错误处理或者一个`for`循环来填充一个复合的数组）,简单的赋值就不适合了。实例变量可以在在构造器中实例化，这里也可以使用错误处理和逻辑。为了给类变量的初始化也提供这样的能力，Java编程语言包含了*静态代码块* *static initialization blocks*.

------

**注意**:  并不是一定要在类定义的开始就声明字段/域，尽管这是最通常的做法。只是要求它们在使用前必须声明和初始化。

------

## 静态代码块

`静态代码块`时在一个普通的`{ }`包括的代码块前面加上`static`关键字。下面是一个例子:

```java
static {
    // whatever code is needed for initialization goes here
}
```

一个类可以有多个静态代码块，并且它们可以出现在类体body的任何地方。运行环境确保所有的静态代码块按照它们在源代码中出现的顺序被调用。

静态代码块有个可替换的方法--你可以使用私有静态方法：

```java
class Whatever {
    public static varType myVar = initializeClassVariable();
        
    private static varType initializeClassVariable() {

        // initialization code goes here
    }
}
```

使用私有静态方法的好处是如果你需要重新初始化变量就可以重用它。

## 初始化实例成员Initializing Instance Members

 通常，你可以经初始化实例成员的代码放进一个构造器，同样还有两个方法可以达到这种目的，初始化代码块，以及final方法;

实例变量初始化代码块域静态代码块类似，不过少了`static`关键字:

```java
{
    // whatever code is needed for initialization goes here
}
```

Java编译器将初始化代码块复制到每一个构造器，因此使用这种方法的好处是可以在多个构造其中分享同一代码块。

 *final method* final方法 不可以被子类重写。在接口域与继承一颗中我们还会详细讨论。下面是一个使用final方法初始化实例变量的例子:

```java
class Whatever {
    private varType myVar = initializeInstanceVariable();
        
    protected final varType initializeInstanceVariable() {

        // initialization code goes here
    }
}

```

特别是当子类想要重用这个初始化方法的时候使用这种方法。使用final方法是因为在实例实例化的过程中调用非final的方法可能引起很多的问题。（思考）