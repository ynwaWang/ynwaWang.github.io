---
layout: page
title: "sql历程"
date: 2020-04-15
author: ynwa
category: up
tags: stars
finished: false
---



# MySQL

[参考文章-步步深入：MySQL架构总览->查询执行流程->SQL解析顺序](https://www.cnblogs.com/annsshadow/p/5037667.html)

[参考文章-mysql group by 底层原理](https://www.cnblogs.com/pc-boke/articles/9916594.html)

### 两层架构

SQL Layer + Storage Engine Layer 

### 查询执行流程

1. 查询缓存 - 哈希值引用，所以任何文本的改变都可能导致缓存未命中
2. 解析器：先词法分析+语法分析，生成解析树
3. 基于代价的优化器：生成执行计划
4. 存储引擎接口

### SQL解析顺序

```sql
FROM <left_table>
ON <join_condition>
<join_type> JOIN <right_table>
WHERE <where_condition>
GROUP BY <group_by_list>
HAVING <having_condition>
SELECT 
DISTINCT <select_list>
ORDER BY <order_by_condition>
LIMIT <limit_number>
```

### SELECT原理



### JOIN原理

Nested-Loop Join 和Block Nested-Loop Join

### Group原理

#### 松散索引

using index for group-by

- 聚合函数都只能限定为min和max

#### 紧凑索引

using where, using index

#### 临时文件

using filesort，也就是建立临时表，对文件进行排序



# Hive



# spark





# Kylin



# Presto

