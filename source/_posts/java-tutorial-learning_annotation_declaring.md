---
title: Java 学习指南_学习Java：定义一个注解类型
date: 2018-03-21 18:21:59
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

# 定义一个注解类型

许多注解代替代码中的注释。

假设一个软件组通常在类体的起始处填写注释已提供重要的信息:

```java
public class Generation3List extends Generation2List {

   // Author: John Doe
   // Date: 3/17/2002
   // Current revision: 6
   // Last modified: 4/12/2004
   // By: Jane Doe
   // Reviewers: Alice, Bill, Cindy

   // class code goes here

}
```

为了使用注解添加这些元数据，你必须先定义一个注解类型 *annotation type*. 其语法如下:

```java
@interface ClassPreamble {
   String author();
   String date();
   int currentRevision() default 1;
   String lastModified() default "N/A";
   String lastModifiedBy() default "N/A";
   // Note use of array
   String[] reviewers();
}
```

注解类型的定义看起来像是接口的定义，只不过关键字`interface`前面多了一个符号 (`@`) (@ = AT, 与注解的符号一样).

注解类型是接口 *interface*的一种格式后面的课程会讲到,现在你不需要理解接口。

上面的注解类型定义，类体中包含了注解类型元素 *annotation type element* 的定义,看起来像是方法，不过注意，他们可以定义默认值。

定义注解类型之后，你可以使用这个注解类型，并填入元素值，像下面这样:

```java
@ClassPreamble (
   author = "John Doe",
   date = "3/17/2002",
   currentRevision = 6,
   lastModified = "4/12/2004",
   lastModifiedBy = "Jane Doe",
   // Note array notation
   reviewers = {"Alice", "Bob", "Cindy"}
)
public class Generation3List extends Generation2List {

// class code goes here

}
```

------

**注意:** 为了是 `@ClassPreamble` 注解定义的元素出现在java文档生成器生成的文档中，你必须为 `@ClassPreamble` 注解的定义添加d `@Documented` 注解:

```
// import this to use @Documented
import java.lang.annotation.*;

@Documented
@interface ClassPreamble {

   // Annotation element definitions
   
}
```

------



