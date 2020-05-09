---
layout: page
title: "周报"
date: 2020-04-02
author: ynwa
category: up
tags: stars
finished: false
---
## 2020-04-02开始
+ 定时：每晚19：30，提醒今日学习

+ 定时：每周日晚21：00，提醒周报，总结每日学习和每周文章的进展

+ 每周产出一篇面向面试的文章

  内容要和书本大致相同，不要自己发挥，看看2016-07-20-jvm文章就明白了，瞎扯淡啊，然后背也要背下来

+ 电脑每天带

  

## W1:20200402~20200405

### 学习材料

+ [HIVE-sql语句转换成MR](https://www.cnblogs.com/Dhouse/p/7132476.html)
+ [HIVE如何执行MR](https://www.cnblogs.com/grasser/p/9257933.html)
+ [MySQL-Understanding the query execution plan](https://dev.mysql.com/doc/refman/8.0/en/using-explain.html)
+ [!! Hive SQL转化为MapReduce执行计划深度解](https://blog.csdn.net/i000zheng/article/details/81082774)
+ [MySQL探秘(二)：SQL语句执行过程详解](https://juejin.im/post/5b7036de6fb9a009c40997eb)

### 目标 

sql贯穿我的9年java和4年数仓，在不同技术架构下的执行过程是不同的，其中原理也有差异，作为2个领域的专家，必须了解原理和性能调优

1. 先了解mysql和hive的sql执行过程，即执行计划是怎么来的

   **<u>本周先把这个文章写出来</u>**

2. 后续是sql方面的调优，mysql是索引和优化器，hive是mr优化和MapJoin优化器等

### 感悟

#### 简历与面试

+ 关于简历和面试
  FAB 法则的思路其实非常简单，就是你不但要说「是什么」、还要回答「好在哪里」以及「能给对方带来什么价值」。

  F:feature

  A:advantage

  B:beneifit

+ 给论据不给论点

+ 提供充足的证明

  1. 经历证明，大厂背景、项目经历
  2. 能力证明，当经历不够强则需要“能力证明”来补充
  3. 学习能力，对应届生和新人而言

### 周报：完成进展

## W2:20200407~20200412

### 目标

整理思路，按照各操作相关算法（JOIN/GROUP/DISTINCT等）、SQL历程（其中涉及到解析、优化，就需要关注CBO、RBO的区别）、索引原理等

按这个思路，sql原理就能比较精通，各种优化都能搞

-- 其实这个P6程度应该都能搞懂。。。。

### 感悟

数据治理，包含元数据、数据质量（包含源头治理、质量监控、SLA协议）、数据集市（主题域和业务线、指标定义和层级）


## W3:20200413~20200419

### 学习资料

1. [美团技术文章-领域模型的实践](https://mp.weixin.qq.com/s?__biz=MjM5NjQ5MTI5OA==&mid=2651747236&idx=1&sn=baf67052ec1961c3c6de1af26fba9b22&chksm=bd12aae98a6523ff90b3461d00fee548554fdeb2112b541de87d0c59dea45bc60d2f5211d6a6&scene=21#wechat_redirect)
2. [博客-网易flink-林小铂](http://www.whitewood.me/about/)
3. [分布式ID](https://mp.weixin.qq.com/s/8CGN6aeMy9UuI58ZWlUGEg)
4. [美团技术文章-数据治理平台的建设与实践](https://mp.weixin.qq.com/s/eQZH7HEwfgC1rzLjgSaIOw)
5. [spark streaming与flink的比较](https://zhuanlan.zhihu.com/p/40698254)
6. [flink学习资料大合集](https://juejin.im/post/5d67c61a6fb9a06b0a278988)
7. [宝藏-Spark VS Flink 下一代大数据计算引擎之争，谁主浮沉（上）](https://ververica.cn/developers/big-data-computing-engine-battle/)

### 要求

1. 熟练掌握Hadoop、Hive、Hbase、zookeeper、kafka等分布式框架；熟悉spark相关环境和工作原理
2. 精通主流Oracle、mysql、MongoDB、redis、elasticsearch

### 目标

文章：flink与spark streaming的区别

### 感悟

维度建模和合理的分层能够解决业务在使用数仓中的遇到的问题吗？

数据治理和数据赋能的关系是啥？

### 自我介绍

突出每个阶段的重点

1. 微易：数仓已经搭建完成，围绕埋点展开的，流量分析（spark）-> 画像（主题域的构建）-> 实时（flink）
2. 政采云：0-1的搭建数仓，数仓分层分主题
3. 大搜车：数据治理



# W4：20200420~20200424

### 方向

<b> 背面试题！背面试题！背面试题！</b>

Hadoop、Hive、Spark、Flink、Zookeeper、分布式

### 面试题

1. [Hadoop面试题](https://www.aboutyun.com//forum.php/?mod=viewthread&tid=25195&extra=page%3D1&page=1&)
2. [Flink面试题1](https://juejin.im/post/5de90b586fb9a016502f3c36#heading-4)
3. [Flink面试题2](https://blog.csdn.net/huzechen/article/details/102827576)
4. [王知无](https://shimo.im/docs/jdPhrtFwVCAMkoWv/read)



# W5：20200426~20200430

### 学习资料

1. [实时流处理系统反压机制 - 综述](https://blog.csdn.net/qq_21125183/article/details/80708142)
2. [Flink如何优雅解决反压，涉及内存管理](https://yq.aliyun.com/articles/64821)
3. 





## W6：20200506~20200509

### 学习资料

1. [kafka常见面试题](https://zhuanlan.zhihu.com/p/89294602)
2. Flink 的2个使用场景，实时用户订单标签、用户页面复杂事件



>  技术上主要是技术的深度与广度，分布式系统的稳定性（如，服务注册发现，限流，熔断，幂等，核对）。  知道中间件的原理，选型理由等



### 分布式

> **开发高并发系统时，有三把利器用来保护系统** ：缓存、限流、降级

#### 限流

