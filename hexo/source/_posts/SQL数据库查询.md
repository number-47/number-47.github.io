---
title: SQL数据库查询
tags: SQL入门经典
categories: SQL
date: 2017-12-10 12:56:35
---
## Select语句

数据库查询语句(DQL)

```
select [* | distinct column1 , column2 ]
from   table [,table2]
where  [condition1 | expression1] [and | orcondition2 | expression2 ]
order by column1 | integer [ASC升序 | DESC降序]
```
distinct：在结果中去除重复的记录。
order by：输出结果以某种形式排序。默认升序asc 
**order by可以使用整数代表字段**<!--more-->
eg:
```
select *
from products_tbl
order by 1;
//上面查询语句输出的会按照products_tbl的第一个字段进行升序排序。
select *
from products_tbl
order by 1，2;
//上面查询语句输出的会先对products_tbl的第一个字段进行升序排序，再对第二个字段进行升序排序。
select *
from products_tbl
order by 1，2 desc;
//上面查询语句输出的会先对products_tbl的第一个字段进行升序排序，再对第二个字段进行降序排序。
```
## 统计表里的记录数量COUNT()
```
select COUNT(*)
from table_name;
//查询table_name的表中有多少行数据
如果统计的字段规定not null，那么统计结果和表里的数量相同
如果统计字段规定可以null，那么就只统计有数据的数据。
```
eg：
```
select COUNT(PROD_ID)
from PRODUCTS_TBL;
//统计PRODUCTS_TBL里字段PROD_ID的值的数量
```
## 使用字段别名
```
select column_name alias_name(别名)
from table_name
```
eg:
```
select prod_desc, prod_desc product
from products_tbl;
```
![sql字段别名输出](/images/img-sql字段别名输出.png)