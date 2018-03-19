---
title: Java 学习指南_学习Java：基础-枚举类
date: 2018-03-19 18:51:59
tags: 
- java
- tutorial
- 教程
- 类
- enum
- 枚举类
categories:
- java
keywords:
- java
- 教程
- tutorial
- enum
- 枚举类
---

# 枚举类

枚举类型 *enum type* 是一种特殊的数据类型，可以使一个变量值为一组预定义的常量来。变量值必须等于预定义的常量值中的一个。常见的例子包括指南者中的方向(值 NORTH, SOUTH, EAST, and WEST) 以及一周中的每一天.

因为他们是常量，所以枚举类的成员都是用大写字母表示。

Java编程语言中，你可以使用`enum`关键字定义枚举类。例如，一周中的每一天可以定义如下:

```java
public enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY 
}
```

你可以在任何你想表达一组固定的常量集合时使用枚举类。包含了自然界中的列举类型例如太阳系中的行星以及任何你可能在编译时就知道的任何可能值—例如，菜单中的选项，命令行中的标记等等.

以下代码是如何使用上面定义的`Day`枚举类型:

```java
public class EnumTest {
    Day day;
    
    public EnumTest(Day day) {
        this.day = day;
    }
    
    public void tellItLikeItIs() {
        switch (day) {
            case MONDAY:
                System.out.println("Mondays are bad.");
                break;
                    
            case FRIDAY:
                System.out.println("Fridays are better.");
                break;
                         
            case SATURDAY: case SUNDAY:
                System.out.println("Weekends are best.");
                break;
                        
            default:
                System.out.println("Midweek days are so-so.");
                break;
        }
    }
    
    public static void main(String[] args) {
        EnumTest firstDay = new EnumTest(Day.MONDAY);
        firstDay.tellItLikeItIs();
        EnumTest thirdDay = new EnumTest(Day.WEDNESDAY);
        thirdDay.tellItLikeItIs();
        EnumTest fifthDay = new EnumTest(Day.FRIDAY);
        fifthDay.tellItLikeItIs();
        EnumTest sixthDay = new EnumTest(Day.SATURDAY);
        sixthDay.tellItLikeItIs();
        EnumTest seventhDay = new EnumTest(Day.SUNDAY);
        seventhDay.tellItLikeItIs();
    }
}
```

输出如下:

```java
Mondays are bad.
Midweek days are so-so.
Fridays are better.
Weekends are best.
Weekends are best.
```

Java编程语言中的枚举类型比其他语言中的要更加欠打。 `enum` 声明定义了一个类(交过枚举类型 *enum type*).枚举类型，类体也可以包含方法以及其他成员。编译器在创建枚举类型时会自动的增加一些特殊的代码。例如，他们有已个静态的`values`方法可以返回包含所有定义的枚举值的数据。这个方法通常与`for-each`结构结合使用，来迭代枚举类中的所有类型。例如，下面的代码 `Planet` 类例子遍历了太阳系中的所有行星.

```java
for (Planet p : Planet.values()) {
    System.out.printf("Your weight on %s is %f%n",
                      p, p.surfaceWeight(mass));
}
```

------

**注意**:所有的枚举类型简单的继承了类 `java.lang.Enum`。因为Java只能继承自一个类（参考 [Declaring Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/classdecl.html)).Java不支持多重继承 (参考 [Multiple Inheritance of State, Implementation, and Type](https://docs.oracle.com/javase/tutorial/java/IandI/multipleinheritance.html))，因此所有的枚举类都不能再继承任何类。

------

下面的例子中，`Planet`是一个枚举类，代表了太阳系中的所有行星.他们通过的常量属性质量和半径来定义。

每一个枚举常量定义的同时包含了质量与半径参数。这些参数在常量创建的时候传递给构造器。Java要求常量必须首先声明，优先与任何的成员和方法。因此，当枚举类有额外的字段和方法时，枚举常量结束时必须以分号semicolon结束.

------

**Note**:枚举类的构造器必须是私有级别或者是包级的访问权限。它将在自动创建定义在枚举类体开始的常量。你不能自己调用枚举类的构造方法。

------

另外，对于他的属性和构造器，`Planet`提供方法允许你获取每一个行星的表面重力以及重量。下面是一个简单的程序，获取你在地球的体重（任一单位）并计算出你在其他所有星球的体重（同样单位下）:

```java
public enum Planet {
    MERCURY (3.303e+23, 2.4397e6),
    VENUS   (4.869e+24, 6.0518e6),
    EARTH   (5.976e+24, 6.37814e6),
    MARS    (6.421e+23, 3.3972e6),
    JUPITER (1.9e+27,   7.1492e7),
    SATURN  (5.688e+26, 6.0268e7),
    URANUS  (8.686e+25, 2.5559e7),
    NEPTUNE (1.024e+26, 2.4746e7);

    private final double mass;   // in kilograms
    private final double radius; // in meters
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }
    private double mass() { return mass; }
    private double radius() { return radius; }

    // universal gravitational constant  (m3 kg-1 s-2)
    public static final double G = 6.67300E-11;

    double surfaceGravity() {
        return G * mass / (radius * radius);
    }
    double surfaceWeight(double otherMass) {
        return otherMass * surfaceGravity();
    }
    public static void main(String[] args) {
        if (args.length != 1) {
            System.err.println("Usage: java Planet <earth_weight>");
            System.exit(-1);
        }
        double earthWeight = Double.parseDouble(args[0]);
        double mass = earthWeight/EARTH.surfaceGravity();
        for (Planet p : Planet.values())
           System.out.printf("Your weight on %s is %f%n",
                             p, p.surfaceWeight(mass));
    }
}
```

如果你运行这个类 `Planet.class` 并且输入参数175, 可以说的如下输出:

```
$ java Planet 175
Your weight on MERCURY is 66.107583
Your weight on VENUS is 158.374842
Your weight on EARTH is 175.000000
Your weight on MARS is 66.279007
Your weight on JUPITER is 442.847567
Your weight on SATURN is 186.552719
Your weight on URANUS is 158.397260
Your weight on NEPTUNE is 199.207413
```