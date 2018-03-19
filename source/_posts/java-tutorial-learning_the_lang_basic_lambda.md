---
title: Java 学习指南_学习Java：基础-Lambda表达式
date: 2018-03-15 15:51:59
tags: 
- java
- tutorial
- 教程
- 类
- Lambda表达式
categories:
- java
keywords:
- java
- 教程
- tutorial
- 类
- Lambda表达式
---

# Lambda 表达式 Lambda Expressions

使用匿名类的一个问题在于，如果你要实现的匿名类非常的简单，例如只包含一个方法的借口，那么匿名列的语法看起来就不够简洁和轻便。这种情况下，你通常会尝试将某个功能作为参数传递给一其他方法，例如当点击按钮的时候会采取什么措施。Lambda表达式可以提供这样的功能，将功能作为方法的参数，或者代码作为数据。

上一节中， [Anonymous Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html), 向你展示了实现一个基本的类而不需要命名，譬如只有一个方法的类，不过匿名类看起来有点复杂和笨重。Lambda表达式可以使你更加紧凑的表达一个单方法类的实例。

本节将包含以下的内容:

- [Lambda表达式的经典应用Ideal Use Case for Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#use-case)
  - [方法1：创建搜索某一特点的成员的方法Approach 1: Create Methods That Search for Members That Match One Characteristic](#approach1)
  - [方法2：创建更加通用的搜索方法Approach 2: Create More Generalized Search Methods](#approach2)
  - [方法3：用局部类实现特定搜索规则相关的的代码Approach 3: Specify Search Criteria Code in a Local Class](#approach3)
  - [方法4：用匿名类实现特定搜索规则相关的代码Approach 4: Specify Search Criteria Code in an Anonymous Class](#approach4)
  - [方法5：用Lambda表达式实现特定搜索规则的代码Approach 5: Specify Search Criteria Code with a Lambda Expression](#approach5)
  - [方法6：通过标准的功能接口使用lambda表达式Approach 6: Use Standard Functional Interfaces with Lambda Expressions](#approach6)
  - [方法7：在你的应用中使用Lambda表达式Approach 7: Use Lambda Expressions Throughout Your Application](#approach7)
  - [方法8：使用反应提高可扩展性Approach 8: Use Generics More Extensively](#approach8)
  - [方法9：使用已Lambda表达式作为参数的聚合操作Approach 9: Use Aggregate Operations That Accept Lambda Expressions as Parameters](#approach9)
- [在GUI应用中使用Lambda表达式Lambda Expressions in GUI Applications](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#lambda-expressions-in-gui-applications)
- [Lambda表达式语法Syntax of Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#syntax)
- [访问闭合区间的局部变量Accessing Local Variables of the Enclosing Scope](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#accessing-local-variables)
- [目标类型Target Typing](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#target-typing)[目标类型以及方法参数Target Types and Method Arguments](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#target-types-and-method-arguments)
- [序列化Serialization](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#serialization)

<!-- more -->

## [Lambda表达式最佳实践Ideal Use Case for Lambda Expressions]()

假设你正在创建一个社交网络应用。你想要创建一个功能来满足管理员的各种操作，例如，向社交网络应用中中满足特定规则的成员发送消息。下面的表格描述了这个案例的详细信息。

| 字段            | 描述                                       |
| ------------- | ---------------------------------------- |
| 名称            | 对选择的成员进行操作                               |
| 主要角色          | 管理员Administrator                         |
| 前置条件          | 管理员已登录到系统                                |
| 完成条件          | 操作只对符合特定规则的成员生效                          |
| 内容梗概          | 管理员确定要执行操作的成员。管理员明确要执行的操作。管理员选择Submit按钮。系统找到所有满足条件的成员。系统对所有符合条件成员执行操作 |
| 扩展            | 1a. 管理员可以在提交操作之前预览那些符合条件的成员。             |
| 发生频率Frequency | 每天数次                                     |

假设社交网络应用中的成员可以用如下的 [`Person`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/Person.java) 类表示:

```java
public class Person {

    public enum Sex {
        MALE, FEMALE
    }

    String name;
    LocalDate birthday;
    Sex gender;
    String emailAddress;

    public int getAge() {
        // ...
    }

    public void printPerson() {
        // ...
    }
}
```

假设你社交网络应用中的成员是存储在一个 `List<Person>` 实例中.

本章开始用一种稚拙的方法实现这个用例。然后使用局部类类和匿名类来改进，最后使用lambda表达式通过一种高效和简洁的方式完成。本章节中 [`RosterTest`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/RosterTest.java)例子中可以找到相关的代码片段。.

### [方法1：创建搜索符合某些特征的成员的方法]()

一个简单的途径就是创建数个方法methods;每一个方法搜索符合一个特征的成员，譬如性别或者年龄。下面的代码打印出了年龄大于某特定年龄的成员:

```java
public static void printPersonsOlderThan(List<Person> roster, int age) {
    for (Person p : roster) {
        if (p.getAge() >= age) {
            p.printPerson();
        }
    }
}
```

**注意**:  [`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) 是一个有序的集合 [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html). 集合是在一个单独单眼里包含多个元素的对象。集合是用来存储，获取，操作以及表达集合数据。参考 [Collections](https://docs.oracle.com/javase/tutorial/collections/index.html) 获取更多集合相关的信息.

这种方法可能使你的应用非常的脆弱，譬如可能英文介绍里提到的扩展(例如新的数据类型)而导致程序无法工作。假设你应用的升级改变了`Person`类的数据结构，该数据结构包含了不同的成员变量；或许类使用了不同的数据类型来存储年龄，或者用不同的算法来计量年龄。你就不得不重写你的API来满足这些改变。另外，这个方法还有不必要的限制，如果你想要打印出小于特定年龄的成员时改怎么办呢?

### [方案2：创建更加通用的方法Approach 2: Create More Generalized Search Methods]()

下面的方法比上一个方法`printPersonOlderThan`更通用一些；可以打印出特定年龄范围的成员：:

```java
public static void printPersonsWithinAgeRange(
    List<Person> roster, int low, int high) {
    for (Person p : roster) {
        if (low <= p.getAge() && p.getAge() < high) {
            p.printPerson();
        }
    }
}
```

那么如果你想要打印出某一性别，或者是某一性别和特定年龄范围组合的相关成员？如果你决定改变`Person`类型的属性增加诸如情感状态或者地理位置？尽管这个方法比之前的方法更通用，但是尝试为每一种可能的搜索都创建单独的方法同样导致脆弱的代码。你可以将说明具体搜索范围的代码分割出来，创建另外一个类。

### [方案3：在局部类中说明搜索标准Approach 3: Specify Search Criteria Code in a Local Class]()

下面的方法打印出符合你搜索标准的成员:

```java
public static void printPersons(
    List<Person> roster, CheckPerson tester) {
    for (Person p : roster) {
        if (tester.test(p)) {
            p.printPerson();
        }
    }
}
```

这个方法检查`List`参数`roster`中的每一个`Person`实例是否满搜索标准，通过调用`CheckPerson`参数`tester`的`test`方法来实现。如果`tester.test`返回一个`True`，呢么`Person`实例中的`printPerson`方法就回被调用.

针对不同的搜索标准，你需要实现`CheckPerson`接口:

```java
interface CheckPerson {
    boolean test(Person p);
}
```

下面的类实现了`CheckPerson`接口，明确了`test`方法的一个具体实现。这个方法过滤了符合美国服兵役条件的成员:如果`Person`参数是男性并且年龄在18到25之间则返回`True`:

```java
class CheckPersonEligibleForSelectiveService implements CheckPerson {
    public boolean test(Person p) {
        return p.gender == Person.Sex.MALE &&
            p.getAge() >= 18 &&
            p.getAge() <= 25;
    }
}
```

通过这个类，你创建一个新的`Person`实例并且调用`printPersons`方法:

```java
printPersons(
    roster, new CheckPersonEligibleForSelectiveService());
```

尽管这个方案没有那么脆弱了——当你改变Person的数据结构时，无需再重写你的方法——当你仍然需要额外的代码：一个新的结构以及一个本地类来查询你计划进行操作的成员。因为`CheckPersonEligibleForSelectiveService`实现了一个接口，所以你可以通过匿名类来代替局部类，并且可以避免对每一中搜索都创建一个新的类。

### [方案4：Approach 4: Specify Search Criteria Code in an Anonymous Class]()

下列代码中`printPersons`方法调用中的一个参数是一个匿名类，这个匿名类筛选出美国需要服兵役的成员:年龄介于18到25岁的男性成员。:

```java
printPersons(
    roster,
    new CheckPerson() {
        public boolean test(Person p) {
            return p.getGender() == Person.Sex.MALE
                && p.getAge() >= 18
                && p.getAge() <= 25;
        }
    }
);
```

这个方案减少了必须的代码，因为你不需要为每一个查询都创建一个新的类。然而，匿名类的语法非常的笨重，考虑到`CheckPerson`接口中实际只包含了一个方法。在这种情况下，你可以使用你个lambda表达式来代替匿名类，也就是下一节所讲的内容.

### [方案5：使用lambda表达式表明搜索标准Approach 5: Specify Search Criteria Code with a Lambda Expression]()

`CheckPerson`接口是一个*functional interface*功能接口.功能接口是指只包含一个抽象方法 [abstract method](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)的接口. (当然功能接口可能包含一个或者多个默认方法 [default methods](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html)或者静态方法 [static methods](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html#static).) 因为一个功能接口只包含了一个抽象方法，当你实现它的时候你可以移除方法名。这么做就替代了匿名类的表达式，使用了lambda表达式 *lambda expression*,正如如下代码方法调用中说所用的样子:

```java
printPersons(
    roster,
    (Person p) -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25
);
```

参考 [Lambda 表达式语法Syntax of Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#syntax)获取如何定义Lambda表达式的更多信息.

你可以使用标准的功能接口来代替`CheckPerson`接口，可以进一步减少所需的代码量.

### [方法6：使用标准的功能接口实现Lambda表达式Approach 6: Use Standard Functional Interfaces with Lambda Expressions]()

重现审视CheckPerson 接口:

```java
interface CheckPerson {
    boolean test(Person p);
}
```

这是一个非常简单的是接口。因为他只包含一个抽象方法所以他是一个功能接口。这个方法接口一个参数并返回布尔值。这个方法如此简单所以你没有必要再应用中定义它。因此，JDK定义了数个标准的功能接口，你可以在`java.util.function`包中找到这些接口。

例如，你个使用 `Predicate<T>`接口来代替 `CheckPerson`.这个接口包含了方法 `boolean test(T t)`:

```java
interface Predicate<T> {
    boolean test(T t);
}
```

接口 `Predicate<T>` 是泛型接口的一个例子. (参考泛型（更新） [Generics (Updated)](https://docs.oracle.com/javase/tutorial/java/generics/index.html) 一颗来获取更多关于泛型的信息.) 泛型类（例如泛型接口）在尖括号中表明一个或多个类型参数(`<>`). 这个接口只包含了一个参数，`T`,当你定义实际的类型参数时，你有一个参数类型，例如 `Predicate<Person>` :

```java
interface Predicate<Person> {
    boolean test(Person t);
}
```

参数类型，包含了一个拥有同样参数类型的方法 `CheckPerson.boolean test(Person p)`. 因此，你可以使用 `Predicate<T>` 替换 `CheckPerson`类，如下所示:

```java
public static void printPersonsWithPredicate(
    List<Person> roster, Predicate<Person> tester) {
    for (Person p : roster) {
        if (tester.test(p)) {
            p.printPerson();
        }
    }
}
```

结果，下面的方法调用就如同你在方法3中 `printPersons` [Approach 3: Specify Search Criteria Code in a Local Class](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#approach3) 一样，可以获取符合服兵役条件的成员:

```java
printPersonsWithPredicate(
    roster,
    p -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25
);
```

这里并不是唯一可以使用lambda表达式的地方。下面的方案推荐了其他使用lambda表达式的方法.

### [方案7:在你的整个应用中使用lambda表达式Approach 7: Use Lambda Expressions Throughout Your Application]()

重新考虑方法 `printPersonsWithPredicate` ，看看你可以在哪里使用lambda表达式:

```java
public static void printPersonsWithPredicate(
    List<Person> roster, Predicate<Person> tester) {
    for (Person p : roster) {
        if (tester.test(p)) {
            p.printPerson();
        }
    }
}
```

这个犯法检查了`List`参数`roster`中每一个`Person`实例是否符合具体的标准`Predicate`参数`tester`。如果Person实例确实满足`tester`的条件，`Person`实例就调用`printPerson`方法.

取代了调用`printPerson`方法，你可以对满足搜索条件的成员制定不同的操作。你同样可以通过lambda表达式来实现操作。假如你希望有一个类似printPerson方法的lambda表达式，获取一个Person参数并返回void。记住，使用lambda表达式，你需要实现一个功能接口。本例中，你需要实现一个接受Person参数并且返回为void的接口。`Consumer<T>`接口，包含了`void accept(T t)`方法，刚好符合这一特征.下面的代码使用你个`Consumer<Person>`的实例的`accept`方法调用，替换了`p.printPerson()`方法的调用:

```java
public static void processPersons(
    List<Person> roster,
    Predicate<Person> tester,
    Consumer<Person> block) {
        for (Person p : roster) {
            if (tester.test(p)) {
                block.accept(p);
            }
        }
}
```

这样，如下的方法调用同样实现了方案3中的功能，lambda表达式使用的代码如下所示:

```
processPersons(
     roster,
     p -> p.getGender() == Person.Sex.MALE
         && p.getAge() >= 18
         && p.getAge() <= 25,
     p -> p.printPerson()
);
```

如果你想要对成员的信息做更多的操作而不只是打印出来。假设你需要验证成员的简介并且获取他们的联系信息。在本例中，你需要一个方能接口把汗了一个返回值的抽象方法。 `Function<T,R>`接口包含一个方法 `R apply(T t)`.下面的代码通过参数`mapper`，获取了数据并通过`block`参数进行的具体的操作：

```java
public static void processPersonsWithFunction(
    List<Person> roster,
    Predicate<Person> tester,
    Function<Person, String> mapper,
    Consumer<String> block) {
    for (Person p : roster) {
        if (tester.test(p)) {
            String data = mapper.apply(p);
            block.accept(data);
        }
    }
}
```

下面的方法取得了过滤后的成员的邮箱地址并且打印出了他们:

```java
processPersonsWithFunction(
    roster,
    p -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25,
    p -> p.getEmailAddress(),
    email -> System.out.println(email)
);
```

### [方案8：使用泛型提高扩展性Approach 8: Use Generics More Extensively]()

重新考虑方法 `processPersonsWithFunction`. 如下代码是一个泛型的版本，可以接受任何类型元素集合作为参数:

```java
public static <X, Y> void processElements(
    Iterable<X> source,
    Predicate<X> tester,
    Function <X, Y> mapper,
    Consumer<Y> block) {
    for (X p : source) {
        if (tester.test(p)) {
            Y data = mapper.apply(p);
            block.accept(data);
        }
    }
}
```

如果需要打印符合条件的成员的e-mail地址，调用`processElements`方法的代码如下所示:

```java
processElements(
    roster,
    p -> p.getGender() == Person.Sex.MALE
        && p.getAge() >= 18
        && p.getAge() <= 25,
    p -> p.getEmailAddress(),
    email -> System.out.println(email)
);
```

方法调用执行了一下的操作:

1. 获取对象集合 `source`. 本例中，获取了`Person`对象的集合`roster` .`roster`集合是一个`List`同样是个 `Iterable`可迭代的对象.
2. 过滤对象中匹配 `Predicate` 对象 `tester`条件的 成员.  `Predicate`对象在本例中满足了服兵役条件的成员。
3. 通过 `Function` 对象 `mapper`映射每一个成员.本例中获取了每个成员的e-mail地址.
4. 通过 `Consumer` 对象 `block`方法对映射后的结果做具体的操做，本例中将应设计过也就是e-mail地址打印了出来.

你同样可以使用聚合操作（连贯操作）来替代以上的操作步骤。.

### [方案9：使用接受Labmda表达式为参数的集合操作Approach 9: Use Aggregate Operations That Accept Lambda Expressions as Parameters]()

下面的例子使用连贯操作打印出了符合条件的承欢的e-mail地址:

```java
roster
    .stream()
    .filter(
        p -> p.getGender() == Person.Sex.MALE
            && p.getAge() >= 18
            && p.getAge() <= 25)
    .map(p -> p.getEmailAddress())
    .forEach(email -> System.out.println(email));
```

如下表格列出了processElements功能中各个步骤以及对应的连贯操作方法:

| `processElements` Action（方法步骤）           | Aggregate Operation(集合操作)                |
| ---------------------------------------- | ---------------------------------------- |
| Obtain a source of objects获取资源，集合对象      | `Stream<E> **stream**()`                 |
| Filter objects that match a `Predicate` object过滤对象 | `Stream<T> **filter**(Predicate<? super T> predicate)` |
| Map objects to another value as specified by a `Function` object将集合中对象映射为其他的值 | `<R> Stream<R> **map**(Function<? super T,? extends R> mapper)` |
| Perform an action as specified by a `Consumer` object通过`Consumer`对象执行具体的操作 | `void **forEach**(Consumer<? super T> action)` |



操作 `filter`, `map`, 以及 `forEach` 是 *aggregate operations*聚合操作. 局和操作将元素作为一个流来处理，而不是直接从集合中（也就是为什么要首先调用`stream`方法的原因）.*stream*流是一个元素集合的序列。区别与集合的是，它并不是存储元素的数据结构，流负责从集合中取出资源，通过一个管道。管道pipeline是一系列的流式操作，在本例中的`filter-map-forEach`。另外，局和操作通常接受lambda表达式作为参数，是你可以自定义操作的行为。

获取更多关于聚合操作的信息，你可以参考 [Aggregate Operations](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) 一课.

## [Lambda表达式在GUI应用的使用Lambda Expressions in GUI Applications]()

处理GUI应用的事件，例如按键事件，鼠标事件，以及滚动事件。通常你都会创建事件处理器，一般都是通过实现特定的接口。一般来说，事件处理器接口是功能接口；他们通常只有一个方法。

在JAVAFX例子中 [`HelloWorld.java`](https://docs.oracle.com/javase/8/javafx/get-started-tutorial/hello_world.htm) (前一章节中 [Anonymous Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html)), 中提到的你可以将如下所示的匿名类代码替换为Lambda表达式:

```java
        btn.setOnAction(new EventHandler<ActionEvent>() {

            @Override
            public void handle(ActionEvent event) {
                System.out.println("Hello World!");
            }
        });
```

`btn.setOnAction`方法调用定义当你鼠标选择了`btn`对象代表的按钮式要放生的事情。这个方法要求一个`EventHandler<ActionEvent>`类型的对象作为参数。`EventHandler<ActionEvent>` 接口只包含了一个方法`void handle<T event>` 。这个接口是一个功能接口，因此你可以使用如下的`Lambda`来替换他:

```java
        btn.setOnAction(
          event -> System.out.println("Hello World!")
        );
```

## [Lambda表达式的语法Syntax of Lambda Expressions]()

一个Lambda表示由如下几部分构成:

- 一个圆括号包围、逗号分隔的参数形式的列表.`CheckPerson.test`方法包含了一个参数`p`,代表了`Person`类的实例。

  **注意**:你可以省略参数类型。同样当只有一个参数时，你也可以省略圆括号。例如下面的Lambda表达式依然是有效的:

  ```java
  p -> p.getGender() == Person.Sex.MALE 
      && p.getAge() >= 18
      && p.getAge() <= 25
  ```

- 箭头符号, `->`

- 一个方法体, 包含一个单独的表达式或者语句块:

  ```
  p.getGender() == Person.Sex.MALE 
      && p.getAge() >= 18
      && p.getAge() <= 25
  ```

  如果只有一个表达式，Java运行时会返回表达式的值，同样你可以使用返回语句，如下:

  ```
  p -> {
      return p.getGender() == Person.Sex.MALE
          && p.getAge() >= 18
          && p.getAge() <= 25;
  }
  ```

  返回语句不是一个表达式；在lambda表达式中如果你使用的语句块则必须用`{}`来闭合，但是你只调用了没有返回值的方法时时可以省略`{}`,如下：

  ```java
  email -> System.out.println(email)
  ```

注意lambda表达式的定义看起来像是方法的定义;你可以认为lambda表达式是一个匿名方法——没有命名的方法.

接下来的例子, [`Calculator`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/Calculator.java), 使用了不止一个参数:

```java
public class Calculator {
  
    interface IntegerMath {
        int operation(int a, int b);   
    }
  
    public int operateBinary(int a, int b, IntegerMath op) {
        return op.operation(a, b);
    }
 
    public static void main(String... args) {
    
        Calculator myApp = new Calculator();
        IntegerMath addition = (a, b) -> a + b;
        IntegerMath subtraction = (a, b) -> a - b;
        System.out.println("40 + 2 = " +
            myApp.operateBinary(40, 2, addition));
        System.out.println("20 - 10 = " +
            myApp.operateBinary(20, 10, subtraction));    
    }
}

```

方法`operationBinary`实现类两个整形的数学运算。运算有每个实例自身区分实现。本例中定义了加法和减法两种运算，代码输出结果如下:

```
40 + 2 = 42
20 - 10 = 10
```

## [访问局部变量Accessing Local Variables of the Enclosing Scope]()

就像局部类和匿名类一样，lambda表达式可以获取变量 [capture variables](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html#accessing-members-of-an-enclosing-class); 他们同局部类和匿名类具有相同的访问权限，lambda表达式么有任何的遮蔽问题（参考 [Shadowing](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html#shadowing) 获取更多信息).Lambda表达式是此法范围的。意思是他不从父类继承命名也不引入新的命名空间。定义Lambda表达式只解释为它是在闭合的环境内，下面的例子 [`LambdaScopeTest`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/LambdaScopeTest.java), 进行了演示:

```java
import java.util.function.Consumer;

public class LambdaScopeTest {

    public int x = 0;

    class FirstLevel {

        public int x = 1;

        void methodInFirstLevel(int x) {
            
            // The following statement causes the compiler to generate
            // the error "local variables referenced from a lambda expression
            // must be final or effectively final" in statement A:
            //
            // x = 99;
            
            Consumer<Integer> myConsumer = (y) -> 
            {
                System.out.println("x = " + x); // Statement A
                System.out.println("y = " + y);
                System.out.println("this.x = " + this.x);
                System.out.println("LambdaScopeTest.this.x = " +
                    LambdaScopeTest.this.x);
            };

            myConsumer.accept(x);

        }
    }

    public static void main(String... args) {
        LambdaScopeTest st = new LambdaScopeTest();
        LambdaScopeTest.FirstLevel fl = st.new FirstLevel();
        fl.methodInFirstLevel(23);
    }
}
```

上述例子输出如下:

```java
x = 23
y = 23
this.x = 1
LambdaScopeTest.this.x = 0
```

如果你在定义lambda表达式时将y替换为x，编译器将会产生错误:

```java
Consumer<Integer> myConsumer = (x) -> {
    // ...
}
```

编译器产生错误"变量x已经在方法`methodInFirstLevel(int)`中声明"因为lambda表达式并不引入新的命名空间，因此，你可以直接访问闭合范围内的成员变量，方法，以及局部变量。例如，lambda比到时直接访问方法`methodInFirstLevel`的参数`x`.要方位闭合类中的变量，则需要使用关键字`this`。本例中，`this.x`指向成员变量`FirstLevel.x`.

然而，就像局部类和匿名类一样，你个lambda表达式只能访问闭合块中定义为final或者final作用的变量或者参数，假设你在代码中增加一行:

```java
void methodInFirstLevel(int x) {
    x = 99;
    // ...
}
```

应为代码片段中，变量FirstLevel.x 不再是有效的最终变量.将导致编译器差生类似"lambda表达式必须引用final或者等同final的变量":

```java
System.out.println("x = " + x);
```

## [目标类型Target Typing]()

怎么确定lambda表达式的类型呢？回想一下筛选成员是所用的lambda表达式:

```java
p -> p.getGender() == Person.Sex.MALE
    && p.getAge() >= 18
    && p.getAge() <= 25
```

这个lambda表达式在以下两个方法中用到:

- `public static void printPersons(List<Person> roster, CheckPerson tester)` in [Approach 3: Specify Search Criteria Code in a Local Class](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#approach3)
- `public void printPersonsWithPredicate(List<Person> roster, Predicate<Person> tester)` in [Approach 6: Use Standard Functional Interfaces with Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#approach6)

当Java运行时调用方法`printPersons`是，他期望的数据类型是`CheckPerson`,因此lambda是就是这种类型，但是当java运行时调用方法`printPersonWithPredicate`时，他期望的类型是`Predicate<Person>`,因此lambda表达式就是这种类型。这种方法期望的数据类型叫做目标类型 *target type*.为了确认lambda表达式的类型，java编译器根据其出现的上下文或者情景中的目标类型来决定。下面列出了java编译器可以确定目标类型的情形:

- 变量声明Variable declarations
- 赋值Assignments
- 返回语句Return statements
- 数组初始化Array initializers
- 方法或者狗高企参数Method or constructor arguments
- Lambda表达式体Lambda expression bodies
- 表达式`?:`情形Conditional expressions, `?:`
- 类型转换表达式Cast expressions

### [目标类型和方法参数Target Types and Method Arguments]()

作为方法参数，java编译器根据另外两个语言特性确认目标累心：重载以及类型参数引用。

考虑下面的两个功能接口 ( [`java.lang.Runnable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html) 以及 [`java.util.concurrent.Callable`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Callable.html)):

```java
public interface Runnable {
    void run();
}

public interface Callable<V> {
    V call();
}
```

方法 `Runnable.run` 不返回值 ，而 `Callable<V>.call` 返回.

假设你重载了方法`invoke`如下所示 (参考 [Defining Methods](https://docs.oracle.com/javase/tutorial/java/javaOO/methods.html) 获取更多重载的信息):

```java
void invoke(Runnable r) {
    r.run();
}

<T> T invoke(Callable<T> c) {
    return c.call();
}
```

而方法的调用如下?

```java
String s = invoke(() -> "done");
```

方法调用 `invoke(Callable<T>)` 会被调用因为他有一个返回值;而方法`invoke(Runnable)`不会因为他没有返回值，所以lambda表达式的`() -> "done"` 的类型是 `Callable<T>`.

## [序列化Serialization]()



如果你个lambda表达式的目标类型以及获取的参数是可以序列化的，那么你可以序列化 [serialize](https://docs.oracle.com/javase/tutorial/jndi/objects/serial.html) 一个lambda表达式。不过，就像内部类 [inner classes](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html#serialization)一样，强烈不建议序列化.