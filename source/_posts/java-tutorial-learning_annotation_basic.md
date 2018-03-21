---
title: Java 学习指南_学习Java：注解基础
date: 2018-03-21 17:26:59
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

# 注解基础

## 注解的格式

最贱的注解格式实例如下:

```java
@Entity
```

标志符号 (`@`) 向编译器表示紧跟着的信息是注解，下面的例子注解的名字为`Override`:

```java
@Override
void mySuperMethod() { ... }
```

注解可以包含元素 *elements*,可以是署名的，也可以是匿名的，元素有对应的值:

```java
@Author(
   name = "Benjamin Franklin",
   date = "3/27/2003"
)
class MyClass() { ... }
```

或者

```java
@SuppressWarnings(value = "unchecked")
void myMethod() { ... }
```

如果只有一个名为`value`的元素，那么元素署名可以省略，如下:

```java
@SuppressWarnings("unchecked")
void myMethod() { ... }
```

如果注解不包含元素，那么小括号也可以移除，就像之前的`@Override`注解.

也可以在统一个声明或者定义处使用多个注解:

```java
@Author(name = "Jane Doe")
@EBook
class MyClass { ... }
```

如果多个注解拥有同样的类型，叫做重复注解repeating annotation:

```java
@Author(name = "Jane Doe")
@Author(name = "John Smith")
class MyClass { ... }
```

重复注解在Java SE8中支持的，获取更多相关信息可以参看 [Repeating Annotations](https://docs.oracle.com/javase/tutorial/java/annotations/repeating.html).

注解类型可以是`java.lang`或者`java.lang.annotation`包中的一种。之前的例子中`Override` and `SuppressWarnings` 是 [预定义注解predefined Java annotations](https://docs.oracle.com/javase/tutorial/java/annotations/predefined.html).你也可以定义自己的注解类型， `Author` 和 `Ebook` 注解是自定义注解类型。

## 注解可以用在哪里

注解可以用定义：类，字段，方法以及其他编程元素定义时可以使用。挡在定义时使用注解，按照惯例每一个注解占一行.

Java SE8 版本中，注解同样可以应用在类型使用时，以下是一些列子:

- 类型实例创建表达式:

  ```
      new @Interned MyObject();
  ```

- 类型转换:

  ```
      myString = (@NonNull String) str;
  ```

- `implements` 引用时:

  ```
      class UnmodifiableList<T> implements
          @Readonly List<@Readonly T> { ... }
  ```

- 声明抛出异常时:

  ```
      void monitorTemperature() throws
          @Critical TemperatureException { ... }
  ```

这种形式的注解叫做类型注解 *type annotation*.获取更多相关信息，参考 [类型注解与插件式类型系统Type Annotations and Pluggable Type Systems](https://docs.oracle.com/javase/tutorial/java/annotations/type_annotations.html).