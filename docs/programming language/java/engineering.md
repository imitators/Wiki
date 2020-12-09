# Java 工程化

java 规定，类文件中必须有和类名同名的类。

## IDE

### idea

正常情况下一个窗口一个项目，使用 modules 时能存在多个项目。

### eclipse

一个窗口多个项目。

## 项目构建

项目构建工具负责以下内容：

- 下载依赖
- 将源代码编译成二进制代码
- 打包生成的二进制代码
- 进行单元测试
- 部署到生产系统

### Maven 

Maven 负责项目构建，管理，jar 包下载和所有的包管理。

#### 目录结构

maven 目录结构（使用 modules 时）：

```
|-A module
    |-src
        |-main
        |   |-java
        |   |resource
        |
        |-test
        |   |-java
        |   |-resource
        |
        |-pom.xml：jar包的配置文件

B module
    src
    pom.xml

pom.xml：引入其他的pom.xml
```

微服务才需要多个 module。

#### pom.xml

maven 中的 jar 包配置文件。

## --常用框架--

## Spring

Spring 架构如下图所示，其中包含了功能模块和常用框架：

```
-----------------------------------------------------------------
|DAO            |ORM            |JEE            |Web            |
|               |               |               |               |
|Spring JDBC    |Hibernate      |               |Spring Web MVC |
|               |OJB            |               |Struts2        |
|               |ibatis         |               |               |
|               |               |               |               |
|-------------------------------|               |               |
|AOP                            |               |               |
|                               |               |               |
|Spring AOP                     |               |               |
|                               |               |               |
|---------------------------------------------------------------|
|Core                                                           |
|                                                               |
|The IOC container                                              |
-----------------------------------------------------------------
```

### DAO

DAO (Data Access Object) 模式是一种结构模式，它使用抽象API将应用程序/业务层与持久层（通常是关系数据库，但可以是任何其他持久性机制）隔离开。

sql语句

### AOP

### ORM

ORM (Object-relational Mapper, 对象关系映射)

### container

spring 容器就是实例化对象。

### IOC 控制反转

从主动获取变为被动获取。

例如 Class A 中用到了 Class B 的对象b，一般情况下，需要在 Class A 的代码中显式的 `new B()`。

采用依赖注入技术之后，A的代码只需要定义一个**私有的B对象**，不需要直接new来获得这个对象，而是通过相关的**容器控制程序**来将B对象在外部new出来并注入到A类里的引用中。而具体获取的方法、对象被获取时状态由配置文件（如XML）来指定。

#### DI 依赖注入

依赖注入有以下实现方式：

- 基于接口。实现特定接口以供外部容器注入所依赖类型的对象。
- 基于 set 方法。实现特定属性的public set方法，来让外部容器调用传入所依赖类型的对象。
- 基于构造函数。实现特定参数的构造函数，在新建对象时传入所依赖类型的对象。
- 基于注解。基于Java的注解功能，在私有变量前加“@Autowired”等注解，不需要显式的定义以上三种代码，便可以让外部容器传入对应的对象。该方案相当于定义了public的set方法，但是因为没有真正的set方法，从而不会为了实现依赖注入导致暴露了不该暴露的接口（因为set方法只想让容器访问来注入而并不希望其他依赖此类的对象访问）。

#### 依赖查找

依赖查找更加主动，在需要的时候通过调用框架提供的方法来获取对象，获取时需要提供相关的配置文件路径、key等信息来确定获取对象的状态

## MyBatis 框架

### ORM 对象关系映射

数据库表和java类的对应关系

entity、bean

### 动态sql

使用 `if choose trim foreach` 等逻辑来控制sql语句的形成。

```
<select id="findActiveBlogWithTitleLike"
     resultType="Blog">
  SELECT * FROM BLOG
  WHERE state = ‘ACTIVE’
  <if test="title != null">
    AND title like #{title}
  </if>
</select>
```

### criteria

mybatis通过反向工程生成的方法，用于查询反向工程生成的sql语句。

## 设计模式

### 策略模式(鸭子例子所用到的模式)

### 装饰者模式

## Data transfer object (DTO)

#### 枚举类型

一般用于状态码，在定义json格式后使用。

把所有的可能都封装在一个类中。