---
title: Java 学习指南_学习Java：接口
date: 2018-03-26 15:40:59
tags: 
- java
- tutorial
- 教程
- interface
- 接口
categories:
- java
keywords:
- java
- 教程
- tutorial
- interface
- 接口
---



# 接口

软件工程中的很多情况写，让各个独立的开发小组遵循一个"合约"，来详细说明他们的软件是如何相互作用的。每个小组应该能再完全不知道其他小组写的代码的情况下编写自己的代码。广泛的说，接口`interfaces`就是这样的合约。

例如，想象一下未来社会，电脑控制的机器人汽车运载乘客穿过城市的街道而不需要人为的操作。汽车制造商编写软件（当然，用java语言）来控制他们的汽车，停止，启动，加速，左转等等。另外一个工业小组，电子制导设备制造商，制造电脑系统来接受GPS（Global Positioning System）位置信息以及无线传输的交通状况信息，并根据这些信息驾驶汽车。

汽车制造商必须发布一个工业标准详细说明调用什么方法可以让汽车移动（任何一家厂商的任何一辆车）。这时候制导系统厂商就可以编写软件调用接口所规定的方法命令汽车运行。这样工业组并不需要了解其方法具体是怎么实现的，汽车厂商也高度保留了其所有权并可以随时修改其实现，同时又遵循与已经公布的接口标准。

## Java中的接口

Java编程语言中，接口interface是一个引用类型，与类class相似，不过只可以包含常量，方法签名，默认方法，静态方法，嵌套类型。只有默认方法和静态方法可以存在方法体。接口不能被实例化——只能被类实现或者被其他的借口扩展。后续的借口将会讲到扩展的内容。

定义一个接口与定义一个类非常类似:

```java
public interface OperateCar {

   // constant declarations, if any

   // method signatures
   
   // An enum with values RIGHT, LEFT
   int turn(Direction direction,
            double radius,
            double startSpeed,
            double endSpeed);
   int changeLanes(Direction direction,
                   double startSpeed,
                   double endSpeed);
   int signalTurn(Direction direction,
                  boolean signalOn);
   int getRadarFront(double distanceToCar,
                     double speedOfCar);
   int getRadarRear(double distanceToCar,
                    double speedOfCar);
         ......
   // more method signatures
}
```

注意方法签名没有大括号包围的方法体有分号终结。

要使用接口，你学写一个类来实现implements这个接口。当一个科实例化的类实现一个接口是，他提供接口中定义的方法的方法体，例如：,

```java
public class OperateBMW760i implements OperateCar {

    // the OperateCar method signatures, with implementation --
    // for example:
    int signalTurn(Direction direction, boolean signalOn) {
       // code to turn BMW's LEFT turn indicator lights on
       // code to turn BMW's LEFT turn indicator lights off
       // code to turn BMW's RIGHT turn indicator lights on
       // code to turn BMW's RIGHT turn indicator lights off
    }

    // other members, as needed -- for example, helper classes not 
    // visible to clients of the interface
}
```

上面是机器人汽车例子中，需要实现接口的事汽车制造商。雪佛兰Chevrolet的实现可能与丰田Toyota的实现相当的不同，当然两家厂商都会遵循同样的接口。制导系统厂商，作为接口的消费者，创建系统用来根据汽车的GPS数据，数字地图，你及交通数据驾驶汽车。这么做的做，制导系统厂商只需调用接口中的方法: turn, change lanes, brake, accelerate等等。

## 接口做为API

机器人汽车的例子展示了接口作为工业标准*Application Programming Interface (API)*. APIs在商业软件中也同样常见。通常，一个公司出售的软件包包含了其他公司想要在他们的产品中使用的复杂方法。一个数字图像处理方法的软件包出售给制作终端用户平面设计软件的公司。图形处理公司写一些类来实现一个接口，这个类对他们的客户开放。平面设计软件公司通过使用接口中定义的方法签名和返回类型使用图形处理方法。这样在图形处理公司的API是公开的，但是API的实现作为私密信息得到保护——事实上他们可以在后续长期工作中根据其客户依赖的原有接口不断的改进其实现方法。