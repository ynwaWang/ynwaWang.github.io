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

[hadoop的mapReduce和Spark的shuffle过程的详解与对比及优化](https://blog.51cto.com/machenjie/1968921)

[MapReduct的shuffle过程详解](https://matt33.com/2016/03/02/hadoop-shuffle/)

[yarn详解](https://www.ibm.com/developerworks/cn/opensource/os-cn-hadoop-yarn/)



### hive

[hive性能优化面试题](https://zhuanlan.zhihu.com/p/65436503)

hive分为几种表:内部表/外部表/分区表/桶表

[hive性能调优-计算分配的map和reduce个数](http://www.voidcn.com/article/p-mjvjishu-bgd.html)

[hive性能调优-关键参数](https://blog.csdn.net/boyu_tung/article/details/52878434)

[hive性能优化-10条](https://www.cnblogs.com/frankdeng/p/9463897.html)

### spark

<u>√</u>  [Spark作业调度中stage的划分](https://wongxingjun.github.io/2015/05/25/Spark%E4%BD%9C%E4%B8%9A%E8%B0%83%E5%BA%A6%E4%B8%ADstage%E7%9A%84%E5%88%92%E5%88%86/)

+ 为什么要划分stage：划分stage的依据是宽依赖，从性能优化和失败恢复上考虑，窄依赖更佳；无法避免宽依赖的情况下，划分出来就有优化的空间

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

+ ES：倒排索引/反向索引
+ mysql：存储引擎级别的概念，InnoDb 聚集索引

### Flink

[aliyun-实时计算 Flink SQL 核心功能解密](https://yq.aliyun.com/articles/457438?spm=a2c4e.11153940.0.0.737e1ff1tqwrhv)

EventTime+Watermarks机制处理乱序问题

Flink+cep解决复杂事件问题

[Exactly-once](http://www.whitewood.me/2018/10/16/Flink-Exactly-Once-%E6%8A%95%E9%80%92%E5%AE%9E%E7%8E%B0%E6%B5%85%E6%9E%90/)

+ 定义Exactly-once语义，需先定义at-least-once语义。
+ 消息投递要考虑3种情况：正常返回、错误返回、超时，其中错误返回还要分可重试错误返回和不可重试错误返回。可重试错误返回和超时的情况都需要重发消息，来保证at-least-once的语义。
+ 在at-least-once语义的基础上，保证重发的消息只被消费一次或者从业务结果来看只被消费了一次，这就需要可识别重发消息或者消息消费的幂等性





## 一专多能
### 数仓

1. 0-1的数仓建设,基于用户画像项目重构数仓规范,结果是2套规范并行
2. 2套数仓并行,集市的开发模式到统一数仓开发模式的转变:多条业务线涉及多个主题域的梳理,建立数仓
3. 集市和数仓构建模式的思考,分层定位的思考,按主题迁移的思考

总结来说,很多人都能切身体会到集成/稳定/随时间变化这3个数仓特征,比如提供跨业务线的数据导出功能和集中展示功能/每日脚本的幂等性/缓慢变化维的处理,但是对于第一个:面向主题,理解就没有那么深入.

为什么面向主题是第一个特征?



### hadoop生态圈

1. hive的性能优化，主要是数据倾斜的原理和解决方案
2. spark：stage划分的原理、spark对MR的优化
3. ElasticSearch和mysql的索引原理
4. flink：
5. 是否放弃hbase？



## 自我介绍该说什么？ 

> 个人能力的成长经历，什么阶段学会了什么，目前的能力特长是什么，解决过什么难点痛点问题，怎么分析怎么落地实现，拿到什么结果，一两个例子能反映你的核心能力



star：

situation 背景

task 工作任务

action 采取的行动

result 结果



1. 你如何理解你应聘的岗位？做什么？
2. 你认为需要具备什么资格？
3. 你具备哪些资格？
4. 有什么事件可以印证？



#### 当前阶段思考的问题是：维度建模方法论如何在日常工作中践行?

1. 需求分析
2. 建模设计



思考的重点：

重构和迁移、文档化、分层分主题（重要的不是怎么分，而是为什么这么分）



3个月工作总结:

1. 带人（一个月）： 重构+数仓建模步骤,如何做需求分析,如何以数仓建模的角度去阅读ETL代码
   + 一个问题：数仓招人的标准是啥，是开发技能还是建模思维？
2. 团队管理角度：周报规范、周会规范(讨论重构和模型review)、新人指引和tips
   + 利弊不明：团队管理有缺陷的团队，我发挥了什么作用，改进了什么？
3. 负责的业务模型：风控订单模型、GPS模型和指标、画像重构、智明（供应链的快照+明细）、新车二网、数仓分层模型讨论



#### 团队的问题

团队放养、主题不明、职责不分、交接不清、文档不写

想试行轮岗和需求池的制度，做好交接、知识分享、团队协作，但是领导不认可，我只能在小组内进行推广

> 应用+模型，实际上日常工作还是以对接业务和产品需求为主



# 计算连续日期

```sql
with data_room as (
    select 9999589 as roomid,'2017-01-01' as pt_day
    union all
    select 9999589 as roomid,'2017-01-02' as pt_day
    union all
    select 9999589 as roomid,'2017-01-04' as pt_day
    union all
    select 9999589 as roomid,'2017-01-05' as pt_day
    union all
    select 9999589 as roomid,'2017-01-06' as pt_day
    union all
    select 9999589 as roomid,'2017-01-07' as pt_day
    union all
    select 9999589 as roomid,'2017-01-12' as pt_day
    union all
    select 9999589 as roomid,'2017-01-13' as pt_day
    union all
    select 9999589 as roomid,'2017-01-15' as pt_day
)

-- select roomid,min(pt_day) continuity_frist_day,max(pt_day) continuity_last_day,count(*) continuity_days
select roomid,pt_day,rn,date_sub(pt_day,rn)
from (
	select roomid,to_date(pt_day) pt_day,row_number()over(partition by roomid order by to_date(pt_day) asc) rn
	from data_room 
	where roomid=9999589 and pt_day between '2017-01-01' and '2017-01-16'
) x     
-- ) x group by roomid,date_sub(pt_day,rn) 
```



| roomid  | pt_day     | rn   | Date_sub(pt_day,rn) |
| ------- | ---------- | ---- | ------------------- |
| 9999589 | 2017-01-01 | 1    | 2016-12-31          |
| 9999589 | 2017-01-02 | 2    | 2016-12-31          |
| 9999589 | 2017-01-04 | 3    | 2017-01-01          |
| 9999589 | 2017-01-05 | 4    | 2017-01-01          |
| 9999589 | 2017-01-06 | 5    | 2017-01-01          |
| 9999589 | 2017-01-07 | 6    | 2017-01-01          |
| 9999589 | 2017-01-12 | 7    | 2017-01-05          |
| 9999589 | 2017-01-13 | 8    | 2017-01-05          |
| 9999589 | 2017-01-15 | 9    | 2017-01-06          |

