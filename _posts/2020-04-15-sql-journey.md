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

[参考文章-SQL优化器原理-查询优化器综述](https://zhuanlan.zhihu.com/p/40478975)

### 两层架构

SQL Layer + Storage Engine Layer 

### 查询执行流程

1. 客户端发起请求
2. 查询缓存 - 哈希值引用，所以任何文本的改变都可能导致缓存未命中
3. 解析器：先词法分析+语法分析，生成解析树
4. 基于代价的优化器：生成执行计划
5. 存储引擎接口：执行执行计划

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







# Hive



# Kylin



# Presto

