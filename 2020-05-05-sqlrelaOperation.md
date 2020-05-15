---
title: sql语句
date: 2020-05-05 09:42:32
categories: 
    - 数据库
tags: 
    - sql语句
---

# 概述

sql语句分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。

| SQL功能     | 动词                           |
| ----------- | ------------------------------ |
| 数据定义DDL | CREATE、DROP、ALTER            |
| 数据操纵DML | SELECT、INSERT、UPDATE、DELETE |
| 数据控制DCL | GRANT、REVOKE                  |

# 数据定义DDL

<table>
    <tr>
        <td rowspan="2">操作对象</td> 
        <td colspan="3">操作方式</td>
   </tr>
    <tr>
        <td >创建</td>
        <td>删除</td >  
        <td>修改</td > 
    </tr>
    <tr>
        <td>模式</td>
        <td>CREATE SCHEMA</td >  
        <td>DROP SCHEMA</td > 
        <td></td > 
    </tr>
    <tr>
        <td>表</td>
        <td>CREATE TABLE</td >  
        <td>DROP TABLE</td > 
        <td>ALTER TABLE</td >
    </tr>
    <tr>
        <td>视图</td>
        <td>CREATE VIEW</td >  
        <td>DROP VIEW</td > 
        <td></td >
    </tr>
    <tr>
        <td>索引</td>
        <td>CREATE INDEX</td >  
        <td>DROP INDEX</td > 
        <td>ALTER INDEX</td >
    </tr>
</table>
数据库->房子

模式->房间

表->房间里的各种各样的柜子

索引->记录柜子里存放东西的小本子

视图->将柜子里的东西按需取出后，展示给用户看

![image-20200505172706161](模式图.png)

## 模式

**创建**

为用户ZHANG创建一个模式TEST，并且在其中定义一个表TAB1

```sql
CREATE SCHEMA TEST AUTHORIZATION ZHANG
CREATE TABLE TAB1(COL1 SMALLINT,COL2 INT,COL3 CHAR(20));
```

**删除**

```sql
DROP SCHEMA TEST CASCADE;
//CASCADE:级联，删除模式时同时把下属数据库对象全部删除
//RESTRICT:如果已经定义了下属数据库则拒绝删除
```

## 表

**创建**

定义一个course表

```sql
CREATE TABLE Course
(Cno CHAR(9) PRIMARY KEY,//列级完整性约束条件，主码
 Cname CHAR(20) UNIQUE NOT NULL,//UNIQUE取唯一值,NOT NULL 列级完整性约束条件，不能为空
 Cpno Char(4)//先修课
 FOREIGN KEY(Cpno) REFERENCES Course(Cno)//表级完整性约束条件，Cpno是外码，被参照表是Course，被参照列是Cno
);
```

**修改**

向Course中增加课程学分,类型为INT

```SQL
ALTER TABLE Course ADD Cpoint INT;
```

修改Cno为INT

```sql
ALTER TABLE Course ALTER COLUMN Cno INT;
```

增加课程名称必须取唯一值

```sql
ALTER TABLE Course ADD UNIQUE(Cname)
```

**删除**

```sql
DROP TABLE Course CASCADE;
//CASCADE:级联，删除模式时同时把下属数据库对象全部删除
//RESTRICT:如果已经定义了下属数据库或视图则拒绝删除
```

注：在不同的数据库管理系统中CASCADE和RESTRICT处理策略，系统之间会存在差异。

## 视图

**建立**

建立ls视图

```sql
CREATE VIEW ls(Sno,Snamw,Grade)//如果涉及到两个表且有同名列需要声明视图中的属性列名
AS
SELECT Sno，Sname，Sage
FROM Student
WHERE Sdept='xinxi'
WITH CHECK OPTION;//当后续对该视图进行操作时，DBMS会自动加上Sdept='xinxi';
```

**删除**

删除视图bts

```
DROP VIEW bts CASCADE;
```

**查询**

在信息系统中查找年龄小于20的学生

```sql
SELECT Sno,Sage
FROM ls
WHERE Sage<20;//系统转化为WHERE Sage<20 AND Sdept='xinxi';
```

**更新**

将Sno=201215122学生姓名改为刘辰

```sql
UPDATE ls
SET Sname=‘刘辰’
WHERE Sno=‘201215122’;//系统转化为WHERE Sno=‘201215122’ AND Sdept='xinxi';
```

## 索引

**建立**

在SC表中按照Sno升序和Cno降序建立唯一索引SCno

```SQL
CREATE UNIQUE INDEX SCno ON SC(Sno ASC,Cno DESC)
```

**修改**

将SC表的SCno索引名改为SCSno

```sql
ALTER INDEX SCno RENAME TO SCSno
```

**删除**

删除student表中的stusname索引

```SQL
DROP INDEX stusname
```

# 数据操作DML

## 查询

查询全体学生姓名和出生年份

```sql
SELECT Sname,2014-Sage /*查询结果的第2列是一个算术表达式，2014-学生的年龄=学生出生日期*/
FROM Student;
```

| Sname | 2014-Sage |
| ----- | --------- |
| lili  | 1994      |

查询全体学生的姓名、出生年份和所在院系（院系用小写表示），出生年份使用别名‘birthday’

```sql
SELECT Sname,'Year of Birth:' birth,2014-Sage birthday,LOWER(Sdept)
FROM Student;
```

| name | birth          | birthday | department |
| ---- | -------------- | -------- | ---------- |
| lili | Year of Birth: | 1994     | cs         |

查询SC表中选课的学生号

