---
layout: page
title: "mysql事务原理"
date: 2016-07-21
author: ynwa.fuji
category: coding
tags: mysql
finished: false
---

## ACID描述事务属性
`> A tomicity`
原子性

`> C onsistency`
一致性

`> I solation`
隔离性

* Read Uncommitted
: 未提交读
* Read Committed
: 提交后才能读(一般的事务隔离性都做到这个程度)
* Repeatable Read
: 在一个事务中执行两次查询,如果间隙有提交的事务,那么我们会发现2次的结果不一致;此隔离级别就是解决这个问题的
* Serializable
: 对读加锁,所有操作都是串行的

`> D urabiity`
持久性

## 事务日志

`> 如何实现`

* 更新记录的内存版本
* 保存事务的日志,在一块特定的日志文件里执行顺序写入操作
* 定时把这些日志文件里的事务刷盘

`> 这个和大部分的db系统是相同的吗?比如redis的aof/mongodb的啥来着`

`> mysql的binlog?`


## MVCC实现事务
`> 在记录中增加2个隐藏字段`

* version
* deleteVersion

`> 每次事务开始,mysql自增事务序列号TID`

* 新增记录
: version = TID
* 更新记录
: 新增一条version = TID的新记录同时更新老记录deleteVersion = TID
: 与亚信的处理方式是相同的
* 删除记录
: 记录deleteVersion = TID
* 查询记录
: 查询version <= TID