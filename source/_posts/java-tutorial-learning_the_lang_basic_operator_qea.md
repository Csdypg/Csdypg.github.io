---
title: Java 学习指南_学习Java：运算符问题与练习
date: 2017-09-07 16:58:59
tags: 
- java
- tutorial
- 教程
- Operator
categories:
- java	
keywords:
- java
- 教程
- tutorial
- Operator
- 运算符
---

# 运算符问题与练习

## 问题

1. 观察以下代码片段.

   ```
   arrayOfInts[j] > arrayOfInts[j+1]

   ```

   包含了那些运算符?

2. 观察以下代码片段.

   ```
   int i = 10;
   int n = i++%5;

   ```

   1. 代码执行以后 `i` 和 `n` 的值应该是什么?
   2. 如果用前置自增操作符(`++i)`)，取代后置自增操作符 (`i++`),  `i` and `n` 的最终值应该是什么?

3. 为了反转一个`boolean`, 应该使用哪一个操作符?

4. 哪一个运算符是位了比较两个对象的值, `=` 还是 `==` ?

5. 解释后面的代码片段: `result = someCondition ? value1 : value2;`

## 练习

1. 将一下代码改变位符合运算符为变量赋值:

   ```java
   class ArithmeticDemo {

        public static void main (String[] args){
             
             int result = 1 + 2; // result is now 3
             System.out.println(result);

             result = result - 1; // result is now 2
             System.out.println(result);

             result = result * 2; // result is now 4
             System.out.println(result);

             result = result / 2; // result is now 2
             System.out.println(result);

             result = result + 8; // result is now 10
             result = result % 7; // result is now 3
             System.out.println(result);
        }
   }
   ```

2. 以下代码中，解释 "6"为什么被打印了两次:
   ```java
   class PrePostDemo {
       public static void main(String[] args){
           int i = 3;
           i++;
           System.out.println(i);    // "4"
           ++i;                     
           System.out.println(i);    // "5"
           System.out.println(++i);  // "6"
           System.out.println(i++);  // "6"
           System.out.println(i);    // "7"
       }
   }
   ```

<!-- more-->

# 答案

## 问题答案

1. 观察以下代码片段:
   ```java
   arrayOfInts[j] > arrayOfInts[j+1]
   ```

   问题:代码中包含了那些运算符?

   答案:

   ```
   >
   ```

   ```
   +
   ```

2. 观察一下代码片段:

   ```
   int i = 10;
   int n = i++%5;
   ```

   1. **Question:** 代码执行以后 `i` 和 `n` 的值应该是什么?

      **Answer:** `i` 11,  `n`  0.

   2. **Question:** 如果用前置自增操作符(`++i)`)，取代后置自增操作符 (`i++`),  `i` and `n` 的最终值应该是什么?
      **Answer:** `i` 11,  `n`  1.

3. **Question:**为了反转一个`boolean`, 应该使用哪一个操作符??
   **Answer:** 逻辑否 "!".

4. **Question**: 哪一个运算符是位了比较两个对象的值, `=` 还是 `==`  ?
   **Answer:** The `==` 比较,  `=` 赋值.

5. **Question:** 解释以下代码: `result = someCondition ? value1 : value2;`
   **Answer:**代码可以读作: "如果 `someCondition` 为 `true`, 将 `value1` 复制给 `result`. 否则,将 `value2` 赋值给 `result`."

## 练习


## 练习答案

1. 将一下代码改变位符合运算符为变量赋值:
   ```java
   class ArithmeticDemo {

       public static void main (String[] args){

           int result = 1 + 2; // result is now 3
           System.out.println(result);
    
           result = result - 1; // result is now 2
           System.out.println(result);
    
           result = result * 2; // result is now 4
           System.out.println(result);
    
           result = result / 2; // result is now 2
           System.out.println(result);
    
           result = result + 8; // result is now 10
           result = result % 7; // result is now 3
           System.out.println(result);
    
       }
   }
   ```

   一种解法:

   ```java
   class ArithmeticDemo {

       public static void main (String[] args){
           int result = 3;
           System.out.println(result);
    
           result -= 1; // result is now 2
           System.out.println(result);
    
           result *= 2; // result is now 4
           System.out.println(result);
    
           result /= 2; // result is now 2
           System.out.println(result);
    
           result += 8; // result is now 10
           result %= 7; // result is now 3
           System.out.println(result);
    
       }
   }
   ```

2. 以下代码中，解释 "6"为什么被打印了两次:

   ```
   class PrePostDemo {
       public static void main(String[] args){
           int i = 3;
           i++;
           System.out.println(i);    // "4"
           ++i;                     
           System.out.println(i);    // "5"
           System.out.println(++i);  // "6"
           System.out.println(i++);  // "6"
           System.out.println(i);    // "7"
       }
   }
   ```

   代码


   ```
   System.out.println(++i);
   ```

​    

  计算结果 6, 因为前缀版的

​    

   ```
   ++
   ```

​    

   本行计算出已经增加的结果，下一行,

​    

   ```
   System.out.println(i++);
   ```

​    

 本行计算出当前的结果, 然后再增加1.因此7在下一行才会打印.
   ```
System.out.println(i);
   ```

