---
title: Java 学习指南_学习Java：基础-控制流程-switch 语句
date: 2017-09-20 16:00:59
tags: 
- java
- tutorial
- 教程
- switch
categories:
- java
keywords:
- java
- 教程
- tutorial
- switch
---

# switch 语句

与 `if-then` 和 `if-then-else` 语句不通, `switch`语句可以有一定数量的可能执行路径。  `switch` 可以对 `byte`, `short`, `char`, 以及 `int`p基本数据类型使用. 同样可以对*枚举类型*使用 (参考 [Enum Types](http://docs.oracle.com/javase/tutorial/java/javaOO/enum.html)), 字符串 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 类使用, 以及基本数据类型的包装类: [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html),[`Byte`](https://docs.oracle.com/javase/8/docs/api/java/lang/Byte.html), [`Short`](https://docs.oracle.com/javase/8/docs/api/java/lang/Short.html), 和 [`Integer`](https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html) (参考 [Numbers and Strings](http://docs.oracle.com/javase/tutorial/java/data/index.html)).

以下的代码示例中 [`SwitchDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/SwitchDemo.java), 声明了一个名为`mongth`的`int`。代码使用`switch`语句，根据`month`的值显示出月份的名字.

```java
public class SwitchDemo {
    public static void main(String[] args) {

        int month = 8;
        String monthString;
        switch (month) {
            case 1:  monthString = "January";
                     break;
            case 2:  monthString = "February";
                     break;
            case 3:  monthString = "March";
                     break;
            case 4:  monthString = "April";
                     break;
            case 5:  monthString = "May";
                     break;
            case 6:  monthString = "June";
                     break;
            case 7:  monthString = "July";
                     break;
            case 8:  monthString = "August";
                     break;
            case 9:  monthString = "September";
                     break;
            case 10: monthString = "October";
                     break;
            case 11: monthString = "November";
                     break;
            case 12: monthString = "December";
                     break;
            default: monthString = "Invalid month";
                     break;
        }
        System.out.println(monthString);
    }
}
```

本例中, `August` 被输出.

 `switch`语句的代码体也叫做 *switch block*s (switch代码块). `switch` 代码块中的语句可以用一个或者多个`case`或者 `default`标签分类。`switch`语句运算表达式的值，然后执行匹配的`case`标签后的所有语句。你同样可以使用`if-then-else`语句实现以上代码的功能:

```java
int month = 8;
if (month == 1) {
    System.out.println("January");
} else if (month == 2) {
    System.out.println("February");
}
...  // and so on
```

决定使用`if-then-else`语句还是`switch`语句取决于可读性以及语句所要测试的表达式。 `if-then-else` 语句可以用来检验基于值的范围或者条件的表达式，`switch`语句可以用来检验基于整数，枚举值，以及字符串`String`对象。

另外一个有趣的点时`break`语句.每一个`break`语句终结闭合的 `switch` 语句，控制流程继续跟随`switch`代码块的下一语句。`break`语句时必须的，如果为没有`break`语句，`switch`代码块 将会*fall through*跌穿（整段垮掉）:所有匹配的`case`标签之后的语句都会按照顺序执行，不管随后的`case`标签后的表达式是否匹配，直到遇见一个`break`语句。下面的程序 [`SwitchDemoFallThrough`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/SwitchDemoFallThrough.java) 展示了一个争端垮掉的 `switch`代码块. 程序显示了整数对应的月份以及一年当中随后的月份:

```java
public class SwitchDemoFallThrough {

    public static void main(String[] args) {
        java.util.ArrayList<String> futureMonths =
            new java.util.ArrayList<String>();

        int month = 8;

        switch (month) {
            case 1:  futureMonths.add("January");
            case 2:  futureMonths.add("February");
            case 3:  futureMonths.add("March");
            case 4:  futureMonths.add("April");
            case 5:  futureMonths.add("May");
            case 6:  futureMonths.add("June");
            case 7:  futureMonths.add("July");
            case 8:  futureMonths.add("August");
            case 9:  futureMonths.add("September");
            case 10: futureMonths.add("October");
            case 11: futureMonths.add("November");
            case 12: futureMonths.add("December");
                     break;
            default: break;
        }

        if (futureMonths.isEmpty()) {
            System.out.println("Invalid month number");
        } else {
            for (String monthName : futureMonths) {
               System.out.println(monthName);
            }
        }
    }
}
```

代码输出结果如下:

```java
August
September
October
November
December
```

技术上来说，最后一个`break`并不时必须的因为流程执行跌出`switch`语句。推荐使用一个`break`语句，这样可以使修改代码更加容易并且不容出错。`default`部分代码处理么有被任何一个`case`标签表明的其他任何值。

以下的示例代码中 [`SwitchDemo2`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/SwitchDemo2.java), 展示了如何在语句中使用多个`case`标签，代码计算指定月份的天数:

```java
class SwitchDemo2 {
    public static void main(String[] args) {

        int month = 2;
        int year = 2000;
        int numDays = 0;

        switch (month) {
            case 1: case 3: case 5:
            case 7: case 8: case 10:
            case 12:
                numDays = 31;
                break;
            case 4: case 6:
            case 9: case 11:
                numDays = 30;
                break;
            case 2:
                if (((year % 4 == 0) && 
                     !(year % 100 == 0))
                     || (year % 400 == 0))
                    numDays = 29;
                else
                    numDays = 28;
                break;
            default:
                System.out.println("Invalid month.");
                break;
        }
        System.out.println("Number of Days = "
                           + numDays);
    }
}
```

以下为代码的输出:

```
Number of Days = 29
```

## 在switch语句中使用字符串

Java SE 7以及之后的版本中，你可以在`switch`语句的表达式中使用字符串`String`对象。以下代码, [`StringSwitchDemo`](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/examples/StringSwitchDemo.java),根据字符串`month`的`String`值显示出对应月份的数字:

```java
public class StringSwitchDemo {

    public static int getMonthNumber(String month) {

        int monthNumber = 0;

        if (month == null) {
            return monthNumber;
        }

        switch (month.toLowerCase()) {
            case "january":
                monthNumber = 1;
                break;
            case "february":
                monthNumber = 2;
                break;
            case "march":
                monthNumber = 3;
                break;
            case "april":
                monthNumber = 4;
                break;
            case "may":
                monthNumber = 5;
                break;
            case "june":
                monthNumber = 6;
                break;
            case "july":
                monthNumber = 7;
                break;
            case "august":
                monthNumber = 8;
                break;
            case "september":
                monthNumber = 9;
                break;
            case "october":
                monthNumber = 10;
                break;
            case "november":
                monthNumber = 11;
                break;
            case "december":
                monthNumber = 12;
                break;
            default: 
                monthNumber = 0;
                break;
        }

        return monthNumber;
    }

    public static void main(String[] args) {

        String month = "August";

        int returnedMonthNumber =
            StringSwitchDemo.getMonthNumber(month);

        if (returnedMonthNumber == 0) {
            System.out.println("Invalid month");
        } else {
            System.out.println(returnedMonthNumber);
        }
    }
}
```

代码的输出结果为 `8`.

 `switch` 表达式的`String` 值 与`case`标签中对应的值进行比较，就像使用 [`String.equals`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#equals-java.lang.Object-) 方法。为了使`StringSwitchDemo` 可以接受所有忽略大小写的月份，`month`被转换为小写形式。(通过 [`toLowerCase`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#toLowerCase--) 方法),  并且`case`标签中对应的字符串值也全部为小写。

**注意**: 本例中，检查了`month`的值是否为`null`，确保任何switch语句中的任何表达式值不为`null`,方式抛`NullPointerException` 空指针异常.