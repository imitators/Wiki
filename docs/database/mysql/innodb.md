# InnoDB

## 存储

在 InnoDB 存储引擎中，所有的数据都被逻辑地存放在表空间中，**表空间**（tablespace）是存储引擎中最高的存储逻辑单位，在表空间的下面又包括**段**（segment）、**区**（extent）、**页**（page）。

默认页空间为 16KB。最小区空间为 1MB。页数量最少为 64 个。

页是 InnoDB 进行磁盘管理的最小单位。

## 文件结构

InnoDB 会将**表的定义**存储在 .frm 文件中，**数据索引等信息**存储在 .ibd 文件中。

### .ibd

## index

### B+ tree index

B+ 索引语句和哈希索引在进行范围搜索或者模糊查询 (fuzzy query) 时，优势明显。

### hash index

哈希索引和 B+ 索引语句等价时，优势明显。

大规模数据容易出现 hash 冲突问题 (hash collision problem)。
