---
title: Java 学习指南_学习Java：默认方法
date: 2018-03-27 16:50:59
tags: 
- java
- tutorial
- 教程
- interface
- 接口
- Default Methods
- 默认方法
categories:
- java
keywords:
- java
- 教程
- tutorial
- interface
- 接口
- Default Methods
- 默认方法
---

# 默认方法Default Methods

接口章节 [Interfaces](https://docs.oracle.com/javase/tutorial/java/IandI/createinterface.html) 描述了一个例子，关于电脑控制汽车生产厂商发布工业标准接口，调用其中的方法可以对他们的汽车进行操控。如果电脑控制汽车厂商为汽车增加了新的功能，例如飞行的功能，会怎么样呢？这些厂商需要明确新的方法是其他的公司（例如电子制导系统公司）调整他们的软件来控制汽车飞行。这些厂商要在哪里声明这些飞行相关的方法呢？如果他们吧方法添加在原有的接口中，那么已经实现了这些接口的开发者就必须重写他们的实现。如果作为静态方法添加，开发者会将其作为工具方法，而不是必要的和兴方法来对待。

默认方法可以让你为库里的接口添加新的功能，并且在重写旧版本接口的代码时确保两部分功能兼容。

考虑下面的接口, [`TimeClient`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/TimeClient.java), 在之前的联系中出现的 [Answers to Questions and Exercises: Interfaces](https://docs.oracle.com/javase/tutorial/java/IandI/QandE/interfaces-answers.html):

```java
import java.time.*; 
 
public interface TimeClient {
    void setTime(int hour, int minute, int second);
    void setDate(int day, int month, int year);
    void setDateAndTime(int day, int month, int year,
                               int hour, int minute, int second);
    LocalDateTime getLocalDateTime();
}
```

下面的类, [`SimpleTimeClient`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/defaultmethods/SimpleTimeClient.java), 实现了上面的接口 `TimeClient`:

```
package defaultmethods;

import java.time.*;
import java.lang.*;
import java.util.*;

public class SimpleTimeClient implements TimeClient {
    
    private LocalDateTime dateAndTime;
    
    public SimpleTimeClient() {
        dateAndTime = LocalDateTime.now();
    }
    
    public void setTime(int hour, int minute, int second) {
        LocalDate currentDate = LocalDate.from(dateAndTime);
        LocalTime timeToSet = LocalTime.of(hour, minute, second);
        dateAndTime = LocalDateTime.of(currentDate, timeToSet);
    }
    
    public void setDate(int day, int month, int year) {
        LocalDate dateToSet = LocalDate.of(day, month, year);
        LocalTime currentTime = LocalTime.from(dateAndTime);
        dateAndTime = LocalDateTime.of(dateToSet, currentTime);
    }
    
    public void setDateAndTime(int day, int month, int year,
                               int hour, int minute, int second) {
        LocalDate dateToSet = LocalDate.of(day, month, year);
        LocalTime timeToSet = LocalTime.of(hour, minute, second); 
        dateAndTime = LocalDateTime.of(dateToSet, timeToSet);
    }
    
    public LocalDateTime getLocalDateTime() {
        return dateAndTime;
    }
    
    public String toString() {
        return dateAndTime.toString();
    }
    
    public static void main(String... args) {
        TimeClient myTimeClient = new SimpleTimeClient();
        System.out.println(myTimeClient.toString());
    }
}
```

Suppose that you want to add new functionality to the `TimeClient` interface, such as the ability to specify a time zone through a [`ZonedDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/ZonedDateTime.html) object (which is like a[`LocalDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html) object except that it stores time zone information):

```java
public interface TimeClient {
    void setTime(int hour, int minute, int second);
    void setDate(int day, int month, int year);
    void setDateAndTime(int day, int month, int year,
        int hour, int minute, int second);
    LocalDateTime getLocalDateTime();                           
    ZonedDateTime getZonedDateTime(String zoneString);
}
```

下面对于接口 `TimeClient`的修改，你也必须修改 类 `SimpleTimeClient` 并实现其中新增的方法 `getZonedDateTime`. 不过, 与其将 `getZonedDateTime` 作为 `abstract` 抽象的,不如将它替换为默认方法 *default implementation*. (记住 [abstract method](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html) 是没有实现的方法.)

```java
package defaultmethods;
 
import java.time.*;

public interface TimeClient {
    void setTime(int hour, int minute, int second);
    void setDate(int day, int month, int year);
    void setDateAndTime(int day, int month, int year,
                               int hour, int minute, int second);
    LocalDateTime getLocalDateTime();
    
    static ZoneId getZoneId (String zoneString) {
        try {
            return ZoneId.of(zoneString);
        } catch (DateTimeException e) {
            System.err.println("Invalid time zone: " + zoneString +
                "; using default time zone instead.");
            return ZoneId.systemDefault();
        }
    }
        
    default ZonedDateTime getZonedDateTime(String zoneString) {
        return ZonedDateTime.of(getLocalDateTime(), getZoneId(zoneString));
    }
}
```

在方法签名前使用 `default` 关键字来明确接口中的方法是默认方法。接口中定义的所有方法包括默认方法，都是`public`的，因此你可以省略`public`修饰符。

这样定义接口的话，你就不需要修改类 `SimpleTimeClient`, 这个类 (以及所有实现了接口 `TimeClient`的类),都会已定义的 `getZonedDateTime` 方法.下面的例子, [`TestSimpleTimeClient`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/defaultmethods/TestSimpleTimeClient.java),调用了`SimpleTimeClient`一个实例的 `getZonedDateTime` 的方法:

```java
package defaultmethods;
 
import java.time.*;
import java.lang.*;
import java.util.*;

public class TestSimpleTimeClient {
    public static void main(String... args) {
        TimeClient myTimeClient = new SimpleTimeClient();
        System.out.println("Current time: " + myTimeClient.toString());
        System.out.println("Time in California: " +
            myTimeClient.getZonedDateTime("Blah blah").toString());
    }
}
```

## [扩展包含有默认方法的接口Extending Interfaces That Contain Default Methods]()

当你从一个包含有默认方法的接口进行扩展时，你可以有一下做法：

- 不提及默认方法，让扩展的几口继承原有的默认方法
- 重新定义默认方法，声明为`abstract`
- 重新定义默认方法，复写它

假设你按照下面的写法扩展 `TimeClient` 接口:

```java
public interface AnotherTimeClient extends TimeClient { }
```

任何实现了 `AnotherTimeClient` 接口的类都有默认方法 `TimeClient.getZonedDateTime`的实现.

假设你按照如下写法扩展 `TimeClient接口:

```java
public interface AbstractZoneTimeClient extends TimeClient {
    public ZonedDateTime getZonedDateTime(String zoneString);
}
```

任何实现接口 `AbstractZoneTimeClient`的类都必须重新实现方法 `getZonedDateTime`;这个方法现在是抽象方法 `abstract` ，就像接口中其他的非默认和非静态方法一样 。

假设你按照如下写法扩展 `TimeClient接口:

```java
public interface HandleInvalidTimeZoneClient extends TimeClient {
    default public ZonedDateTime getZonedDateTime(String zoneString) {
        try {
            return ZonedDateTime.of(getLocalDateTime(),ZoneId.of(zoneString)); 
        } catch (DateTimeException e) {
            System.err.println("Invalid zone ID: " + zoneString +
                "; using the default time zone instead.");
            return ZonedDateTime.of(getLocalDateTime(),ZoneId.systemDefault());
        }
    }
}
```

任何实现 `HandleInvalidTimeZoneClient` 接口的类都会用其中的 `getZonedDateTime` 方法实现类替代原有接口 `TimeClient`中的默认方法实现.

## [静态方法Static Methods]()

默认方法之外，你也可以在接口中定义静态方法 [static methods ](https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html).（静态方法属于类而不是其他的对象。类的每个实例都可以分享类它的静态方法）这样能让你更加容易的组织你库里的辅助方法；你可以将静态方法定义在统一接口中而不是其他的类里面。下面的例子定义了一个静态方法，获取一个 [`ZoneId`](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html) 对象先关的时区标识符；如果该对象没有给出相关的时区标识符则使用系统默认的时区标识符。（这样你就可以简化方法 `getZonedDateTime`）:

```java
public interface TimeClient {
    // ...
    static public ZoneId getZoneId (String zoneString) {
        try {
            return ZoneId.of(zoneString);
        } catch (DateTimeException e) {
            System.err.println("Invalid time zone: " + zoneString +
                "; using default time zone instead.");
            return ZoneId.systemDefault();
        }
    }

    default public ZonedDateTime getZonedDateTime(String zoneString) {
        return ZonedDateTime.of(getLocalDateTime(), getZoneId(zoneString));
    }    
}
```

就像类中定义的静态方法一样，在接口中定义静态方法同样是在方法签名前面加上`static`关键字。因为接口中定义的所有方法都是`public`的，所以你可以省略`public`修饰符。

## [在已有的代码库中融入默认方法Integrating Default Methods into Existing Libraries]()

默认方法可以你是你在已有的接口中添加新的功能，并同时确保兼容老版本接口写的代码。特别的是，默认方法允许你添加接受lambda表达式作为参数。本节演示了如何使用默认方法和静态方法增强 [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)接口.

考虑 `Card` 以及 `Deck` 类，在之前的联系中出现过 [Questions and Exercises: Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/QandE/creating-questions.html).本例重写了两个类 [`Card`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/defaultmethods/Card.java) 以及 [`Deck`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/defaultmethods/Deck.java) 作为接口. `Card` 接口包含了两个枚举类型 `enum` (`Suit` 和 `Rank`) 以及两个抽象方法(`getSuit` 和 `getRank`):

```java
package defaultmethods;

public interface Card extends Comparable<Card> {
    
    public enum Suit { 
        DIAMONDS (1, "Diamonds"), 
        CLUBS    (2, "Clubs"   ), 
        HEARTS   (3, "Hearts"  ), 
        SPADES   (4, "Spades"  );
        
        private final int value;
        private final String text;
        Suit(int value, String text) {
            this.value = value;
            this.text = text;
        }
        public int value() {return value;}
        public String text() {return text;}
    }
    
    public enum Rank { 
        DEUCE  (2 , "Two"  ),
        THREE  (3 , "Three"), 
        FOUR   (4 , "Four" ), 
        FIVE   (5 , "Five" ), 
        SIX    (6 , "Six"  ), 
        SEVEN  (7 , "Seven"),
        EIGHT  (8 , "Eight"), 
        NINE   (9 , "Nine" ), 
        TEN    (10, "Ten"  ), 
        JACK   (11, "Jack" ),
        QUEEN  (12, "Queen"), 
        KING   (13, "King" ),
        ACE    (14, "Ace"  );
        private final int value;
        private final String text;
        Rank(int value, String text) {
            this.value = value;
            this.text = text;
        }
        public int value() {return value;}
        public String text() {return text;}
    }
    
    public Card.Suit getSuit();
    public Card.Rank getRank();
}
```

 `Deck` 接口包含了许多操作cards的方法:

```java
package defaultmethods; 
 
import java.util.*;
import java.util.stream.*;
import java.lang.*;
 
public interface Deck {
    
    List<Card> getCards();
    Deck deckFactory();
    int size();
    void addCard(Card card);
    void addCards(List<Card> cards);
    void addDeck(Deck deck);
    void shuffle();
    void sort();
    void sort(Comparator<Card> c);
    String deckToString();

    Map<Integer, Deck> deal(int players, int numberOfCards)
        throws IllegalArgumentException;

}
```

类 [`PlayingCard`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/defaultmethods/PlayingCard.java) 实现了 接口 `Card`, 类 [`StandardDeck`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/defaultmethods/StandardDeck.java) 实现了接口 `Deck`.

类 `StandardDeck` 实现了类的 `Deck.sort` 方法:

```java
public class StandardDeck implements Deck {
    
    private List<Card> entireDeck;
    
    // ...
    
    public void sort() {
        Collections.sort(entireDeck);
    }
    
    // ...
}
```

 `Collections.sort` 方法讲一个List实例进行了排序，List实例的元素类型是实现了 [`Comparable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html)接口.成员变量 `entireDeck` 是一个元素为`Card`的 `List`实例。 `Card `实现了`Comparable` 接口. 类 `PlayingCard` 实现了 [`Comparable.compareTo`](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html#compareTo-T-) 方法，内容如下:

```java
public int hashCode() {
    return ((suit.value()-1)*13)+rank.value();
}

public int compareTo(Card o) {
    return this.hashCode() - o.hashCode();
}
```

 方法 `StandardDeck.sort()` 通过 `compareTo` 方法是扑克先按照花色再按照点数排序。如果你想要让扑克先按照点数，再按照花色排序该怎么做呢？你可能需要实现`Comparator`接口来明确新的排序规则，并使用方法[`sort(List list, Comparator c)`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#sort-java.util.List-java.util.Comparator-) ( `sort `方法包含`Comparator`参数的版本).你可以在类`StandardDeck`中定义如下方法:

```java
public void sort(Comparator<Card> c) {
    Collections.sort(entireDeck, c);
}  
```

有了这个方法你可以，你是可以使用 `Collections.sort` 明确 `Card` 类实例的排序规则.一种方法是实现 `Comparator` 接口来明确扑克排序的规则.下面的类 [`SortByRankThenSuit`](https://docs.oracle.com/javase/tutorial/java/IandI/examples/defaultmethods/SortByRankThenSuit.java) 进行了示例:

```java
package defaultmethods;

import java.util.*;
import java.util.stream.*;
import java.lang.*;

public class SortByRankThenSuit implements Comparator<Card> {
    public int compare(Card firstCard, Card secondCard) {
        int compVal =
            firstCard.getRank().value() - secondCard.getRank().value();
        if (compVal != 0)
            return compVal;
        else
            return firstCard.getSuit().value() - secondCard.getSuit().value(); 
    }
}
```

下面的调用时扑克先按照点数再按照花色排序:

```java
StandardDeck myDeck = new StandardDeck();
myDeck.shuffle();
myDeck.sort(new SortByRankThenSuit());
```

不过，这种方法太冗长verbose；如果你可以明确按照什么排序而不是怎么排序会更好。假设你是写`Compatator`接口 开发者。你会在`Comparator`接口中添加什么默认方法或者静态方法来是其他开发者更加简单的明确排序规则？

一开始，你想要将这些扑克按照点数排序而不管花色。你可以这样调用 `StandardDeck.sort方法:

```java
StandardDeck myDeck = new StandardDeck();
myDeck.shuffle();
myDeck.sort(
    (firstCard, secondCard) ->
        firstCard.getRank().value() - secondCard.getRank().value()
); 
```

因为接口 `Comparator` 是一个功能接口 [functional interface](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#approach6), 所以你可以使用lambda表达式作为`sort`方法的参数。本例中，lambda表达式比较了两个整数值。

这样可以是开发者通过只调用`Card.getRank`方法就简单的创建一个`Comparator`实例。并且，他可以付诸开发者`Comparator`实例来比较任何可以通过入住`getValue` `hashCode`等方法返回数字值的对象。`Comparator`接口已经通过静态方法 [`comparing`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#comparing-java.util.function.Function-java.util.Comparator-)增强而拥有这个能力:

```java
myDeck.sort(Comparator.comparing((card) -> card.getRank()));  
```

这个例子中，你也可以通过方法引用来代替 [method reference](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html):

```java
myDeck.sort(Comparator.comparing(Card::getRank));  
```

这种调用很好的演示了用什么排序而不是怎么排序.

 `Comparator` 接口同样有其他类似`comparing`版本的静态方法增强如  [`comparingDouble`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#comparingDouble-java.util.function.ToDoubleFunction-java.util.Comparator-) 和 [`comparingLong`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#comparingLong-java.util.function.ToLongFunction-) 可以用来创建通过其他数据类型比较的 `Comparator` 实例.

假设你的开发者想要创建一个 `Comparator` 实例，使用不止一个条件比较对象。例如，你如何将扑克先按照点数再按照花色排序？像前面的例子一样，你可以使用lambda表达式来明确这些排序规则:

```java
StandardDeck myDeck = new StandardDeck();
myDeck.shuffle();
myDeck.sort(
    (firstCard, secondCard) -> {
        int compare =
            firstCard.getRank().value() - secondCard.getRank().value();
        if (compare != 0)
            return compare;
        else
            return firstCard.getSuit().value() - secondCard.getSuit().value();
    }      
); 
```

如果开发者可以通过一系列的 `Comparator` 实例来构造 `Comparator` 实例，将会更加简单. `Comparator` 接口已经通过默认方法  [`thenComparing`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#thenComparing-java.util.Comparator-)增强而拥有了这个能力:

```java
myDeck.sort(
    Comparator
        .comparing(Card::getRank)
        .thenComparing(Comparator.comparing(Card::getSuit)));
```

 `Comparator` 接口同样有其他版本的 `thenComparing`方法 (例如  [`thenComparingDouble`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#thenComparingDouble-java.util.function.ToDoubleFunction-) 以及 [`thenComparingLong`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#thenComparingLong-java.util.function.ToLongFunction-)) 这样你可以构造 `Comparator` 实例来比较其他的数据类型.

假设你的开发者想要创建 `Comparator` 实例，倒序排列一个集合，例如你想要将扑克按照点数降序排列，从A到2.像之前一样你可以定义lambda表达式来实现。不过，如果可以通过已有的`Comparator`实例调用方法将会更简单。`Comparator`接口已经预知了默认方法 [`reversed`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#reversed--):

```java
myDeck.sort(
    Comparator.comparing(Card::getRank)
        .reversed()
        .thenComparing(Comparator.comparing(Card::getSuit)));
```

这个例子演示了 `Comparator` 接口是如何通过默认方法，静态方法，lambda表达式，以及方法引用来增强的，这样就创建了更有表现力的库和方法，功能开发者可以快速的推断出该如何调用其中的方法。用同样的构造来创建你自己的库里的接口。