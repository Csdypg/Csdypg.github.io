---
title: Java 学习指南_学习Java：基础-局部类
date: 2017-10-24 14:51:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- Local Class
- 局部类
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- Local Class
- 局部类
---

# 局部类Local Classes

局部类是指定义在一个代码块*block*中的类，一组包含与`{}`之内的一组语句。

本节包含了以下内容:

- 定义一个局部类[Declaring Local Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html#declaring-local-classes)
- 访问所属类的成员Accessing Members of an Enclosing Class
  - 遮蔽与局部类[Shadowing and Local Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html#shadowing-and-local-classes)
- 局部类与内部类相似[Local Classes Are Similar To Inner Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html#local-classes-are-similar-to-inner-classes)

## 定义局部类[Declaring Local Classes]()

你可以在任何代码块中定义局部类(参考 [Expressions, Statements, and Blocks](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/expressions.html) 表达式，语句代码块获取更多的信息).例如:你可以在一个方法体内，一个`for`循环内或者一个`if`语句中定义局部类。

下面的例子, [`LocalClassExample`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/LocalClassExample.java),验证了两个电话号码。他在方法`validatePhoneNumber`方法内定义了一个局部类`PhoneNumber`:

```java
public class LocalClassExample {
  
    static String regularExpression = "[^0-9]";
  
    public static void validatePhoneNumber(
        String phoneNumber1, String phoneNumber2) {
      
        final int numberLength = 10;
        
        // Valid in JDK 8 and later:
       
        // int numberLength = 10;
       
        class PhoneNumber {
            
            String formattedPhoneNumber = null;

            PhoneNumber(String phoneNumber){
                // numberLength = 7;
                String currentNumber = phoneNumber.replaceAll(
                  regularExpression, "");
                if (currentNumber.length() == numberLength)
                    formattedPhoneNumber = currentNumber;
                else
                    formattedPhoneNumber = null;
            }

            public String getNumber() {
                return formattedPhoneNumber;
            }
            
            // Valid in JDK 8 and later:

//            public void printOriginalNumbers() {
//                System.out.println("Original numbers are " + phoneNumber1 +
//                    " and " + phoneNumber2);
//            }
        }

        PhoneNumber myNumber1 = new PhoneNumber(phoneNumber1);
        PhoneNumber myNumber2 = new PhoneNumber(phoneNumber2);
        
        // Valid in JDK 8 and later:

//        myNumber1.printOriginalNumbers();

        if (myNumber1.getNumber() == null) 
            System.out.println("First number is invalid");
        else
            System.out.println("First number is " + myNumber1.getNumber());
        if (myNumber2.getNumber() == null)
            System.out.println("Second number is invalid");
        else
            System.out.println("Second number is " + myNumber2.getNumber());

    }

    public static void main(String... args) {
        validatePhoneNumber("123-456-7890", "456-7890");
    }
}
```

这个例子通过两部验证一个电话号码，首先将电话号码中所有除了0-9的数字一处，然后检查电话号码是否包含了10个数字（北美的电话号码长度）.例子的输出如下：

```
First number is 1234567890
Second number is invalid
```

## 局部类访问你所处类的成员[Accessing Members of an Enclosing Class]()

局部类有访问其所处类成员的权限。前面的例子中，`PhoneNumber`构造器访问了成员 `LocalClassExample.regularExpression`. 另外，局部类有访问局部变量的权限。不过，局部类只能访问被声明未`final`的局部变量。当一个局部类访问一个局部变量或者时所处代码块的参数时，它捕获*captures*了那个变量或者参数。例如，`PhoneNumber`构造器可以访问局部变量`numberLength`因为他是定义未`final`的；`numberLength`是一个*捕获变量*captured *variable*.

然而你，Java SE 8开始，可以访问所属代码块中定义未final或者有效最终*effectively final*的变量以及参数.例如，假设变量`numberLength`没有被声明为`final`，并且在`PhoneNumber`的构造其中加了如下的代码，将其变量值改变为数字7：

```java
PhoneNumber(String phoneNumber) {
    numberLength = 7;
    String currentNumber = phoneNumber.replaceAll(
        regularExpression, "");
    if (currentNumber.length() == numberLength)
        formattedPhoneNumber = currentNumber;
    else
        formattedPhoneNumber = null;
}
```

因为这个赋值语句，变量`numberLength`就是不再时一个有效最终值。这样做的结果就是，当`PhoneNumber`类尝试引用局部变量 `numberLength`时， Java编译器生成一个错误信息，类似“local variable referenced from an inner class must be final or effectively final”（内部类中引用的局部变量必须是一个最终或或者一个等效最终值）

```
if (currentNumber.length() == numberLength)
```

从Java SE 8开始，你再一个方法中定义局部变量时，他可以访问方法的参数。例如，你可以再局部类`PhoneNumber`中定义如下方法:

```java
public void printOriginalNumbers() {
    System.out.println("Original numbers are " + phoneNumber1 +
        " and " + phoneNumber2);
}
```

方法`printOriginalNumbers`方位了方法 `validatePhoneNumber`的两个参数 `phoneNumber1` 以及`phoneNumber2` 。

### [局部类与遮蔽Shadowing and Local Classes]()

再局部类中声明一个类型（譬如变量）遮蔽其所在闭合范围内拥有相同名字的类型。参考遮蔽 [Shadowing](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html#shadowing) 获取更多信息。

## [局部类与内部类相似Local Classes Are Similar To Inner Classes]()

局部类与内部类相似，因为它们都不定义任何的静态static成员。局部类如果再静态方法内，譬如 `PhoneNumber`类,定义再静态方法 `validatePhoneNumber`中,就只能引用闭合范围内的静态成员。如果你不讲成员变量 `regularExpression` 定义为静态static,那么Java编译器就会生成一个错误， "non-static variable `regularExpression` cannot be referenced from a static context."（非静态变量`regularExpression`不能再一个静态的上下文中引用)

局部类是非静态的，因为它可以方法所属闭合代码块中的实例变量。因此它们几乎不能包含任何类型的静态声明。

你不能再一个代码块中定义接口，因为接口再本质上静态的。例如，下面的代码引用是不能编译的因为接口`HelloThere`被定义再方法`greetInEnglish`方法体中:

```java
    public void greetInEnglish() {
        interface HelloThere {
           public void greet();
        }
        class EnglishHelloThere implements HelloThere {
            public void greet() {
                System.out.println("Hello " + name);
            }
        }
        HelloThere myGreeting = new EnglishHelloThere();
        myGreeting.greet();
    }
```

你不能再一个局部类中定义静态的初始化器或者成员。以下的代码不能通过编译，因为方法 `EnglishGoodbye.sayGoodbye` 被声明为 `static`. 当遇到这种方法定义时编译器会生成一个错误类似 "modifier 'static' is only allowed in constant variable declaration"（限定符static只能用再常量的声明上） :

```java
    public void sayGoodbyeInEnglish() {
        class EnglishGoodbye {
            public static void sayGoodbye() {
                System.out.println("Bye bye");
            }
        }
        EnglishGoodbye.sayGoodbye();
    }
```

局部类可以有静态成员除非时常量. (常量 *constant variable*是一个定义为final的基本数据类型或者String字符串类型的变量初始化为一个编译时的常量表达式。编译时常量表达式同时时一个字符串或者时编译时可以计算的运算表达式。参考理解成员变量[Understanding Class Members](https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html) 获取更多信息.) 以下代码摘绿可以通过编译，因为静态成员 `EnglishGoodbye.farewell` 是一个常量:

```java
    public void sayGoodbyeInEnglish() {
        class EnglishGoodbye {
            public static final String farewell = "Bye bye";
            public void sayGoodbye() {
                System.out.println(farewell);
            }
        }
        EnglishGoodbye myEnglishGoodbye = new EnglishGoodbye();
        myEnglishGoodbye.sayGoodbye();
    }
```