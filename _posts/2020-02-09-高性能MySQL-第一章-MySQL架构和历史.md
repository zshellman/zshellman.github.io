---
layout: page
title: 高性能MySQL 第一章 MySQL架构和历史
mermaid: true
---

# 第一章 MySQL架构和历史

MySQL的逻辑架构

![1581255725010](..\img\mysql_logic.png)

第一层大多数基于网络的客户端/服务器的工具或者服务都有类似的结构。

第二层里大多数MySQL的核心服务功能都在这一层，包括查询解析、分析、优化、缓存以及所有的内置函数，所有的跨存储引擎的功能都在这一层实现：存储过程、触发器、试图等。

第三层包含了存储引擎，存储引擎负责MySQL中数据的存储和提取。服务器通过API与存储引擎进行通信。



MySQL中一条语句执行顺序

```flow
st=>start: 客户端
op=>operation: 连接器
cond=>condition: 是否在缓存
sub=>operation: 分析器
sub2=>operation: 优化器
sub3=>operation: 执行器
e=>end
e2=>end: 存储引擎

st->op->cond
cond(yes)->op
cond(no)->sub->sub2->sub3->e2
```


MySQL对于并发控制采用锁机制来处理，读锁，写锁。锁的粒度有表锁和行锁。

MySQL事务是就是一组原子性的SQL查询，或者说是一个独立的工作单元。

MySQL隔离级别：

- Read Uncommitted(读未提交)
- Read Committed（读取提交内容）
- Repeatable Read（可重读）
- Serializable（可串行化）

MySQL存储引擎：

- InnoDB：支持事务型引擎，默认存储引擎
- MyISAM：不支持事务





