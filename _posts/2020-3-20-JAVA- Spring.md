---
layout: post
title: "Spring"
subtitle: ''
comments: false
author: "Gump"
header-style: text
date: 2020-3-20 20:30:21 +0800
tags:
    - Java 
    - 开源项目
    - 笔记
---

# JAVA-- Spring

## Bean生命周期

1、解析Bean配置信息，將配置信息转换为BeanDefinition对象，注册到BeanDefinitionRegistry中。

2、执行所有的BeanFactoryPostProcessor的postProcessBeanFactory（）方法对Bean工厂信息进行修改，包括修改或新增BeanDefinition对象。

注意：如果需要控制BeanFactoryPostProcessor的执行顺序需要实现PriorityOrdered接口，getOrder（）方法返回的值越小，执行优先级越高。

3、通过BeanDefinition对象实例化所有Bean，注入依赖。

4、执行所有BeanPostProcessor对象的postProcessBeforeInitialization（）方法。

5、执行Bean的初始化方法，例如InitializingBean接口的afterPropertiesSet方法，或init-method属性指定的方法。

执行所有BeanPostProcessor对象的postProcessAfterInitialization（）方法


## IOC容器

ioc容器是一个线程安全的hashmap,ConcurrentHashMap

## ObjectProvider

在一些场景下替代@AutoWired, 特别是在框架代码中；@AutoWired是强依赖，找不到对应的bean会报错，不确定Bean一定存在的情况下可以用objectProvider的getIfAvailable,另外还提供了另外一个方法getIfUnique

## BeanDefinitionRegistry

BeanDefinition容器，所有的Bean定义都注册在BeanDefinitionRegistry对象中。

## ImportBeanDefinitionRegistrar

ImportBeanDefinitionRegistrar是一个接口，该接口的实现类作用于在Spring解析Bean配置生成BeanDefinition对象阶段。
在Spring解析Configuration注解时，向Spring容器中增加额外的BeanDefinition。

## BeanFactoryPostProcessor

在容器的启动阶段， BeanFactoryPostProcessor允许我们在容器实例化相应对象之前，对注册到容器的BeanDefinition所保存的信息做一些额外的操作，比如修改bean定义的某些属性或者增加其他信息等。

## BeanPostProcessor

其存在于对象实例化阶段。跟BeanFactoryPostProcessor类似，它会处理容器内所有符合条件并且已经实例化后的对象。简单的对比，BeanFactoryPostProcessor处理bean的定义，而BeanPostProcessor则处理bean完成实例化后的对象

## Aware

作用就是在对象实例化完成以后将Aware接口定义中规定的依赖注入到当前实例中;

ApplicationContextAware接口，实现了这个接口的类都可以获取到一个ApplicationContext对象。

## @ImportAutoConfiguration

与@EnableAutoConfiguration的功能更相似，而且能够更细粒度的控制导入的类。

## BeanDefinitionRegistryPostProcessor

用于在BeanDefinition对象注册完成后，访问、新增或者修改BeanDefinition信息。

## CommandLineRunner

程序启动时执行一些动作

## EnvironmentAware

凡注册到Spring容器内的bean，实现了EnvironmentAware接口重写setEnvironment方法后，在工程启动时可以获得application.properties的配置文件配置的属性值。



# spring boot

# spring cloud

## spring cloud netfix

**feature**

- Service Discovery: Eureka instances can be registered and clients can discover the instances using Spring-managed beans
- Service Discovery: an embedded Eureka server can be created with declarative Java configuration
- Circuit Breaker: Hystrix clients can be built with a simple annotation-driven method decorator
- Circuit Breaker: embedded Hystrix dashboard with declarative Java configuration
- Client Side Load Balancer: Ribbon
- External Configuration: a bridge from the Spring Environment to Archaius (enables native configuration of Netflix components using Spring Boot conventions)
- Router and Filter: automatic registration of Zuul filters, and a simple convention over configuration approach to reverse proxy creation

Q:为什么在Spring Cloud项目中可以直接在配置文件中配置Hystrix属性？

A:Hystrix用Archaius做了动态配置，Spring cloud桥接了Archaius,所以spring cloud的配置文件相对于Hsytrix的配置文件

