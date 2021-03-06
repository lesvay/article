---
title: 数据库相关概念
date: 2020-05-06 11:44:39
categories: 
    - 数据库
tags: 
    - 数据库概念
---

# 数据库系统

![发展阶段](fazhan.png)

## 组成

数据库系统是由数据库、数据库管理系统、应用程序和数据库管理员DBA组成的存储、管理、处理和维护数据的系统。

![组成](zucheng.png)

### 数据

数据库中存储的基本对象，是描述事物的符号记录

### 数据库

存放数据的仓库，是长期存储在计算机内、有组织的、可共享的大量数据的集合。数据库中的数据按一定的数据模型组织、描述和存储，具有较小的冗余度、较高的数据独立性和易扩展性，并可为各种用户共享。具有永久存储、有组织和可共享三个基本特点。

### 数据库管理系统

同操作系统一样是计算机的基础软件

- 数据定义功能：提供数据定义语言DDL，用户通过它可以很方便地对数据库中的数据对象的组成与结构进行定义。
- 数据组织、存储和管理：数据库管理系统要分类组织、存储和管理各种数据，包括数据字典、用户数据、数据的存取路径。确定以何种文件结构和存取方式在存储级上组织这些数据，如何实现数据之间的联系。其目标是提高存储空间利用率和方便存取，提供多种存取方法来提高存取效率。
- 数据操纵功能：数据库管理系统还提供数据操纵语言DML，用户可以使用它操纵数据，实现对数据库的基本操作，如查询、插入、删除、修改。
- 数据库的事物管理和运行管理：数据库在建立、运行和维护时由数据库管理系统统一管理和控制，以保证事物的正确运行，保证数据的安全性、完整性、多用户对数据的并发使用及发生故障后的系统恢复。
- 数据库的建立和维护功能：包括数据库初始数据的输入、转换功能，数据库的转储、恢复功能，数据库的重组织功能和性能监视、分析功能等。这些功能通常是由一些实用程序或管理工具完成的。
- 其他功能：数据库管理系统与网络中其他软件的通信功能、与另一个数据库管理系统文件系统的数据转换功能、异构数据库之间的互访和互操作功能。

## 特点

- 结构化：不仅数据内部是结构化的，而且整体也是结构化的。比如一个学校的各类组织的集合，而非其中一个。
- 数据的共享性高、冗余度低且以扩充
- 数据独立性高
  - 物理独立性：用户的应用程序与数据库中数据的物理存储是相互独立的
  - 逻辑独立性：用户的应用程序与数据库的逻辑结构是相互独立的
- 数据由数据库管理系统统一管理和控制
  - 数据的安全性保护：放止不合法使用造成的数据泄密和破坏
  - 数据的完整性检查：正确性、有效性和相容性
  - 并发控制：对多用户并发操作加以控制和协调
  - 数据库恢复：将数据库从错误状态恢复到某一已知的正确状态

## 构造

### 硬件平台及数据库

- 足够大的内存
- 足够大的磁盘
- 通道能力

### 软件

- 数据库管理系统
- 支持数据库管理系统运行的操作系统
- 具有与数据库接口的高级语言及其编译系统
- 以数据库管理系统为核心的应用开发工具
- 为特定应用环境开发的数据库应用系统

### 人员

- 数据库管理员
  - 决定数据库中的信息内容和结构
  - 决定数据库的存储结构和存取策略
  - 定义数据的安全性要求和完整性约束条件
  - 监控数据库的使用和运行
  - 数据库的改进和重组、重构
- 系统分析员和数据库设计人员
- 应用程序员：负责设计和编写应用系统的程序模块
- 用户
  - 偶然用户：不经常访问，但每次访问需要不同信息
  - 简单用户：主要是查询和更新，机票预定工作人员
  - 复杂用户：工程师、科学家等

## 模式

### 模式的概念

- 模式是指数据库中全体数据的逻辑结构和特征的描述
- 模式是相对稳定的，而实例是相对变动的

### 三级模式

- 外模式：子模式或用户模式，它是数据库用户能够看见和使用的局部数据的逻辑结构和特征的描述，是数据库用户的数据视图，是与某一应用有关的数据的逻辑表示。
- 模式：逻辑模式，是数据库中全体数据的逻辑结构和特征的描述，是所有用户的公共数据视图。
- 内模式：存储模式，一个数据库只有一个内模式，是数据物理结构和存储方式的描述，是数据在数据库内部的组织方式。

### 二级映像

- 外模式\模式映像：当模式改变时，管理员对外模式\模式映像做出相应改变，使外模式保持不变。
- 模式\内模式映像：当存储结构即内模式改变时，管理员对模式\内模式映像做出相应改变，使模式保持不变。

## 模型

数据库是一种模型，是对现实世界数据特征的抽象

