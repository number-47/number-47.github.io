---
title: SQL数据类型
date: 2017-12-10 12:56:35
tags: SQL入门经典
categories: SQL
---

## SQL数据类型

- CHAR(n)：定长数据类型

- VARCHAR(n)：变长数据类型，n表示字段能够保存的最多字符数量

- BLOB：大对象类型，二进制大对象，保存很长的二进制字符串

- TEXT：长字符串类型，可以看作一个大VARCHAR字段<!--more-->




## 数值类型

- BIT(n)

- BIT VARCHAR(n)

- DECIMAL(p, s)

- INTEGER

- SMALLINT

- BIGINT

- FLOAT(p, s)

- DOUBLE PRECISION(p, s)

- REAL(s)
  p表示字段的最大长度
  s表示小数点后面的位数

## 小数点类型

DECIMAL(p, s)

p：有效位数

s：标度

```sql
eg:DECIMAL(4,2)  最大值为99.99
//有效位数是4，也就是数值总位数是4，标度是2小数点后面的位数
```

如果实际数值的小数位数超出定义的位数，数字就会被四舍五入。

##浮点数

**REAL：**单精度浮点数，单精度浮点数的有效位1—21（包含）

**DOUBLE PRECISION：**双精度浮点数的有效位22—53（包含）

## 日期和时间类型

- DATE

- TIME

- DATETIME

- TIMESTAMP

##直义字符串

  一系列字符，比如姓名或电话号码，这是有用户或程序明确指定的。

## 自定义类型

由用户定义的类型，允许用户根据已有的数据类型来定制自己的数据类型。

```SQL
MYSQL
//创建自定义类型
CRATE TYPE PERSON AS OBJECT
(NAME VARCHAR(30),
SSN VARCHAR(9));
//引用自定义类型
CREATE TABLE EMP_PAY
(EMPLOYEE PERSON,
SALARY DECIMAL(10,2),
HIRE_DATE DATE
);
```

## 域

域是能够被使用的有效数据类型的集合。域与数据相关联，从而只接受待定的数据，在域创建之后，我们可以向域添加约束，约束与数据类型共同发挥作用，从而限制字段能够接受的数据。

```
//创建域
CREATE DOMAIN MONEY_D AS NUMBER(8,2);
//添加约束
ALTER DOMAIN MONEY_D
ADD CONSTRANINT MONEY_CON1
CHECK (VALUE > 5);
//引用域
CREATE TABLE EMP_PAY
(EMP_ID NUMBER(9),
EMP_NAME VARCHAR2(30),
PAY_RATE MONET_D
);
```





  