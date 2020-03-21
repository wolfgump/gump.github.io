---
layout: post
title: "Effective Java"
subtitle: ''
comments: false
author: "Gump"
header-style: text
date: 2020-3-20 20:30:21 +0800
tags:
    - Java 
    - 笔记
---

# effective java



## 考虑用静态工厂代替构造器

示例

```java
public static Boolean valueOf(boolean b){
	return b? Boolean.TRUE:Boolean.FALSE;
}
```



 类通过静态的工厂方法提供客户端实例，有以下优点：

- 静态工厂方法与构造器相比的一大优势在，他有名称；
- 不必每次调用的时候都创建一个新的对象
- 