---
layout: page
title: "数仓面试题"
date: 2019-07-02
author: ynwa
category: up
tags: stars
finished: false

---

### Hadoop

MapReduce的运行过程/运行原理

shuffle的过程

yarn的底层原理



### 数据仓库

数据倾斜

hive分为几种表:内部表/外部表/分区表/桶表

### spark

<u>√</u>  [Spark作业调度中stage的划分]([https://wongxingjun.github.io/2015/05/25/Spark%E4%BD%9C%E4%B8%9A%E8%B0%83%E5%BA%A6%E4%B8%ADstage%E7%9A%84%E5%88%92%E5%88%86/](https://wongxingjun.github.io/2015/05/25/Spark作业调度中stage的划分/))

如何控制task执行的并发量

spark任务优化/提高运行速度

spark提交一个job之后的运行过程

spark shuffle过程   和  hadoop shuffle的区别

### HBase

Hbase读取数据的过程

master和regionserver的交互

### Elasticsearch

底层查询机制

<em>?</em> [为什么查询快,实际上是索引机制的问题](https://blog.csdn.net/qq924862077/article/details/80382634)

### Flink

[aliyun-实时计算 Flink SQL 核心功能解密](https://yq.aliyun.com/articles/457438?spm=a2c4e.11153940.0.0.737e1ff1tqwrhv)

Exactly-once

窗口/水位





## 一专多能
### 数仓

1. 0-1的数仓建设,基于用户画像项目重构数仓规范,结果是2套规范并行
2. 2套数仓并行,集市的开发模式到统一数仓开发模式的转变:多条业务线涉及多个主题域的梳理,建立数仓
3. 集市和数仓构建模式的思考,分层定位的思考,按主题迁移的思考

总结来说,很多人都能切身体会到集成/稳定/随时间变化这3个数仓特征,比如提供跨业务线的数据导出功能和集中展示功能/每日脚本的幂等性/缓慢变化维的处理,但是对于第一个:面向主题,理解就没有那么深入.

为什么面向主题是第一个特征?



## 自我介绍该说什么？ 

> 个人能力的成长经历，什么阶段学会了什么，目前的能力特长是什么，解决过什么难点痛点问题，怎么分析怎么落地实现，拿到什么结果，一两个例子能反映你的核心能力



维度建模方法论如何在日常工作中践行?

1. 需求分析
2. 建模设计



3个月工作总结:

1. 带了一个月新人: 重构+数仓建模步骤,如何做需求分析,如何以数仓建模的角度去阅读ETL代码
2. 建立周报制度/重构项目讨论制度/模型交接规范
3. 数仓分层模型讨论



团队的问题：

1. 主题不明、职责不分、交接不清、文档不写
2. 

