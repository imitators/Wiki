# 功能点中的 SQLi 发现

## 排序功能

预编译对 order by 子句、表名、列名不生效，所以这类参数经常出现预编译后的 sql 注入。

## MyBatis

`#{param}` 表示对 param 使用预编译，`${param}` 则表示对 param 直接拼接。

研发 `省时省力` 地写代码，最终写出了 MyBatis 框架最常见的漏洞点。

模糊查询对比：

```
SELECT * FROM table_a WHERE name like concat('%', #{name} ,'%')

SELECT * FROM table_a WHERE name like '%${name}%'
```

批量处理对比：

```
// 传入字符串类型的 ids
SELECT * FROM table_a WHERE id IN (${ids})

// 传入集合类型的 ids
SELECT * FROM table_a WHERE id IN
<foreach collection="ids" item="id" open="(" separator="," close=")">
    #{id}
</foreach>
```

## RPC

如果某些功能突然调用了其他系统的接口时，需要格外留意，这种情况容易出现 SQL 注入。

开发和公司安全部门往往无法直接调用A系统中的接口，又不知道哪个系统调用了此接口，可能在测试B系统时才能证明 A 系统的接口存在 SQL 注入。

## 伪废弃接口

只在前端限制使用的接口很容易引发安全问题。

研发很容易在前端注释掉js/删除 HTML/删除首页代码，并且认为未来再用时可以节省时间。

## 弱编译型语言

强编译类型语言的类型比较严格，例如在 `Java` 中，`int` 型参数通常不会存在 SQL 注入和 XSS 漏洞。

弱编译类型的语言很可能转变数据类型，可以留意下，多测试。

不过很多弱类型语言的框架会强制数据类型，例如 `Django`。

## 隐藏参数

ORM 框架会为数据库中的字段与实体对象一一映射，数据库中有哪些字段，建立的实体中就会有哪些属性。

黑盒测试、扫描器不太容易发现隐藏参数的 SQL 注入。

白盒测试较难证明系统提供的 RPC 接口的安全性。

## 前端固定参数

任何前端只能返回某几个固定值的参数，很可能存在 SQL 注入。

甚至很可能原有漏洞被修改成了前端验证。

## HTTP Header 头

Header 头中，最常写入数据库的字段为 `Client-ip` 和 `X-Forwarded-For`，用来记录访问者的 ip。

如果改为判断 `Remote-Addr` 这类不可篡改的参数，漏洞就不复存在了。

时间参数是个很不错的注入点，开发人员的可能害怕处理导致出错，经常使用直接拼接，而不使用预编译。

## MySQL 不同位置的测试

### 表名/字段名

一般来说表名字段名，要么没有闭合字符，要么便是反单引号。

### where 子句

关键在于计算结果的一致性和不一致性。

#### 普通条件

字符型：

```
... where a = 'x'
// return null

... where a = 'x'-'x'
// return 所有数据
```

数字型：

```
4-1

3
```

#### 模糊查询

```
... where `bug_name` like '%输入点%'

?bugname='and'%'='
// return all

?bugname='and'x'='
// return null
```

### order by 子句

```
... order by {输入点1} {输入点2}

?order=1,1
?order=1,0
```

### limit 子句

limit 子句后面只能跟 PROCEDURE 子句和 INTO 子句，所以当注入点