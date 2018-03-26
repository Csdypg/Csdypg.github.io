---
title: Java 学习指南_学习Java：注解-问题与练习
date: 2018-03-26 12:26:59
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

# 问题与练习: 注解

## 问题

1. 问题: 线面的接口有哪些错误:

   ```java
   public interface House {
       @Deprecated
       public void open();
       public void openFrontDoor();
       public void openBackDoor();
   }
   ```

   ​

2. **问题**: 考虑下面的 `House` 类，实现了问题1中的借口.

   ```java
   public class MyHouse implements House {
       public void open() {}
       public void openFrontDoor() {}
       public void openBackDoor() {}
   }
   ```

   如果你编译这个程序，编译器会产生警告，因为`open`方法是反对的（在接口中），你应该做什么来避免警告？

3. 下面的代码在编译时是否会发生错误？为什么？

   ```java
   public @interface Meal { ... }

   @Meal("breakfast", mainDish="cereal")
   @Meal("lunch", mainDish="pizza")
   @Meal("dinner", mainDish="salad")
   public void evaluateDiet() { ... }
   ```

## 练习

1. 练习: 定义一个增强请求的注解类型，包含元素`id`,`synopsis`,`engineer`, 以及`date`. 设定engineer默认值为`unassigned`，date默认值为`unknown`.



# 问题与练习答案: 注解

<!--more -->

## 问题答案

1. 问题: 线面的接口有哪些错误:

   ```java
   public interface House {
       @Deprecated
       public void open();
       public void openFrontDoor();
       public void openBackDoor();
   }
   ```

   **答案** 文档应该反映出 `open` 为什么是反对的以及用什么来代替，例如:

   ```java
   public interface House { 
       /**
        * @deprecated use of open 
        * is discouraged, use
        * openFrontDoor or 
        * openBackDoor instead.
        */
       @Deprecated
       public void open(); 
       public void openFrontDoor();
       public void openBackDoor();
   }
   ```

2. **问题**: 考虑下面的 `House` 类，实现了问题1中的借口.

   ```java
   public class MyHouse implements House {
       public void open() {}
       public void openFrontDoor() {}
       public void openBackDoor() {}
   }
   ```

   如果你编译这个程序，编译器会产生警告，因为`open`方法是反对的（在接口中），你应该做什么来避免警告？

   **答案**: 你可以为`open`方法的实现添加deprecate注解:

   ```java
   public class MyHouse implements House { 
       // The documentation is 
       // inherited from the interface.
       @Deprecated
       public void open() {} 
       public void openFrontDoor() {}
       public void openBackDoor() {}
   }
   ```

   同样，你也可以通过`@SuppressWarings`注解镇压这个警告:

   ```java
   public class MyHouse implements House { 
       @SuppressWarnings("deprecation")
       public void open() {} 
       public void openFrontDoor() {}
       public void openBackDoor() {}
   }
   ```

3. 下面的代码在编译时是否会发生错误？为什么？

   ```java
   public @interface Meal { ... }

   @Meal("breakfast", mainDish="cereal")
   @Meal("lunch", mainDish="pizza")
   @Meal("dinner", mainDish="salad")
   public void evaluateDiet() { ... }
   ```

   **答案**:代码将会编译失败。JDK8之前，重复注解是不支持的。JDK8中，同样会编译失败，因为`Meal`注解类型并没有声明为可重复的。可以通过添加 `@Repeatable` 元注解，并定义一个注解容器类型来修复这个问题:

   ```java
   @java.lang.annotation.Repeatable(MealContainer.class)
   public @interface Meal { ... }

   public @interface MealContainer {
       Meal[] value();
   }
   ```

## 练习答案

1. 练习: 定义一个增强请求的注解类型，包含元素`id`,`synopsis`,`engineer`, 以及`date`. 设定engineer默认值为`unassigned`，date默认值为`unknown`.

   答案:

   ```
   /**
    * Describes the Request-for-Enhancement (RFE) annotation type.
    */
   public @interface RequestForEnhancement {
       int id();
       String synopsis();
       String engineer() default "[unassigned]";
       String date() default "[unknown]";
   }
   ```