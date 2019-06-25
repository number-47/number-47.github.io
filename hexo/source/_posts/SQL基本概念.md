---
title: SQL基本概念
date: 2017-12-10 12:56:35
tags: SQL入门经典
categories: SQL
---

## 概念

## DBMS（数据库管理系统）

**数据库管理系统**，数据被保存在数据库中，这种机制叫做数据库管理系统。

**RDBMS:**关系型数据库管理系统。
## DBA（数据库管理员）

**数据库管理员**

## DBS(数据库系统)

由数据库、数据库管理系统（及其应用的开发工具）、应用数据和DBA组成的存储、管理、处理和维护数据的系统。

## SQL

**结构化查询语句**是与关系型数据库进行通信的标准语言。<!--more-->

## SQL会话

用户利用SQL命令与关系型数据库进行交互时发生的事情。当用户与数据库建立连接时，会话就被建立了。会话可以通过直接与数据库建立链接来申请，也可以通过前端程序来申请。无论何种情况，会话通常是由通过网络访问数据库的用户在终端或工作站建立的。

## CONNECT

命令**CONNECT**用于建立与数据库的连接，它可以申请连接,也可以修改连接。当用户连接到数据库时，SQL会话就被初始化了。

命令如下

```SQL
CONNECT user@database
```

## DISCONNECT/NEXT

命令**DISCONNECT**用于断开用户与数据库的连接。当用户连接到数据库时，SQL会话就被结束了。

当使用**EXIT**命令离开数据库时，SQL会话就结束了，而且用于访问数据库的软件通常会关闭。

## SQL命令的类型

### DDL—数据库定义语言

**DDL**用于创建和重构数据库对象。

基本的DDL命令：

```sql
CREATE TABLE
ALTER TABLE
DROP TABLE
CREATE INDEX
ALTER INDEX
DROP INDEX
CREATE VIEW
DROP VIEW
```



### DML—数据库操作语言

**DML**用于操作关系型数据库对象内部的数据。

基本命令：

```sql
INSERT
UPDATE
DELETE
```



### DQL—数据查询语句

基本命令`SELECT`

### DCL—数据控制语言

**DCL**用于控制对数据库里数据的访问，通常用于创建与用户访问相关的对象，以及控制用户权限。

基本命令：

```sql
ALTER PASSWORD
GRANT
REVOKE
CREATE SYNONYM
```

### 数据管理命令

用于对数据库里的操作进行审计和分析，还有助于分析系统性能。

基本命令：

```
START AUDIT
STOP AUDIT
```

### 事务控制命令

用于管理数据库事务

```sql
COMMIT //保存数据库事务
ROLLBACK //撤销数据库事务
SAVEPIONT //在一组事务里创建标记点以用于回退（ROLLBACK）
SET TRANSACTION //设置实物名称
```