### 概念模型

- 信息模型，按照用户的观点对数据和信息进行建模，主要用于数据库的设计
- 实体：客观存在并可相互区别的事物
- 属性：实体所具有的某一特性成为属性
- 码：唯一标识实体的属性集称为码
- 实体型：用实体名及其属性名集合来抽象和刻画同类实体
- 实体集：同一类型实体的集合
- 联系
  - 一对一：对于实体集A中的每一个实体，实体集B中至多只有一个与之对应，反之亦然。
  - 一对多：对于实体集A中的每一个实体，实体集B中有n个实体与之联系，反正对于B，A至多只有一个实体与之联系
  - 多对多：对于实体集A中的每一个实体，B中有n个与之联系，反之对于B，A中有m个与之联系
- 另一种表示方法：实体-联系方法，即E-R方法

### 逻辑模型

主要用于数据库管理系统的实现。

#### 层次模型

- 有且只有一个结点没有双亲结点，这个结点称为根结点
- 根以外的其他结点有且只有一个双亲结点
- 只能处理一对多的实体联系
- 优点
  - 数据结构比较简单清晰
  - 层次数据库的查询效率高
- 缺点
  - 不适用于现实中的其他联系
  - 当一个结点具有多个双亲时，该模型很笨拙
  - 查询子女结点必须通过双亲结点
  - 结构严密，层次命令趋于程序化

#### 网状模型

- 允许一个以上的结点无双亲
- 一个结点可以有多于一个的双亲
- 优点
  - 更为直接的描述现实世界
  - 具有良好的性能，存取效率较高
- 缺点
  - 结构比较复杂
  - 需要嵌入某一高级语言中，用户不易掌握
  - 用户必须先了解系统结构细节，选取适合的存取路径，加重编写负担

#### 关系模型

- 关系：一个关系对应通常说的一张表
- 元组：表中的一行即为一个元组
- 属性：表中的一列即为一个属性
- 码：码键
- 域：一组具有相同数据类型的值的集合
- 分量：元组中的一个属性值
- 关系模式：对关系的描述
- 关系模型要求关系必须是规范化的，每一个分量必须是一个不可分的数据项
- 用户只需要指出干什么找什么，不必详细说明怎么干怎么找
- 优点
  - 建立在严格的数学概念的基础上
  - 概念单一、结构简单清晰、易懂
  - 存取路径对用户透明
- 缺点
  - 由于存取路径透明，查询效率低于格式化数据模型
- 关系操作
  - 查询：选择、投影、并、差、笛卡尔积
  - 插入、删除、修改：基本操作
- 关系数据语言
  - 关系代数语言ISBL
  - 关系演算语言
    - 元组关系演算语言ALPHA\QUEL
    - 域关系演算语言QBE
  - 具有关系代数和关系演算双重特点的语言SQL
- 关系完整性
  - 域完整性：指数据库数据取值的正确性，它包括数据类型、精度、取值范围以及是否允许空值等
  - 实体完整性：是指关系的主关键字不能重复也不能取“空值"
  - 参照完整性：定义建立关系之间联系的主关键字与外部关键字引用的约束条件
  - 用户定义的完整性：是根据应用环境的要求和实际的需要，对某一具体应用所涉及的数据提出约束性条件

#### 面向对象数据模型

#### 对象关系数据模型

#### 半结构化数据模型

### 物理模型

对数据最底层的抽象，描述数据在系统内部的表示方式和存取方法

## 组成要素

- 数据结构：描述数据组成对象以及对象之间的联系。如层次结构、网状结构和关系结构
- 数据操作：指对数据库中各种对象的实例允许执行的操作的集合，包括操作及有关的操作规则。如增删改
- 数据的完整性的约束条件：是一组完整性规则
- 数据的完整性约束条件

## 基本层联系

是指两个记录以及它们之间一对多（一对一）的联系

# 数据库安全性

## 安全性概述

### 不安全因素

- 非授权用户对数据库的恶意存取和破坏
- 数据库中重要或敏感的数据被泄露
- 安全环境的脆弱性

### 安全级别