```SQL
SELECT DISTINCT Sno//DISTINCT表示查询结果不重复，不加默认为ALL
FROM SC;
```

| Sno       |
| --------- |
| 201215121 |

### 条件查询

```sql
SELECT DISTINCT Sno
FROM SC
WHERE Sage<20;
```

### 范围查询

```sql
WHERE Sage NOT BETWEEN 20 AND 23
```

### 集合查询

```sql
WHERE Sage IN(20,21,22)
```

### 字符匹配

```sql
WHERE Sage LINK '2012%2'//%表示任意长度，_表示单个字符，\转义字符
```

### 空值查询

```sql
WHERE Grade IS NULL;
```

### 多重条件查询

```sql
WHERE Sdept='CS' AND Sage<20;
WHERE Sdept='CS' OR Sage<20;
```

### ORDER BY

查询全体学生，查询结果按所在系号升序排列，同一系中的学生按年龄降序排列。

```sql
SELECT *
FROM student
ORDER BY Sdept,Sage DESC;//升序为ASC
```

### 聚集函数

| 函数                          | 作用 |
| ----------------------------- | ---- |
| COUNT(※)                    | 统计元组个数 |
| COUNT([DISTINCT\|ALL]<列名>) | 统计一列中值的个数 |
| SUM([DISTINCT\|ALL]<列名>)  | 计算一列值的总和 |
| AVG([DISTINCT\|ALL]<列名>)  | 计算一列的平均值 |
| MAX([DISTINCT\|ALL]<列名>)  | 求一列的最大值 |
| MIN([DISTINCT\|ALL]<列名>)  | 求一列的最小值 |

查询选修1号课程的学生平均成绩

```sql
SELECT AVG(Grade)
FROM SC
WHERE Cno='1';
```

### GROUP BY

查询平均成绩大于等于90分的学生学号和平均成绩

```sql
SELECT Sno,AVG(Grade)
FROM SC
GROUP BY Sno
HAVING AVG(Grade)>=90;//聚集函数的条件查询
```

### 等值与非等值连接查询

```sql
SELECT Student.*,SC.*
FROM Student,SC
WHERE Student.SNO=SC.Sno;
```

### 自身连接查询

```sql
SELECT FIRST.Cno,SECOND.Cpno
FROM Course FIRST,Course SECOND
WHERE FIRST.Cpno=SECOND.Cno;
```

### 外连接

```sql
SELECT Student.Sno,Sname,Ssex
FROM Student LEFT OUTER JOIN SC ON(Student.Sno=SC.Sno)
```

### 嵌套查询

#### IN

```sql
SELECT Sno,Sname,Sdept
FROM Student
WHERE Sdept IN(
		SELECT Sdept
		FROM Student
		WHERE Sname='刘晨'
);

==>

SELECT Sno,Sname,Sdept
FROM Student S1,Student S2
WHERE S1.Sdept=S2.Sdept AND S2.Sname='刘晨';
```

IN 也可以替换为>、 <、 !=、 =、 >= 、<=、<>(非)

#### 谓词查询

ANY (SOME)某个值

ALL所有值

```SQL
SELECT Sname,Sage
FROM Student
WHERE Sage < ANY
			(
			SELECT MAX(Sage)
			FROM Student
			WHERE Sdept='CS'
			)
AND Sdept <> 'CS';			
```

#### EXISTS

返回“true”或“false”

若内层结果非空，WHERE语句返回真值，否则返回假值

### 集合查询

并操作UNION、交操作INTERSECT、差操作EXCEPT

```sql
SELECT *
FROM Student
WHERE Sdept='CS'
UNION(INTERSECT\EXCEPT)
SELECT *
FROM Student
WHERE Sage<=19
```

### 派生表

子查询放在FROM中

```sql
SELECT Sname
FROM Student,(SELECT Sno FROM SC WHERE Cno='1')AS SC1//AS指代别名
WHERE Student.Sno=SC1.Sno;
```

## 插入

普通版

```SQL
INSERT
INTO SC(Sno,Cno)
VALUES('201215128','1');

INSERT
INTO SC
VALUES('201215128','1',NULL,NULL);
```

混合版

对每个系先求学生平均年龄，并把结果存入数据库

```
INSERT
INTO Dept_age(Sdept,Avg_age)
SELECT Sdept,AVG(Sage)
FROM Student
GROUP BY Sdept;
```

## 修改

普通版

```sql
UPDATE Student
SET Sage=22
WHERE Sno='201215121';
```

自嗨版

```sql
UPDATE Student
SET Sage=Sage+1;
```

混合版

```sql
UPDATE SC
SET Grade=0
WHERE Sno IN
		(
        SELECT Sno
        FROM Student
        WHERE Sdept='CS'
        );
```

## 删除

普通版

```sql
DELETE
FROM Student
WHERE Sno='201215121';
```

自嗨版

```sql
DELETE
FROM Student;
```

混合版

```sql
DELETE
FROM Student
WHERE Sno IN
		(
        SELECT Sno
        FROM Student
        WHERE Sdept='CS'
        );
```

# 空值

产生

* 插入NULL
* 连接产生

判断：（WHERE 或 HAVING）IS NULL、IS NOT NULL

逻辑运算

| X Y  | X AND Y | X OR Y | NOT X |
| ---- | ------- | ------ | ----- |
| T T  | T       | T      | F     |
| T U  | U       | T      | F     |
| T F  | F       | T      | F     |
| U T  | U       | T      | U     |
| U U  | U       | U      | U     |
| U F  | F       | U      | U     |
| F T  | F       | T      | T     |
| F U  | F       | U      | T     |
| F F  | F       | F      | T     |

