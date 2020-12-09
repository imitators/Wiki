# SQL

SQL (Structured Query Language)

## 关键字

### 查询关键字

查询关键字 | 使用 | 名称/使用场景/注意事项
-|-|-
... **order by** id ASC/DESC | 根据 id 字段升序/降序排列
... **limit** 5<br/>... **limit** 3,2 | 返回 5 条结果<br/>返回从第 3 条开始的接下来 2 条结果
where name  (not) **like** 'k%' | 返回 name 字段中（不）以字母 k 开头的行
where name (not) **regexp/rlike** '^[GF]' | 返回 name 字段中（不）以字母 G 或 F 开头的行
where name **in** ('test1', 'test2') | 返回 name 字段中值为 test1 或 test2 的行
where num **between** 1 **and** 20<br/>where name **between** 'A' **and** 'H'<br/>where date **between** '2016-05-10' **and** '2016-05-14' | 返回 num 字段中**值**在 1 到 20 之间的行<br/>返回 name 字段中**首字母值**在 A 到 H 之间的行<br/>返回 date 字段中**日期值**在... | \*在不同的数据库中，BETWEEN 操作符会产生不同的结果
select name **as** n ... <br/>... from table **as** t ...<br/>select name, concat(url, ', ', alexa, ', ', country) **as** site_info from Websites; | 指定 name **列**别名为 n<br/>指定 table **表**别名为 t<br/>指定**自定义字段**别名为 site_info | 常用于两个或多个列/表结合在一起，可以省略不写<br/>\*如果**列名称包含空格**，要求使用双引号或方括号
from a **(inner) join** b **on** a.id=b.site_id | 返回 a 和 b 表中 a.id 字段和 b.site_id 字段相等的行 | **内连接**（**等值连接**）(a ∩ b)<br/>join 关键字基于两个或多个表之间的共同字段，把来自这些表的行结合起来<br/>\*对于 inner join 来说，on 和 where 的筛选结果没有区别
from a **left/right join** b **where** a.id=b.id | 返回 a 和 b 表中 a.id 字段和 b.id 字段相等时**左/右表**中的所有行<br/>如果右/左行没有匹配，此时另一表中**未匹配单元格**值为 null | **左连接/右连接** (a)/(b)<br/>对于 left/right/full join 来说，**on** 用于生成临时表，**where** 用于对临时表进行过滤
from a **full (outer) join** b on a.id=b.id where a.id=1 | 生成 a 和 b 表中 a.id 字段和 b.id 字段相等时所有行 | **外连接** (a ∪ b)<br/>left join 和 right join 的并集<br/>\*MySQL 不支持此语句，需要用 join + left join + union 模拟这种查询
from a **cross join** b | 返回 a 表中的行数乘以 b 表中的行数的**笛卡尔积** | **~~使用场景未知~~**
select id from a **union** select id from b; | 返回 a 和 b 表中不重复的 id 字段值 | \*union 只会选取不同的值，请使用 union all 来选取重复的值

#### 通配符

常常和 like 关键字同时使用

通配符 | 描述
-|-
% | 替代 0 个或多个字符
_ （下划线） | 替代 1 个字符
[charlist] | 字符列中的任何单一字符
^[charlist] | 脱字符 `^` 表否定
[^charlist]或[!charlist] | 不在字符列中的任何单一字符


#### 临时表(unknow)

数据库在连接多张表来返回记录时，都会生成一张临时表。

使用 left join 时，有如下差别：

on 条件是在生成临时表时使用的条件，它不管 on 中的条件是否为真，都会返回左边表中的记录。

where 条件是在临时表生成好后，再对临时表进行过滤的条件。这时不会受到 left join 的影响，条件不为真的就全部过滤掉。

对于 left join/right join/full join 来说，使用 on 和 where 结果存在不同。

### 增删改关键字

增删改关键字 | 使用 | 名称/使用场景/注意事项
-|-|-
**select** * **into** newtable from table; | 复制 table 表所有列并插入 newtable 表 | \*select into 先复制数据，再创建**相同结构的空表**，最后拷贝数据，所以要求目标表**必须不存在**<br/>\*MySQL 数据库不支持 SELECT ... INTO 语句，但支持 INSERT INTO ... SELECT
**insert into** b (id, name) **select** id1, name1 from a; | 复制 a 表中的 id1, name1 列并插入表 b 的 id, name 列 | \*insert into select 要求目标表**必须存在**
**create table** table1; | 创建表 table1
**creat database** db1; | 创建数据库 db1

## Constraints

约束 (constraint) 可以在创建表时规定 (create table)，或者在表创建之后规定 (alter table)。

违反约束的数据行为会被约束终止。

> 什么是数据行为？约束如何终止？

举个例子，create table + constraint 的代码如下所示：

```sql
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
```

### NOT NULL

NOT NULL 表示**某列数据非空**。

创建字段时添加约束：

```sql
CREATE TABLE table1 (
    ID int NOT NULL,
    LastName varchar(255),
    Age int
);
```

已有字段添加约束：

```sql
alter table table1 modify Age int NOT NULL;
```

删除约束：

```sql
alter table table1 modify Age int NULL;
```

> 大小写影响嘛？modify是啥玩意？

### UNIQUE

UNIQUE 表示**某列所有数据值都唯一出现**。

创建表时添加 UNIQUE 约束 (**MySQL**)：

```sql
CREATE TABLE table1
(
id int NOT NULL,
UNIQUE (id)
)
```
创建表时添加 UNIQUE 约束 (SQL Server / Oracle / MS Access)：

```sql
CREATE TABLE table1
(
id int NOT NULL UNIQUE
)
```

创建表时多行添加并命名 UNIQUE 约束：

```sql
CREATE TABLE table1
(
id int NOT NULL,
lastname varchar(255) NOT NULL,
CONSTRAINT constraint1 UNIQUE (id, lastname)
)
```

多行添加并命名 UNIQUE 约束：

```sql
ALTER TABLE table1
ADD CONSTRAINT constraint1 UNIQUE (id, lastname)
```

删除约束 (**MySQL**)：

```sql
ALTER TABLE table1
DROP INDEX constraint1
```

删除约束 (SQL Server / Oracle / MS Access)：

```sql
ALTER TABLE table1
DROP CONSTRAINT constraint1
```

### PRIMARY KEY

PRIMARY KEY 表示某列为主键，不能有 NULL。

> primary key 和 null 其中一个存在时，设置另一个会发生什么？
> 
> primary key 和 not null 只存在一个会怎么样？

创建表时添加 PRIMARY KEY 约束 (**MySQL**)：

```sql
CREATE TABLE table1
(
id int not null,
UNIQUE (id)
)
```

### FOREIGN KEY

外键约束。

## 原理



## 可能的工作

regex 是否支持更多正则

on 和 where 在实际场景中的差别

join时数据相同会出现什么？如果能正常输出，多条数据掺杂后，输出顺序如何？

cross join 的使用场景？和此时对应的数据结构？能否用于攻击？

