# JAVA-- 核心知识点

## volatile

https://www.ibm.com/developerworks/cn/java/j-jtp06197.html

## Optional

Optional.orElse() 包含了get

## SPI

### why

面向的对象的设计里，我们一般推荐模块之间基于接口编程，模块之间不对实现类进行硬编码。一旦代码里涉及具体的实现类，就违反了可拔插的原则，如果需要替换一种实现，就需要修改代码。为了实现在模块装配的时候不用在程序里动态指明，这就需要一种服务发现机制。java spi就是提供这样的一个机制：为某个接口寻找服务实现的机制

### 实现

在jdk6里面引进的一个新的特性ServiceLoader，从官方的文档来说，它主要是用来装载一系列的service provider。而且ServiceLoader可以通过service provider的配置文件来装载指定的service provider。当服务的提供者，提供了服务接口的一种实现之后，我们只需要在jar包的META-INF/services/目录里同时创建一个以服务接口命名的文件。该文件里就是实现该服务接口的具体实现类。而当外部程序装配这个模块的时候，就能通过该jar包META-INF/services/里的配置文件找到具体的实现类名，并装载实例化，完成模块的注入。

ServiceLoader可以加载不同jar下的META-INF/services/

### 应用场景

- dubbo 里的扩展点 https://dubbo.apache.org/zh-cn/docs/dev/SPI.html
- 数据库驱动
- Eclipse、idea 的插件

### 双亲委派模型

当一个类加载器收到类加载任务时，会先交给自己的父加载器去完成，因此最终加载任务都会传递到最顶层的BootstrapClassLoader，只有当父加载器无法完成加载任务时，才会尝试自己来加载。

## HashMap

hash算法：

```java
//计算Hash
static final int hash(Object key) {
        int hash;
        return key == null ? 0 : (hash = key.hashCode()) ^ hash >>> 16;
 }
//计算Index
int index = hash(key) & (capacity - 1)
```

求Hash:

获取对象的hashcode以后，先进行移位运算，然后再和自己做异或运算，即：hashcode ^ (hashcode >>> 16)，这一步甚是巧妙，是将高16位移到低16位，这样计算出来的整型值将“具有”高位和低位的性质;

求Index:

因为 A % B = A & (B - 1)，所以，(h ^ (h >>> 16)) & (capitity -1) = (h ^ (h >>> 16)) % capitity，可以看出这里本质上是使用了「除留余数法」

## ThreadLocal

存在的意义：

现在间的数据共享，原型的方法就要定义一个Map<Thread,Value>,这么做对同一个Map多线程访问，会有锁竞争，并发能力差

数据结构：

<img src="../img/java/threadlocal.png" alt="threadlocal" style="zoom:50%;" />

弱引用：

ThreadLocalMap的Key ThreadLocal是弱引用，当程序中不再用到ThreadLocal时，此时只剩ThreadLocalMap的弱引用，会被回收掉

问题：

ThreadLocalMap的Key是弱引用，value是强引用，就会出现key=null,value有值得情况，导致整个Entry不能回收；为了解决这个问题，ThreadLocalMap的get 和set每次都会线性探测key=null的Entry 清楚掉；但这不能彻底解决问题，比如最后一次get后，最后一次的Entry之后没有get set了，就清除不掉了，最坏的情况，这个线程在线程池中一直不释放，就导致线程泄漏，所以又增加了一个remove方法，在每次请求结束都要调用一次remove,防止最坏情况出现

hash冲突：

采用的是线性探测法解决

关键代码：

获取map: 直接获取当前线程的变量

```java
ThreadLocalMap getMap(Thread t) {
    return t.threadLocals;
}
```

