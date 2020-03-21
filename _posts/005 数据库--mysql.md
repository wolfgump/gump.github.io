## What Datatype Should You Use? We Compare Datetime, Timestamp and INT.

Based on this data, I believe Datetime is the best choice in most scenarios. Here’s why:

- It’s faster (according to our three benchmarks).
- It is human-readable without any conversion.
- There are no problems due to time zone switching.
- It uses only 1 byte more than its counterparts.
- It allows for a greater date range (from year 1000 to 9999).

## Mysql索引

### 为什么必须要主键，整型自增

- B+索引，必须有主键
- 整型，存储空间小，一个page内能过存储更多的索引值；比较速度快
- 自增，插入新数据快，不必重新组织索引

### 为什么索引用B+树，不是红黑树、HashMap、跳表

- 红黑树等二叉树会导致索引层次过高，查找速度慢；B+是多叉树能够降低树的层次，并且一次磁盘IO能够读取更多的索引值
- HashMap 无法进行范围查询
- 跳表很类似B+树了，B+只有叶子节点才存储树，一个page内能够放下更多的索引，减少磁盘IO的次数

## ACID

- MySql ACID的实现

  https://www.cnblogs.com/kismetv/p/10331633.html

- Mysql RC RR的选择

  https://www.javazhiyin.com/33516.html

- 事物隔离级别

  隔离性主要区别在读
  RR RC 使用MVVC+排他锁
  RR 写（当前读）会加间隙 

  RR更多应用场景是在报表中

java spring 同类方法调用 expection不回滚

## mysql 默认RR的原因

5.0以前binlog设计只支持statment,

