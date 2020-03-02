# DDD-领域驱动设计



## 理解

  为解决复杂软件设计和代码设计提供一套指导方法、标准、概念

- 结构分层 UI、APP、Domain、Infrastructure
- 核心概念 
  - 统一语言-- 方便业务专家 开发工程共同；UML 名词表
  - Entity
  - ValueObject
  - Repo
  - Domain Event--the state of the business changes (a change that matters to business experts)
  - Aggregate--bind *Entities* & *Value Objects* under the same root
  - Services-- business logic doesn’t belong to a given object
  - 上下文界限
  - CQRS

## 架构图

![img](https://miro.medium.com/max/2092/1*BlLLGEuH7Wtj2AIyFYzdUw.png)