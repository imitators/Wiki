# java 核心概念解析

数据类型
String
运算
关键字
Object 公用方法
继承
反射
异常
泛型 (generic)
注解
特性

## 抽象

## 封装

private/public 的应用

### 成员变量

类中的变量

### 局部变量

类的方法中的变量

## 多态

## 继承

关键词: `extends`

### 面向接口思想

针对继承产生的复用问题，做到了定义与实现相分离。

面向接口思想建立在封装和面向对象之上。

> 面向对象(过程)解决数据的封装问题。

继承中，所有的父类方法必须实现，接口中，子类只需调用接口并指定算法族中的行为。

## 实现类

实现接口中的所有方法的类。

类只能实现接口，子类只能继承父类。

## JavaBean

JavaBeans 是 Java 中一种特殊的类，也是一种可重用的组件。名称中的“Bean”是用于 Java 的可重用软件组件的惯用叫法。

JavaBeans 通过提供符合一致性设计模式的公共方法将内部域暴露称为属性。

这种设计模式中包括：

- 参数使用 `private`
- 无参构造器
- 使用 `getParameter` 和 `setParameter` 获取和修改参数值
- 需要序列化

## 反射

反射是 java 的一种语法，具体操作为通过传入类名的字符串来新建类对象。

反射一定程度上破坏了面向对象，同时为编译时类之间的关系提供了解耦合（无需 import 其他类）。

### 动态代理

## 泛型

不指定类型，用到了再指定

```
<T>
```

## servlet

## 参考资料

[java基础](https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20%E5%9F%BA%E7%A1%80.md)