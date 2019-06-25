---
title: SQL管理数据库对象
date: 2017-12-10 12:56:35
tags: SQL入门经典
categories: SQL
---

## 数据库对象

数据库里定义的、用于存储或是引用数据的对象，比如表、视图、簇、序列、索引和异名。

## 创建表

**CREATE TABLE 命令**

使用方法：

```
CREATE TABLE <表名>(
	<列名>  <数据类型>  [列级完整新约束],  //列级完整新约束 eg：primary key
	<列名>  <数据类型>  [列级完整新约束],  
	...
	[,<表级完整性约束>]
);
```

Eg:<!--more-->

```
CREATE TABLE EMPLOYEE_TBL(
	EMP_ID       CHAR(9)       NOT NULL,
	EMP_NAME     VARCHAR(40)   NOT NULL,
	EMP_ST_ADDR  VARCHAR(20)   NOT NULL,
	EMP_CITY     VARCHAR(15)   NOT NULL,
	EMP_ST       CHAR(2)       NOT NULL,
	EMP_ZIP      INTEGER       NOT NULL,
	EMP_PHONE    INTEGER       NULL,
	EMP_PAGER    INTEGER       NULL
);
```

## 修改表

**ALTER TABLE 命令**

### 修改表的列的属性

**列的属性：**数据类型、长度、有效位或标度、是否为空

```
ALTER TABLE <表名>
ADD [COLUMN] <新列名><数据类型>[完整新约束]
ADD <表级完整新约束>
DROP [COLUMN] <列名> [CASCADE|RESTRICT]
DROP CONSTRAINT<完整性约束名> [RESTRICT|CASCADE]
ALTER COLUMN <列名> <数据类型>
```

**CASCADE：**自动删除引用了该类的其他对象，如视图

**RESTRICT：**如果该列被其他对象引用，RDBMS拒绝删除该列

Eg：

```
//把EMP_ID的数据类型长度从9改为10.
ALTER TABLE EMPLOYEE_TBL 
ALTER COLUMN EMP_ID VARCHAR(10);


//新增EMP_ENGLISH_NAME列
ALTER TABLE EMPLOYEE_TBL
ADD EMP_ENGLISH_NAME VARCHAR(20);

//删除EMP_ENGLISH_NAME列
ALTER TABLE EMPLOYEE_TBL
DROP COLUMN EMP_ENGLISH_NAME;
```

#### 添加自动增加的列

使用IDENTITY类型

```
CREATE TABLE TEST_INCREMENT(
  ID   INT  IDENTITY(1,1) NOT NULL, //(seed = 1,increment = 1) 從1開始,每次遞增1  
  TEST_NAME VARCHAR(20)
);
```

##删除表

```
DROP TABLE <表名> [CASCADE|RESTRICT];
```

## 完整性约束

### 主键约束

### 唯一性约束

###外键约束



