---
title: SQL事务
date: 2017-12-10 12:56:35
tags: SQL入门经典
categories: SQL
---

## 事务

事务(Transaction)是用户定义的一个数据库操作序列，这些操作要么全做，要么全不做，是一个不可分割的工作单位。

## 控制事务

###COMMIT命令

用于把事务所做的修改保存到数据库，把上一个COMMIT或ROLLBACK命令之后的全部事务都保存到数据库。

```
begin transaction
sql语句
commit;
```

<!--more-->

###ROLLBACK命令

用于撤销还没有被保存到数据库的命令，它只能用于撤销上一个COMMIT或ROLLBACK命令之后的实物。

```
begin transaction
sql语句
rollback;
```

eg:

```
begin transaction  
update products_tbl
set cost = 8
where prod_id = '11235';
rollback;

//上面语句会撤销更新的sql，不会让'11235'的prod_id更新为8，而是原来的值
```



###SAVEPOINT

保存点是事务过程中的一个逻辑点，我们可以把事务回退到这个点，而步兵回退到整个实物。

#### 创建savepoint

```
save transaction savepoint_name
```

#### 回退到savepoint

```
rollback transaction savepoint_name
```

eg:

```
BEGIN TRANSACTION

save transaction sp1   //保存点1  更新'11235'的cost为80
update products_tbl
set cost = 80
where prod_id = '11235';

save transaction sp2   //保存点2  更新'11235'的cost为99
update products_tbl
set cost = 99
where prod_id = '11235'

select *			//查询  得到'11235'的cost为99
from products_tbl;
  
rollback transaction sp2;  //回退到保存点2 得到'11235'的cost为80

select *		//查询  得到'11235'的cost为80

from products_tbl;
```



