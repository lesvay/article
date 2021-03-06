---
title: 文件管理
date: 2020-03-16 11:14:55
categories: 
    - 操作系统
tags: 
    - fileManager
---

负责信息管理，有效支持文件存储、检索和修改，解决文件共享、保密和保护问题

功能：目录管理、文件操作管理、文件保护

# 文件的概念

具有文件名的一组相关元素集合，在文件系统中是一个最大的数据单位

| 组成   |                    |
| ------ | ------------------ |
| 数据项 | 描述某一属性的值   |
| 记录   | 属性               |
| 文件   | 一组相关信息的集合 |

属性：名称、标识符、文件类型、文件位置、文件大小、建立时间、用户标识。

## 文件分类

|                |                                          |
| -------------- | ---------------------------------------- |
| 按用途         | 系统文件、库文件、用户文件               |
| 按保护级别     | 只读文件、读写文件、执行文件、不保护文件 |
| 按信息流向分类 | 输入文件、输出文件、输入输出文件         |
| 按数据形式分类 | 源文件、目标文件(二进制文件)、可执行文件 |

## 基本操作

- 创建文件
- 删除文件
- 读文件
- 写文件
- 截断文件
- 设置文件的读写位置

## 文件打开关闭操作

- 打开文件
  - 文件指针
  - 文件打开计数（多个进程可能会同时打开文件）
  - 文件磁盘位置
  - 访问权限
- 关闭文件

## 文件的结构

### 文件的逻辑结构

无结构的流式文件

有结构的记录式文件

- 顺序文件
  - 最简单的一种结构
  - 按长度分：定长记录顺序文件、变长记录顺序文件
  - 按关键字分：串结构(与关键字顺序无关)、与关键字顺序有关
  - 优点：存取快，随机访问
  - 缺点：不会产生外部碎片
- 索引文件
  - 建立一个索引表
  - 优点：随机访问、易于开销
  - 缺点：效率低、空间开销大
- 索引顺序文件：为顺序结构分组，每组第一个建立索引表
- 直接文件、散列文件：关键字值决定物理地址

### 文件的物理结构

- 连续分配
- 链接分配
- 索引分配

## 目录的结构

### 功能

- 实现按名存取
- 提高检索速度
- 允许文件同名：通过不同工作目录加以区分
- 允许文件共享

### 文件控制块

- 文件名
- 文件的结构：逻辑结构是记录式（否定长、记录长度、个数）还是流式，物理结构是什么
- 文件的物理位置
- 存取控制信息：用户的权限
- 管理信息

### 索引节点

- 将文件名与文件描述信息分开
- 文件目录由文件名和指向具体文件的指针
- 磁盘索引节点：文件主标识符、文件类型、文件存取权限、文件物理地址、文件长度、文件连接计数、文件存取时间
- 内存索引节点：磁盘索引节点、索引节点编号、状态、访问计数、逻辑设备号、链接指针

### 单级目录结构

- 只建立一张用户表
- 不允许重名
- 查找效率慢

### 二级目录结构

- 主文件目录：系统中各个用户文件目录的情况
- 用户文件目录：每个用户单独一个目录

### 树形结构

- 第一级目录为根目录
- 非叶子节点为目录
- 叶子节点为文件
- 引入路径名\，当前目录..表示给的目录的父目录

### 图形结构

- 方便共享
- 每增加一个共享链时计数器+1，删除一个共享链计时器-1，当计数器为0时才删除文件

## 文件的共享

- 节省大量的外存空间和主存空间
- 共享动机
  - 相互协作共同完成任务
  - 远程计算机之间需要通信，需要远程文件系统的共享功能
- 共享方式
  - 基于索引节点的共享方式（硬链接）：不同目录的文件指针指向同一文件
  - 利用符号链实现文件共享（软连接）：只有所有者才有指针，其他用户只有路径名

## 文件的保护

- 访问类型（读写增加删除执行等）
- 访问控制：访问控制矩阵、访问控制表、用户权限表、密码与口令

# 文件系统的实现

## 层次结构

- 用户接口（cmd等）
- 文件目录系统
- 存取控制验证（权限）
- 逻辑文件系统与文件信息缓冲区（获取文件的逻辑地址）
- 物理文件系统（获取文件的物理地址）

## 目录的实现

- 线性表
- 散列表

## 文件的实现

外存分配方式

- 连续分配
- 链接分配
  - 隐式分配：指针放在每一个物理块中
  - 显示分配：指针放在内存的一张链接表中
- 索引分配
  - 单级索引分配
  - 两级索引分配
  - 混合索引分配：既采用直接地址，也使用单级或两级索引分配

- 文件存储空间管理
  - 空闲文件表
    - 将一个连续空闲区看作一个文件
    - 若请求等于块数则全部分配
    - 请求小于块数则部分留下
  - 空闲块链表：把所有空闲区域链起来，分配时一次从头开始
  - 位示图法：1表示已分配，0表示未分配，分配时按照需要找到一组值为0的二进制
  - 成组链接法：
    - 所有空闲区按每组100块分成若干组，所有盘号记录到前一组中，形成堆栈
    - 分配空闲盘块的方法
      - 先查找第一组的盘块数，
      - 若不止一块则将超级盘块中的空闲盘块数减一，将栈顶的盘块分配出去
      - 若只剩一块且盘块号不是标记结束的0，则将该块的内容读入超级块中，将该块分配出去
      - 若是0，则分配失败
    - 回收空闲盘块的方法
      - 若第一个不满100块，则只要在超级块的栈顶放入该空闲盘块的块号，并将磁盘块数+1
      - 若已经有100块了，则先将第一组的盘块数和盘块号写入该空闲磁盘块中，再将盘块数=1，栈顶块号=该空闲盘口块号写入超级块中，原来第一组变为第二组

# 磁盘组织与管理

## 物理结构

柱面号、磁头号、扇区号

## 信息

- 引导控制块（分区的第一块，没有操作系统则为空）
- 分区控制块（分区信息）
- 目录结构
- 文件控制块（文件信息）

## 访问时间

- 访问时间=寻道时间+旋转延迟+传输时间
- 寻道时间Ts=m*n+s(m:每移动一个磁道所需时间，s启动磁臂的时间、n移动几条磁道)
- 旋转延迟Tr=（1/r）/2（r旋转速度）
- 传输时间Tt=b/（rN）

## 调度算法

- 先来先服务算法FCFS：先来先服务
- 最短寻道时间优先算法SSTF：离磁头最近
- 扫描算法SCAN：
- 循环扫描算法C-SCAN：单向移动

## 磁盘管理

- 磁盘格式化：空白盘分区并写入基础信息
- 引导块：计算机启动时需要运行初始化程序（自举程序），找到系统内核装入内存，开始操作系统的运行
- 坏扇区
  - 简单磁盘（IDE）手工处理
  - 复杂磁盘（SCSI）维护一个磁盘坏块链表

# 参考文献

天勤操作系统