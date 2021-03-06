---
title: 计算机网络基本概念
date: 2020-03-15 14:57:58
categories: 
    - 计算机网络
tags: 
    - conception
---

# 定义

一些互联自治的计算机系统的集合

# 组成

## 物理组成

### 硬件
  - 主机
  - 通讯处理机（前端处理器）
  - 通讯线路
    - 有线
    - 无线
  - 交换设备
    - 交换机
    - 路由器
    - etc

### 软件
实现资源共享的软件和工具，如：QQ

### 协议
一种规则

## 工作方式组成

### 边缘部分
  - 组成：所有连接在互联网上供用户直接使用的主机
  - 作用：通信、资源共享

### 核心部分
  - 组成大量的网络和连接这些网络的路由器
  - 作用：提供连通性和交换服务

## 功能组成

### 通讯子网
  - 组成：传输介质、通信设备、响应的网络协议
  - 作用：提供数据传输、交换和控制能力，实现信息通讯

### 资源子网
  - 组成：主机、终端、各类软件资源和信息资源
  - 作用：负责全网的数据处理业务，像网络用户提供各种网络资源与服务

# 功能

- 数据通信（最基本，最重要）
- 资源共享
- 分布式处理
- 信息综合处理
- 负载均衡
- 提高可靠性

# 分类

## 分布范围

- 广域网
- 城域网
- 局域网
- 个人区域网

##  拓扑结构

- 星形网络

- 总线型网络

- 环形网络

- 网状形网络

## 传输技术

- 广播式网络
- 点对点网络

## 使用者
  - 公用网
  - 专用网

## 数据交换技术
  - 电路交换网
  - 报文交换网
  - 分组交换网

# 相关组织

- ISO国际标准化组织
- ITU国际电信联盟
- IEEE美国电气和电子工程师协会

# 参考模型

## ISO/OSI

- 应用层
- 表示层
- 会话层
- 传输层
- 网络层
- 数据链路层
- 物理层

## TCP/IP

- 应用层
- 传输层
- 互联网层
- 网络接收层

## 5层模型

- 应用层
- 传输层
- 网络层
- 数据链路层
- 物理层

# 性能指标

## 时延（总时延为四者之和）

- 发送时延（传输时延）
  - 主机或路由器发送数据所需要的时间，从第一位开始发送到最后一位发送完毕
  - 发送时延=数据帧长度（bit）/发送速率（bit/s）
- 传播时延
  - 电磁波在信道中传播一定的距离所需要的时间
  - 传播时延=信道长度（m）/电磁波在信道上的传播速度（m/s）
- 处理时延
  - 主机在路由器在接收到分组时进行处理所需要的时间
- 排队时延
  - 进入路由器在输入队列排队等待处理
  - 确定转发接口后，在输出队列等待转发

## 时延带宽积

- 时延带宽积=传播时延*带宽

## 往返时间

- 从发送方开始发送数据，到发送方收到接收方的确认消息

## 利用率
  - 信道利用率
    - 某信道有%的时间是被利用的
  - 网络利用率
    - 全网络信道利用率加权平均值

# 参考文献

天勤计算网络

