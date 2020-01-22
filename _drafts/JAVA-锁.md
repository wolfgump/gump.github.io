# synconized

## 对象内存对象布局 

> https://www.jianshu.com/p/91e398d5d17c

12字节的头  markword

moniterenter

moniterexit 

lock cmpxcge

Cas 自旋

## 锁升级

> https://blog.csdn.net/tongdanping/article/details/79647337

偏向锁-->轻量级锁-->重量级锁



## ReentrantLock

适用场景：时间锁等候、可中断锁等候、无块结构锁、多个条件变量或者锁投票

## volatile

> 内存屏障实现 MESI

### 线程可见

应用实例：唯一ID解决时间回拨

### 禁止指令重排

应用实例：DCL

对象初始化过程：（半初始化）

```java
class T {
  long m=8;
}
T t1=new T();
```

- 初始化一个T,m=0
- 调用T的构造函数，m此时更新成8
- t1和T实例关联

如果在DCL中实例变量未加volite,在极端情况下发生了指令重排，上面的第三步和第二步发生了互换排序，有个线程拿到的t1是m=0的；