![img](https://img.mubu.com/document_image/682e82e7-6045-4568-bb4f-f4515f232a6e-5292384.jpg)

## 安全性控制

### 身份鉴别

- 静态口令鉴别
- 动态口令鉴别
- 生物特征鉴别
- 智能卡鉴别

### 存取控制

机制：定义用户权限、合法权限检查

方法

#### 自主存取控制

- 用户权限：数据库对象和操作类型

- 定义存取权限称为授权

- 存取控制对象不仅有数据本身，还有数据库模式

  ![img](https://img.mubu.com/document_image/85040007-3109-43aa-a5e9-8f993d772dbd-5292384.jpg)

#### 强制存取控制

- 系统为保证更高程度的安全性，适用于对数据有严格而固定密集分类的部门
- 主体、客体：按照敏感度标记来区分主体是否可以操纵客体
  - 绝密
  - 机密
  - 可信
  - 公开
  - 主体大于等于客体密级时才能读
  - 主体小于等于客体密级时才能写

### 授予与收回

- GRANT向用户授权

- REVOKE收回已经授予用户的权限

- 权限与角色

  ![img](https://img.mubu.com/document_image/2c6c66e8-b680-4767-8eed-fee53c4f4a9f-5292384.jpg)

  - 角色的创建CREATE ROLE<角色名>
  - 角色的授权GRANT<权限>ON<对象类型>对象名TO<角色>
  - 用户的角色分配GRANT<角色>TO<角色>
  - 角色权限的回收REVOKE<权限>ON<对象类型>FROM<角色>

### 视图机制

为不同的用户定义不同的视图

### 审计

- 把用户的所有操作记录到日志中
- 审计事件
  - 服务器事件
  - 系统权限
  - 语句事件
  - 模式对象事件
- 审计功能
  - 基本功能，提供多种审计查阅方式
  - 提供多套审计规则
  - 提供审计分析和报表功能
  - 审计日志管理功能
  - 系统提供查询审计设置及审计记录信息的专门视图
  - AUDIT设置审计功能
  - NO AUDIT取消审计功能

### 数据加密

- 存储加密

  - 透明加密方式：数据在写到磁盘时对数据进行加密，内核级加密方式，对用户完全透明
  - 非透明加密方式：通过多个加密函数实现

- 传输加密

  - 链路加密

  - 端到端加密

    - 基于安全套接层协议可信加密传输方案

      ![img](https://img.mubu.com/document_image/1ff5e808-b97d-4bef-921c-74f510aea6ea-5292384.jpg)

### 其他安全性保护

- 推理控制：避免用户利用能够访问的数据库推理更高级的数据
- 隐蔽信道：避免高安全等级用户按事先约定方式主动向低安全等级用户传输信息
- 数据隐私：控制不愿被他人知道或他人不便知道的个人数据的能力

# 数据库完整性

## 定义

- 正确性：数据符合现实世界语义、反应当前实际状况的
- 相容性：数据库同一对象在不同关系表中的数据是符合逻辑的

## 完整性模型

### 实体完整性

- 主码值是否唯一，不唯一则拒绝插入或修改
- 主码各个属性是否为空，只要有一个为空就拒绝插入或修改

### 参照完整性

- 当两个表中相应元组联系起来可能会破坏参照完整性，必须进行检查
- 拒绝执行：一般设为默认策略
- 级联操作：当删除或修改被参照表的一个元组导致与参照表不一致时，删除或修改参照表中的所有导致不一致的元组
- 设置为空值：当删除或修改被参照表的一个元组导致不一致时，将参照表中的所有导致不一致的元组设置为空值

### 用户定义的完整性

- 属性上的约束条件
  - 不允许取空值
  - 列值为一
  - CHECK短语指定列值应满足的条件
- 元组上的约束条件：拒绝操作

## 完整性约束命名子句

- 完整性约束条件包括：NOT NULL\UNIQUE\PRIMARY KEY\FOREIGN KEY\CHECK
- 修改完整性限制：ALTER TABLE

## 断言

- 通过断言来指定更具体更一般性的约束
- 创建断言：CREATE ASSERTION<断言句><CHECK子句>
- 删除断言：DROP ASSERTION<断言句>

## 触发器

- 是用户定义在关系表上的一类由事件驱动的特殊过程。又叫做事件-条件-动作规则
- 语法规则
  - 只有表的拥有者才可以在表上创建触发器，并且一个表上只能创建一定数量的触发器
  - 触发器名：同一模式下触发器名必须是唯一的，并且触发器名和表名必须在同一模式下
  - 表名：触发器只能定义在基本表上，不能定义在视图上
  - 触发事件：触发事件可以是INSERT\DELETE\UPDATE
  - 触发器类型：触发器按照所触发动作的间隔尺寸可以分为行级触发器和语句级触发器
  - 触发条件：触发条件为真时触发动作体才执行
  - 触发动作体：可以是一个匿名PL/SQL过程块，也可以是对已创建存储过程的调用。如果执行失败，激活触发器的事件就会终止执行，触发器的目标表或触发器可能影响的其他对象不发生任何变化
- 激活触发器
  - 执行该表上的BEFORE触发器，存在多个时遵循谁先创建谁先执行的原则
  - 激活触发器的SQL语句
  - 执行该表上的AFTER触发器
- 删除触发器：DROP TRIGGER<触发器名>ON<表名>。只能是一个已经创建的触发器，并且具有相应权限的用户删除。