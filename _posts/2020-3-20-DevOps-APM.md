---
layout: post
title: "DevOps"
subtitle: 'DevOps APM'
comments: false
author: "Gump"
header-style: text
date: 2019-10-31 20:30:21 +0800
tags:
    - DevOps
    - APM
    - 笔记
---

# APM 

## Logging, Metrics & Tracing

>https://www.dotconferences.com/2017/04/adrian-cole-observability-3-ways-logging-metrics-tracing

### 含义

Logging - recording events

Metrics - data combined from measuring events

Tracing - recording evets with causal ordering

### 作用

Log - easy to "grep",manally read

Metric - can identify trends

Trace - identify cause across services 

## Logging技术栈

ELK

##Metrics 技术栈

### Micrometer

Metrics界的log4j; 背后可以接各种具体的Metric实现，如prometheus、influxdb、JMX、zabbix

#### 概念

- Counter: 

  - 用途：measuring the rate at which some event is occurring over a given time interval.
  - 场景：Consider a simple queue. Counters could be used to measure things like the rate at which items are being inserted and removed.
  - 提示：**Never count something you can time with a `Timer` or summarize with a `DistributionSummary`**

- Guage
	
	- 用途：A gauge is a handle to get the current value
	
	- 场景：size of a collection or map or number of threads in a running state.
	
	- 提示：1.Gauges are useful for monitoring things with natural upper bounds. We don’t recommend using a gauge to monitor things like request count, as they can grow without bound for the duration of an application instance’s life. 
	
	  2.**Never gauge something you can count with a `Counter`!**
	
- Timer

  - 用途： measuring short-duration latencies, and the frequency of such events
  - 场景：

### DropWizard metric



## Trace 技术栈

业界标准 OpenTracing,目前支持这个标准的有：Uber Jaeger、Twitter Zipkin和Apache Skywalking