# 设计模式

设计模式让程序高内聚、低耦合，以达到便于维护、扩展等目的。

## Creational Patterns

创建型模式 (Creational Patterns) 在创建对象时**隐藏创建的逻辑**，能让程序灵活决定创建的对象。

### Factory Pattern

工厂模式 (Factory Pattern) 将类的选择和创建留到子类中进行，主要解决了**接口选择**的问题。

以 Shape 为例，我们将创建一个 Shape 接口和实现 Shape 接口的实体类，下一步是定义工厂类 ShapeFactory。FactoryPatternDemo 类使用 ShapeFactory 来获取 Shape 对象。它将向 ShapeFactory 传递信息（CIRCLE / RECTANGLE / SQUARE），以便获取它所需对象的类型。

```
// Shape.java
public interface Shape{
    void draw();
}

// ShapeFactory.java
public Shape getShape(String Shape){
    if(shapeType == null){
        return null;
    }
    if(shapeType.equalsIgnoreCase("CIRCLE")){
        return new circle();
    } elseif...
}
```

## Behavioral Patterns

行为型模式 (Behavioral Patterns) 特别关注对象之间的通信。

### Strategy Pattern

在策略模式 (Strategy Pattern) 中，一个类的行为或其算法可以在运行时更改。

主要解决：在有多种算法相似的情况下，使用 if...else 所带来的复杂和难以维护。

何时使用：一个系统有许多许多类，而区分它们的只是他们直接的行为。

如何解决：将这些算法封装成一个一个的类，任意地替换。

关键代码：实现同一个接口。

*如果一个系统的策略多于四个，就需要考虑使用混合模式，解决策略类膨胀的问题。

## 可能的工作

SICP