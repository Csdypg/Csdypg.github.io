---
title: Java 学习指南_学习Java：基础-匿名类
date: 2017-12-4 14:51:59
tags: 
- java
- tutorial
- 教程
- 类
- class
- Anonymous Classe
- 匿名类
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- class
- Anonymous Classe
- 匿名类
---

# 匿名类Anonymous Classes

# Anonymous Classes

匿名类可以是你的代码更加简。你可以同时声明和实例化一个匿名类。匿名类与局不累很想，只不过没有名字。如果你只想使用一个局部类一次，就可以是用匿名类。

本节包含了一下主题:

- [声明匿名类](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html#declaring-anonymous-classes)
- [匿名类的语法](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html#syntax-of-anonymous-classes)
- [访问闭合范围内的局部变量，以及声明和访问匿名类的成员](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html#accessing)
- [匿名类的实例](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html#examples-of-anonymous-classes)

## [声明匿名类]()

局不类是声明，而匿名类是表达式，意思是你在另外一个表达式中定义这个类。下面的例子,[`HelloWorldAnonymousClasses`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/HelloWorldAnonymousClasses.java), 在局部变量 `frenchGreeting` 以及`spanishGreeting`的初始化过程中使用了匿名类,而 而局部变量 `englishGreeting`的声明则使用的局部类：

```java
public class HelloWorldAnonymousClasses {
  
    interface HelloWorld {
        public void greet();
        public void greetSomeone(String someone);
    }
  
    public void sayHello() {
        
        class EnglishGreeting implements HelloWorld {
            String name = "world";
            public void greet() {
                greetSomeone("world");
            }
            public void greetSomeone(String someone) {
                name = someone;
                System.out.println("Hello " + name);
            }
        }
      
        HelloWorld englishGreeting = new EnglishGreeting();
        
        HelloWorld frenchGreeting = new HelloWorld() {
            String name = "tout le monde";
            public void greet() {
                greetSomeone("tout le monde");
            }
            public void greetSomeone(String someone) {
                name = someone;
                System.out.println("Salut " + name);
            }
        };
        
        HelloWorld spanishGreeting = new HelloWorld() {
            String name = "mundo";
            public void greet() {
                greetSomeone("mundo");
            }
            public void greetSomeone(String someone) {
                name = someone;
                System.out.println("Hola, " + name);
            }
        };
        englishGreeting.greet();
        frenchGreeting.greetSomeone("Fred");
        spanishGreeting.greet();
    }

    public static void main(String... args) {
        HelloWorldAnonymousClasses myApp =
            new HelloWorldAnonymousClasses();
        myApp.sayHello();
    }            
}
```

## [匿名类的语法Syntax of Anonymous Classes]()

就像之前提到的一样，一个匿名类是一个表达式。匿名类表达式的语法类似调用一个构造器，不过在后边多了定义类的代码块。

参考一下 `frenchGreeting` 对象的实例:

```java
        HelloWorld frenchGreeting = new HelloWorld() {
            String name = "tout le monde";
            public void greet() {
                greetSomeone("tout le monde");
            }
            public void greetSomeone(String someone) {
                name = someone;
                System.out.println("Salut " + name);
            }
        };
```

匿名类表达式由一下几部分组成:

-  `new` 操作符
-  一个用来实现的接口或者用来继承的类的名称。本例中，匿名类为接口`HelloWorld` 的实现。
-  包含构造器参数的圆括号，类似普通的类创建实例表达式。**注意：** 当你实现一个接口时，没有构造器，所以你使用一个空的圆括号。
-  一个类体，包括了类的定义。需要注意的事，在类体中可以允许方法声明，但是不允许有语句。

因为匿名类的定义是一个表达式，他必须是语句的一部分。在本例中，匿名类表达式是实例化`frenchGreeting`对象语句的一部分。（这也解释了为什么需要在闭合的大括号后面需要一个分号）



## [访问闭合氛围内的局部变量，以及声明和访问匿名类的成员]()

就像局不类一样，匿名类可以 [捕获变量capture variables](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html#accessing-members-of-an-enclosing-class);他们对于闭合范围内的局部变量具有相同的访问权限:

- 匿名类可以访问他的闭合类的成员。
- 匿名类不能访问他所属闭合范围内定义不是`final`或者等效于与`final`的局部变量。
- 与嵌套类一样，在匿名类中声明某一类型的变量会遮蔽它所属闭合范围内的其它名字相同的变量。参考 [遮蔽Shadowing](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html#shadowing)以获取更多信息。

匿名类与局不累一样对它自己的成员访问有一些限制:

- 你不能在匿名类中定义静态的初始化器或者是成员接口.
- 匿名类中可以是用静态成员来定义常量。

注意你可以在匿名类中定义以下内容:

- 字段/属性Fields
- 扩展方法（尽管他们没有实现任何父类的方法）
- 实例初始化器
- 局不类

不过你不能再匿名类中定义构造器.

## [匿名类的实例Examples of Anonymous Classes]()

匿名类经常在图形界面的应用中使用。

参考下列JavaFX 列子 [`HelloWorld.java`](https://docs.oracle.com/javase/8/javafx/get-started-tutorial/hello_world.htm) (摘自 [Hello World, JavaFX Style](https://docs.oracle.com/javase/8/javafx/get-started-tutorial/hello_world.htm) 中 [Getting Started with JavaFX](https://docs.oracle.com/javase/8/javafx/get-started-tutorial/javafx_get_started.htm)). 这个例子创建了一个报刊了 **Say 'Hello World'**按钮的框架 :

```java
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;
 
public class HelloWorld extends Application {
    public static void main(String[] args) {
        launch(args);
    }
    
    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Hello World!");
        Button btn = new Button();
        btn.setText("Say 'Hello World'");
        btn.setOnAction(new EventHandler<ActionEvent>() {
 
            @Override
            public void handle(ActionEvent event) {
                System.out.println("Hello World!");
            }
        });
        
        StackPane root = new StackPane();
        root.getChildren().add(btn);
        primaryStage.setScene(new Scene(root, 300, 250));
        primaryStage.show();
    }
}
```

本例中I，方法调用`btn.setOnAction` 定义了当你选择**Say 'Hello World'**按钮的时候回发生什么.这个方法要求一个 `EventHandler<ActionEvent>`类型的对象.  `EventHandler<ActionEvent>`接口仅包含一个方法，handle。这里没有重新定义一个类来实现这个方法，而是直接使用了匿名类表达式。注意这个表达式是传递给`btn.setOnAction` 方法的参数.

因为 `EventHandler<ActionEvent>` 接口仅仅包含一个方法,你同样可以使用lambda表达式来代替匿名类表达式. 参考[Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 章节来获取更多信息.

匿名类是用来实现包含有两个或多个方法接口的理想方法。下面的例子JavaFX example 来自Customization of UI Controls](https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/custom.htm). 代码中创建了一个只接受数字值文本域. 它使用匿名类重新定义了`TextField`类，复写了继承自 `TextInputControl` 类的 `replaceText` 和 `replaceSelection` 方法.

```java
import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.stage.Stage;

public class CustomTextFieldSample extends Application {
    
    final static Label label = new Label();
 
    @Override
    public void start(Stage stage) {
        Group root = new Group();
        Scene scene = new Scene(root, 300, 150);
        stage.setScene(scene);
        stage.setTitle("Text Field Sample");
 
        GridPane grid = new GridPane();
        grid.setPadding(new Insets(10, 10, 10, 10));
        grid.setVgap(5);
        grid.setHgap(5);
 
        scene.setRoot(grid);
        final Label dollar = new Label("$");
        GridPane.setConstraints(dollar, 0, 0);
        grid.getChildren().add(dollar);
        
        final TextField sum = new TextField() {
            @Override
            public void replaceText(int start, int end, String text) {
                if (!text.matches("[a-z, A-Z]")) {
                    super.replaceText(start, end, text);                     
                }
                label.setText("Enter a numeric value");
            }
 
            @Override
            public void replaceSelection(String text) {
                if (!text.matches("[a-z, A-Z]")) {
                    super.replaceSelection(text);
                }
            }
        };
 
        sum.setPromptText("Enter the total");
        sum.setPrefColumnCount(10);
        GridPane.setConstraints(sum, 1, 0);
        grid.getChildren().add(sum);
        
        Button submit = new Button("Submit");
        GridPane.setConstraints(submit, 2, 0);
        grid.getChildren().add(submit);
        
        submit.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent e) {
                label.setText(null);
            }
        });
        
        GridPane.setConstraints(label, 0, 1);
        GridPane.setColumnSpan(label, 3);
        grid.getChildren().add(label);
        
        scene.setRoot(grid);
        stage.show();
    }
 
    public static void main(String[] args) {
        launch(args);
    }
}
```