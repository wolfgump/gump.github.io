# Reids

## 前世今生

### 磁盘存储

存在两个限制

- 寻址，时间在ms级别（s>ms>us>ns）; 内存的寻址时间在ns
- 带宽，百兆；
- 全量IO

### 数据库

- 分治

  数据库在磁盘上存储文件的最基本单位是datapage(mysql的datepage默认大小是16KB),相对于全量IO，如果知道数据在哪个datapage内，只需要读取这个datapage就行了

- 索引

  如何知道数据在哪个datapage内，就需要通过索引

存在问题：

数据量太大后，受带宽和磁盘IO限制，也会变慢

## SAP HANA数据

全内存的SQL数据库，加个很贵

## Redis

相比HANA只放热点数据到内存，成本低；和Mysql比内存读取，速度快

### Value有类型

Memcache的key和value都是String类型

类型对应的就有和类型对应的方法;有了方法服务端能做的事情就多了；否则像memcahe要把key对应的数据全拉下来在客户端操作。

### 单线程还是多线程

业务处理线程是单线程

Redis Server是多线程，做数据落盘之类的

为什么单线程？

> 不用上下文切换，没有并发问题

### BIO->NIO->多路复用NIO

BIO（同步阻塞IO）造成线程阻塞

NIO(同步非阻塞IO) 之select模型，不会线程阻塞，但是会让内核循环次数多；

> 过程：假如有一千个客户端连接，redis server通过select把一千个连接的文件描述符给到内核，内核循环一千个描述符

多路复用NIO(同步非阻塞)  之epoll模型，通过事件机制，有数据写入后内核把有数据的文件描述符放到一个指定位置，redis server的epoll_wait循环读取这个空间

> 同步是最终的数据读取还是由redis server来read,read 是一个同步过程

AIO(异步非阻塞)，发展不太理想，Redis和Netty都没有用

### Redis 在微服务里设计问题

<img src="../img/redis/redis_issue.jpeg" alt="redis_issue" style="zoom:25%;" />

- 如果通过客户端对Redis的多次操作经过nginx转发后分别由购物车1和购物车2发起了redis操作，如果出现网络波动可能先发起的网络请求后到达redis,redis是单线程线性处理的，就出问题了

  > 解决办法：复杂均衡算法通过hash算法，同一个客户端路由到同一个服务器上

### Redis 6.x

新特性：IO多线程

之前处理是IO读取 处理...IO

读取 处理;Reids6.x 是开启多个IO线程，线性IO读取数据，然后单线程处理数据



### Value类型

#### String

- String

- int

  Incre decre  用于秒杀扣减库存、点赞数、浏览数

- Bitmap

  bitop、bitcout 、setbit 用于统计一段时间活跃用户数

#### List

双向链表，key有指向头尾的两个指针

同向命令就是栈

异向命令就是队列

使用场景：唯一ID Segment方案

#### Hash

使用场景：详情页

#### Set

无序/去重

SRANDOMember  抽奖

SPOP 单独抽奖，每次抽一个人

SDIFF 一度好友推荐

SINTER 共同兴趣推荐

#### SortSet

有序Set,跳表实现

使用场景：排行榜

ZAdd

ZScore

ZRank

### 二进制安全

Redis Server不参与编码解码，只接受字节数组；编码和解码都是客户端来做的；

