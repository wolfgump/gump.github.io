## What Datatype Should You Use? We Compare Datetime, Timestamp and INT.

Based on this data, I believe Datetime is the best choice in most scenarios. Here’s why:

- It’s faster (according to our three benchmarks).
- It is human-readable without any conversion.
- There are no problems due to time zone switching.
- It uses only 1 byte more than its counterparts.
- It allows for a greater date range (from year 1000 to 9999).

## 事物隔离级别

隔离性主要区别在读
RR RC 使用MVVC+排他锁
RR 写（当前读）会加间隙 
java spring 同类方法调用 expection不回滚
mysql 默认RR的原因是5.0以前binlog设计只支持statment,  RR更多应用场景是在报表中

## Mysql索引

### 为什么必须要主键，整型自增

- B+索引，必须有主键
- 整型，存储空间小，比较熟读快
- 自增，插入新数据快，不必重新组织索引