---
title: 数据库关系代数
date: 2020-05-02 17:51:16
categories: 
    - 数据库
tags: 
    - 关系代数
---

关系代数是一种抽象的查询语言，用对关系的运算来表达查询

![关系运算符](guanxiyunsuanfu.png)

# 集合运算符

R:

| A    | B    | C    |
| ---- | ---- | ---- |
| a1   | b1   | c1   |
| a1   | b2   | c2   |
| a2   | b2   | c1   |

S:

| A    | B    | C    |
| ---- | ---- | ---- |
| a1   | b2   | c2   |
| a1   | b3   | c2   |
| a2   | b2   | c1   |

## 并

union（∪）

R∪S={t|t∈R∨t∈S}

| A    | B    | C    |
| ---- | ---- | ---- |
| a1   | b1   | c1   |
| a1   | b2   | c2   |
| a2   | b2   | c1   |
| a1   | b3   | c2   |

## 差

except（-）

R-S={t|t∈R∧t!∈S}

| A    | B    | C    |
| ---- | ---- | ---- |
| a1   | b1   | c1   |

## 交

intersection（∩）

R∩S={t|t∈R∧t∈S}

| A    | B    | C    |
| ---- | ---- | ---- |
| a1   | b2   | c2   |
| a2   | b2   | c1   |

## 笛卡尔积

cartesian product（×）

![笛卡尔积公式](dikaer.png)

| R.A  | R.B  | R.C  | S.A  | S.B  | S.C  |
| ---- | ---- | ---- | ---- | ---- | ---- |
| a1   | b1   | c1   | a1   | b2   | c2   |
| a1   | b1   | c1   | a1   | b3   | c2   |
| a1   | b1   | c1   | a2   | b2   | c1   |
| a1   | b2   | c2   | a1   | b2   | c2   |
| a1   | b2   | c2   | a1   | b3   | c2   |
| a1   | b2   | c2   | a2   | b2   | c1   |
| a2   | b2   | c1   | a1   | b2   | c2   |
| a2   | b2   | c1   | a1   | b3   | c2   |
| a2   | b2   | c1   | a2   | b2   | c1   |

# 专门的关系运算

![学生-课程数据库](selectsql.png)

## 选择

selection，where，having（σ）

![选择公式](select.png)

涉及到的运算符

![条件表达式](yunsuanfu.png)

σsdept=‘IS’(Student)

| Sno       | Sname | Ssex | Sage | Sdept |
| --------- | ----- | ---- | ---- | ----- |
| 201215125 | 张立  | 男   | 19   | IS    |

σsage<20(Student)

| Sno       | Sname | Ssex | Sage | Sdept |
| --------- | ----- | ---- | ---- | ----- |
| 201215122 | 刘晨  | 女   | 19   | CS    |
| 201215123 | 王敏  | 女   | 18   | MA    |
| 201215125 | 张立  | 男   | 19   | IS    |

## 投影

projection（∏）

![投影公式](projection.png)

∏Sname·Sdept(Student)

| Sname | Sdept |
| ----- | ----- |
| 李勇  | CS    |
| 刘晨  | CS    |
| 王敏  | MA    |
| 张立  | IS    |

∏Sdept(Student)

| Sdept |
| ----- |
| CS    |
| MA    |
| IS    |

## 连接

join（⋈）

![连接公式](join.png)

<table>
    <tr>
        <td  colspan="3">R</td> 
        <td  colspan="2" >S</td> 
    </tr>
    <tr>
        <td >A</td>
        <td >B</td>
        <td >C</td>
        <td >B</td>
        <td >E</td>
    </tr>
    <tr>
        <td >a1</td>
        <td >b1</td>
        <td >5</td>
        <td >b1</td>
        <td >3</td>
    </tr>
    <tr>
        <td >a1</td>
        <td >b2</td>
        <td >6</td>
        <td >b2</td>
        <td >7</td>
    </tr>
    <tr>
        <td >a2</td>
        <td >b3</td>
        <td >8</td>
        <td >b3</td>
        <td >10</td>
    </tr>
    <tr>
        <td >a2</td>
        <td >b4</td>
        <td >12</td>
        <td >b3</td>
        <td >2</td>
    </tr>
    <tr>
        <td >\</td>
        <td >\</td>
        <td >\</td>
        <td >b5</td>
        <td >2</td>
    </tr>
