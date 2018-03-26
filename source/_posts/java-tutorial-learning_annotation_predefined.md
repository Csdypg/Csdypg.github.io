---
title: Java 学习指南_学习Java：预定义的注解类型
date: 2018-03-23 11:26:59
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

# 预定义的注解类型

Java SE API 预定义了一系列的注解类型。一些是被Java编译器使用，另外一是应用于其他注解(注解的注解).

## Java语言使用的注解

`java.lang` 包中所定义的注解类型有 `@Deprecated`, `@Override`, 以及 `@SuppressWarnings`.

**@Deprecated** [`@Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html) 注解表明了标注的元素是不推荐的并且不应该再继续使用。无论什么时候程序使用了有该标记的类，方法，字段，编译器都会产生一个警告。如果元素标记了`@Deprecated`那么他的主时钟也必须是用Java文档 `@deprecated` 标签，正如下面的例子。在Java文档注释中使用符号`@`与注解中一样并不是巧合的coincidental：他们是关联的概念。不过，要注意，Java文档注释里的标签首字母为小写`d`注解中首字母为`D`.

```java
   // Javadoc comment follows
    /**
     * @deprecated
     * explanation of why it was deprecated
     */
    @Deprecated
    static void deprecatedMethod() { }
}
```

**@Override** [`@Override`](https://docs.oracle.com/javase/8/docs/api/java/lang/Override.html)  注解告知编译器元素是为了复写在父类中定义的元素。复写方法将会在[接口与继承Interfaces and Inheritance](https://docs.oracle.com/javase/tutorial/java/IandI/index.html)一篇中讨论到.

```java
   // mark method as a superclass method
   // that has been overridden
   @Override 
   int overriddenMethod() { }
```

当复写方法的时候并不是必须要使用这个注解，他可以帮助你预防错误。如果标记了`@Override`标记的方法没有正确的复写他父类中的一个方法，编译器就会产生错误。

**@SuppressWarnings** [`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html) 注解告诉编译器，阻止可能产生的特定的警告。下面的例子中，使用了一个不推荐的方法，编译器通常会生成一个警告。在这种情况下，使用这个注解就可以阻止产生警告.

```java
   // use a deprecated method and tell 
   // compiler not to generate a warning
   @SuppressWarnings("deprecation")
    void useDeprecatedMethod() {
        // deprecation warning
        // - suppressed
        objectOne.deprecatedMethod();
    }
```

每一个编译器警告属于一个分类。Java语言明确列出了两类警告： `deprecation` 以及 `unchecked`. 

 `unchecked`警告，当遇到泛型 [generics](https://docs.oracle.com/javase/tutorial/java/generics/index.html)出现之前的遗留代码时可能会出现。 如果要阻止多个类型的警告，参考以下语法:

```
@SuppressWarnings({"unchecked", "deprecation"})
```

**@SafeVarargs** [`@SafeVarargs`](https://docs.oracle.com/javase/8/docs/api/java/lang/SafeVarargs.html) 注解，当使用在一个构造器或者方法时，断定该方法在使用可变参数时没有潜在的不安全因素。使用了该注解，与 `varargs`可变参数使用相关的未检查警告可以被阻止。

**@FunctionalInterface** [`@FunctionalInterface`](https://docs.oracle.com/javase/8/docs/api/java/lang/FunctionalInterface.html) 功能接口注解，在Java SE8中引入。表明是一个功能接口，与Java语言标准中定义的功能接口一样.

## 用于其他注解的注解

用于其注解的注解叫做元注解*meta-annotations*. `java.lang.annotation`中定义了数个元注解.

**@Retention** [`@Retention`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/Retention.html) 保留注解表明了注解是如何被存储的:

- `RetentionPolicy.SOURCE` – 该标记表明注解只在资源层面被保留，编译器会忽略.
- `RetentionPolicy.CLASS` – 该标记表明注解在编译时被保留，JVM会忽略.
- `RetentionPolicy.RUNTIME` – 该标记表明注解会被JVM保留，可以再运行时使用.

**@Documented** [`@Documented`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/Documented.html) 文档注解，表明使用了对应注解的元素，会被Java文档工具Javadoc tool使用。(默认情况下，注解不会被包含在Java文档中)。参考Java文档工具页面 [Javadoc tools page](https://docs.oracle.com/javase/8/docs/technotes/guides/javadoc/index.html)，获取更多相关信息.

**@Target** [`@Target`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/Target.html) 注解，限制了限制了注解可以应用于那种Java元素类型。目标注解可以使用如下的元素类型作为它的值:

- `ElementType.ANNOTATION_TYPE` 可以应用于注解类型.
- `ElementType.CONSTRUCTOR` 可以应用于构造器.
- `ElementType.FIELD` 可以应用于字段或者属性（字段、枚举的常量）.
- `ElementType.LOCAL_VARIABLE` 可以应用于局部变量.
- `ElementType.METHOD` 可以应用于方法级别的注解.
- `ElementType.PACKAGE` 可以应用于包的定义.
- `ElementType.PARAMETER` 可以应用于方法的参数。
- ElementType.TYPE 可以应用于任何的类（接口、类、枚举、注解）。

**@Inherited** [`@Inherited`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/Inherited.html) 继承注解表明，注解类型可以用从器的父类继承。(默认是不可以继承的)，当用户查询类的注解类型而类本身没有该注解时，就会查询其父类是否有该注解。这个注解只能使用与类的定义.

**@Repeatable** [`@Repeatable`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/Repeatable.html) 可重复的注解，在Java SE 8中引入，表明该注解在同一个声明或者类型处可以使用不止一次。参考可重复注解 [Repeating Annotations](https://docs.oracle.com/javase/tutorial/java/annotations/repeating.html).