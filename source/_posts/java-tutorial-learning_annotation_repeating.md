---
title: Java 学习指南_学习Java：可重复注解
date: 2018-03-23 12:26:59
tags: 
- java
- tutorial
- 教程
- 注解
- annotation
categories:
- java
keywords:
- java
- 教程
- tutorial
- 注解
- annotation
---

# Repeating Annotations

#可重复注解

有时候你需要在定义或者类型使用时多次使用同一个注解。Java8中*repeating annotations* 可以实现.



例如，你在写一个程序，使用一个定时服务，是你的方法可以在特定的时间或者按着确切的调度计划执行。类似于UNIX系统的 `cron` 服务.现在你想要设置一个定时器来运行方法, `doPeriodicCleanup`, 在每个月的最后一天和每个周五的晚上11点。为了是计时器生效，创建`@Schedule`注解并在方法 `doPeriodicCleanup`方法上使用两次。第一次明确每个月的最后一天，第二个明确在每个周五晚上11点，一下是代码实例:

```java
@Schedule(dayOfMonth="last")
@Schedule(dayOfWeek="Fri", hour="23")
public void doPeriodicCleanup() { ... }
```

上一个例子在方法上使用了同一个注解两次。你可以在使用标准注解的任何地方重复注解。例如，你有一个处理访问权限的异常的类。使用一个 `@Alert` 注解作用于客户经理，另一个作用于管理员:

```java
@Alert(role="Manager")
@Alert(role="Administrator")
public class UnauthorizedAccessException extends SecurityException { ... }
```

因为共存的原因，重复注解存储在有Java 编译器自动生成的的注解容器 *container annotation* 中。想要实现这种功能，需要在代码中做两处声明。

## Step 1: 定义一个可重复的注解类型

注解类型必须由 `@Repeatable`元注解标注 meta-annotation. 下面的例子定义了一个自定义的 `@Schedule`可重负注解类型:

```java
import java.lang.annotation.Repeatable;

@Repeatable(Schedules.class)
public @interface Schedule {
  String dayOfMonth() default "first";
  String dayOfWeek() default "Mon";
  int hour() default 12;
}
```

元注解 `@Repeatable` meta-annotation的值,包含在括号里, 是Java编译器自动生成的存储重复注解的注解容器的类型。本例中注解容器的类型是 `Schedules`,因此重复注解 `@Schedule` 存储在 `@Schedules` 注解中.

没有声明注解类型为可重复时而多次使用会导致编译时错误。

## Step 2: 声明注解容器类型

注解容器类型必须有一个 `value`元素，元素为数组类型.数组的组件类型必须是可重复注解类型。注解容器 `Schedules` 类型定义如下:

```java
public @interface Schedules {
    Schedule[] value();
}
```

## 获取注解Retrieving Annotations

在反射接口 Reflection API中有几种可以取出注释的方法。方法的作用是返回一个单独的注解，例如[AnnotatedElement.getAnnotation(Class)](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html#getAnnotation-java.lang.Class-), 如果请求的注解类型只存在一个，那么结果不会改变，仍然只返回一个注解。如果某注解类型的注解存在多个，则要先获取他们的注解容器类型。这样，遗留代码仍然可以继续生效。在Java SE 8 中引入了其他的方法，可以通过注解容器一次性返回多个注解，例如[AnnotatedElement.getAnnotationsByType(Class)](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html#getAnnotationsByType-java.lang.Class-). 参考[AnnotatedElement](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) 类的详细介绍获取更多可用方法的信息。

## 设计思路Design Considerations

当设计一个注解类型时，你必须要考虑这种注解类型的注解基数*cardinality*。可以使用注解零次，一次，或者如果注解类型被标记为`@Repeatable`可以使用多次。同样可以通过@Target元注解可以显示注解类型使用的地方。例如，你可以创建一个只用于方法或者字段的可冲入注解。仔细的设计你的注解类型已保证开发者更加有弹性的使用注解，并发挥强大作用，这是非常重要的。