</table>
### 非等值连接

不要求两列相同的值相同，看连接符下面的关系

![非等值连接公式](FEIDENGZHI.png)

| A    | R.B  | C    | S.B  | E    |
| ---- | ---- | ---- | ---- | ---- |
| a1   | b1   | 5    | b2   | 7    |
| a1   | b1   | 5    | b3   | 10   |
| a1   | b2   | 6    | b2   | 7    |
| a1   | b2   | 6    | b3   | 10   |
| a2   | b3   | 8    | b3   | 10   |

### 等值连接

当θ为=，是等值连接，根据某一共同列，两列相同的值连接

| A    | R.B  | C    | S.B  | E    |
| ---- | ---- | ---- | ---- | ---- |
| a1   | b1   | 5    | b1   | 3    |
| a1   | b2   | 6    | b2   | 7    |
| a2   | b3   | 8    | b3   | 10   |
| a2   | b3   | 8    | b3   | 2    |

### 自然连接

等值连接的基础上两列合并，是一种特殊的等值连接要求两个关系进行比较的分量必须是同名的属性组，并且在结果中把重复的属性列去掉。

| A    | B    | C    | E    |
| ---- | ---- | ---- | ---- |
| a1   | b1   | 5    | 3    |
| a1   | b2   | 6    | 7    |
| a2   | b3   | 8    | 10   |
| a2   | b3   | 8    | 2    |

R和S在做自然连接时，选择两个关系在公共属性上值相等的元组构成新的关系。此时，关系R中某些元组有可能在S中不存在公共属性上值相等的元组，从而造成了R中的这些元组被舍弃,S同理，这些被舍弃的元组称为悬浮元组。

### 外连接

把这些悬浮元组也保存在结果关系中，而在其他属性上填空值

| A    | B    | C    | E    |
| ---- | ---- | ---- | ---- |
| a1   | b1   | 5    | 3    |
| a1   | b2   | 6    | 7    |
| a2   | b3   | 8    | 10   |
| a2   | b3   | 8    | 2    |
| a2   | b4   | 12   | NULL |
| NULL | b5   | NULL | 2    |

### 左外连接

值保留⋈左边关系R中的悬浮元组

| A    | B    | C    | E    |
| ---- | ---- | ---- | ---- |
| a1   | b1   | 5    | 3    |
| a1   | b2   | 6    | 7    |
| a2   | b3   | 8    | 10   |
| a2   | b3   | 8    | 2    |
| a2   | b4   | 12   | NULL |

### 右外连接

值保留⋈右边关系R中的悬浮元组

| A    | B    | C    | E    |
| ---- | ---- | ---- | ---- |
| a1   | b1   | 5    | 3    |
| a1   | b2   | 6    | 7    |
| a2   | b3   | 8    | 10   |
| a2   | b3   | 8    | 2    |
| NULL | b5   | NULL | 2    |

## 除运算

division（÷）

![除运算公式](chu.png)

属于R但不属于S的字段，比较K中与S相同的字段中，包含S全部内容的那个。

如有A和B表

<table>
    <tr>
        <td  colspan="2">A</td> 
        <td >B</td> 
    </tr>
    <tr>
        <td >201215121</td>
        <td >1</td>
        <td >1</td>
    </tr>
    <tr>
        <td>201215121</td >  
        <td >2</td>
        <td >3</td>
    </tr>
    <tr>
        <td>201215121</td >
        <td >3</td>
        <td >\</td>
    </tr>
    <tr>
        <td>201215122</td >
        <td >2</td>
        <td >\</td>
    </tr>
    <tr>
        <td>201215122</td > 
        <td >3</td>
        <td >\</td>
    </tr>
</table>

A÷B：

只有201215121中同时含有B中的1和3，所以结果为{201215121}
