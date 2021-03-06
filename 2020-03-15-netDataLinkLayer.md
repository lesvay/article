---
title: 数据链路层相关知识点
date: 2020-03-15 14:59:09
categories: 
    - 计算机网络
tags: 
    - dataLinkLayer

---

# 概述

- 单位：Frames帧
- 硬件：交换机、网桥
- 任务：将网络层传下来的数据报封装成帧
- 协议：PHP、HDLC
- 功能

| 功能           | 描述                                             |
| -------------- | ------------------------------------------------ |
| 链路管理       | 链路连接的建立、拆除、分离                       |
| 帧定界和帧同步 | 接收方确定收到的比特流中一帧的开始位置与结束位置 |
| 差错检测       | 使接收方确定收到的数据就是发送方发送的数据       |
| 透明传输       | 不管什么样的比特组合都应当在链路中传送           |

# 组帧

| 方法                 | 描述                                                         |
| -------------------- | ------------------------------------------------------------ |
| 字符计数法           | 用一个字符表示帧的开始，一个计数字段表示该帧包含的字节数，从而推断出帧的结束位和下一个帧开始位 |
| 字节填充的首尾界符法 | 从128个ASCII码中的33个键盘不能输入的字符中挑出两个作为起始和结束标志。当传输文件不是键盘输入的,文件中会出现起始和结束标志,因此使用字节填充的首尾界符法，SOH-->ESCx,EOT-->ESCy,ESC-->ESCz |
| 比特填充的首尾标志法 | 首尾标志为01111110 文件中每连续5个1,则后面加入1个0           |
| 物理编码违例法       | 利用物理介质上编码违法方式来区分开始和结束                   |

# 差错检测

## 检错编码

- 奇偶校验码

  - 奇校验码:添加一位校验码,使得整个码字里面的1个数是奇数
  - 偶校验码:添加一位校验码,使得整个码字里面的1个数是偶数

- 循环冗余码CRC

  ![图片-CRC计算过程](crc.jpg)


## 纠错编码

海明码（Hamming Code）是一个可以有多个校验位，具有检测并纠正一位错误代码的纠错码，所以它也仅用于信道特性比较好的环境中，如以太局域网中，因为如果信道特性不好的情况下，出现的错误通常不是一位。
海明码的基本思想是将有效信息按某种规律分成若干组，每组安排一个校验位进行奇偶性测试，然后产生多位检测信息，并从中得出具体的出错位置，最后通过对错误位取反来将其纠正。
要采用海明码纠错，需要按以下步骤来进行：计算校验位数→确定校验码位置→确定校验码→实现校验和纠错。

# 传输机制

## 流量控制

| 流量控制          | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| 停止-等待流量控制 | 发送方发送一个帧,得到应答后再发送下一个帧,否则一直等待       |
| 滑动窗口流量控制  | 允许发送多个帧,得到一个应答窗口向前滑动一个帧。当窗口满了,发送方会强行关闭网络层,直到有一个空闲缓冲区出来 |

## 可靠传输机制

利用传输层TCP

## 滑动窗口机制

| 协议             | 窗口状态              | 描述                                                         |
| ---------------- | --------------------- | ------------------------------------------------------------ |
| 停止-等待协议    | 发送窗口=1,接收窗口=1 | 可靠传输（确认：发送确认帧超时，重传：一段时间没有响应就会重新发送）；数据帧破坏（如果帧正确则接收，不正确则丢弃，发送方未收到确认帧等待一段时间后再次发送）；确认帧被破坏（发送方在帧中加入标识，接收方判断是新帧还是旧帧） |
| 后退N帧协议(GBN) | 发送窗口>1,接收窗口=1 | 滑动窗口中，某帧出错，则其及后续帧丢弃，发送方重传           |
| 选择重传协议(SR) | 发送窗口>1,接收窗口>1 | 某帧出错，其后续帧存入接收方缓存中，发送方重发出错帧         |

# 介质访问控制

介质访问控制(medium access control)简称MAC。 是解决当局域网中共用信道的使用产生竞争时，如何分配信道的使用权问题。

## 信道划分介质访问控制

- 频分多路复用：道路变宽
- 时分多路复用：时间分割
- 波分多路复用：波段分割
- 码分多路复用：碎片数据✖码片向量，-1表示比特0，1表示比特1，0表示没有数据

## 随机访问介质访问控制

- 随机接入(争用型)

  | 方法    | 描述                                                         |
  | ------- | ------------------------------------------------------------ |
  | ALOHA   | 不经过任何检测就发送数据，没有收到确认则继续发送             |
  | CSMA    | 1-坚持CSMA：发送节点监听到空闲时，立即发送数据，否则继续监听；p-坚持CSMA：发送节点监听到空闲时，依概率p发送数据，以概率（1-p）延迟一段时间并重新监听；非坚持CSMA：发送节点一旦监听到空闲时，就立即发送数据，否则延迟一段时间重新监听。 |
  | CSMA/CD | 过程：发送数据之前检测总线是否有其他计算机发送数据，若无则发送数据，发送时继续监听，若出现冲突则随机时间后继续发送，适合有线网络，是被动型。 |
  | CSMA/CA | 过程：发送数据之前检测总线是否有其他计算机发送数据，若无则发送数据，一段时间后检查对方是否发回帧确认，若没有继续重发，适合无线型网络，是主动型。 |

- 受控接入：不能随便发送某数据，得到某种东西才能发送

## 轮询访问介质访问控制

- 过程：用户不能随机发送数据，通过一个集中控制的监控站经过轮询过程后再决定信道的分配
- 令牌环局域网
- 令牌传递协议

# 网络

## 局域网

### 以太网

工作原理：采用总线拓扑结构，无连接工作方式，不对发送的数据进行编号，也不要求对方发送确认。

MAC帧如下：

![图片-MAC帧](maczhen.jpg)

- 前导码：前同步符、帧开始定界符

- 目的地址、源地址：目的地址前八位最后一位为0，发给某一工作站；最后一位为1，其余不全为1，发给一组工作站；全为1，广播地址，发给所有工作站。


传输介质，其中10指10Mbit/s，base基带信号

![图片-各种以太网](10base.jpg)

高速以太网：100Base-T以太网、吉比特以太网、10吉比特以太网

无线局域网

- 有固定基础设施的无线局域网（BSS基站）
- 无固定基础设施的无线局域网（自主网络）

IEEE802.11

- 物理层：跳频扩频（FHSS）、直接序列扩频（DSS）、红外线（IR）
- MAC层：分布协调功能（DCF）、点协调功能（PCF）、CSMA/CD、确认机制

### 令牌环网

- 当网络空闲时，环路中只有令牌在网络中循环传递
- 令牌传递到数据要发送的节点，修改令牌标志位，附加要传输的数据
- 数据延环路继续传输，直到遇到接收节点
- 接收节点复制数据，令牌继续传，传回发送节点
- 发送节点检查数据是否出错，出错重传，没有就产生一个新令牌，继续在令牌环上游荡

## 广域网

### PPP

是面向字节的协议，只负责检错、是不可靠传输、点对点通讯、全双工链路。

过程：用户拨号接入ISP，调制解调器对拨号做出确认，并建立一条物理连接，计算机向路由器发送一系列LCP分组，网络控制协议NCP给个人计算机分配一个临时IP，接入网络成功。

![图片-PPP](ppp.jpg)

### HDLC协议

是面向比特的协议

基本配置

- 非平衡配置：由一个主机控制整个链路
- 平衡配置：链路两端的两个站是复合站，每个复合站可以平等的发起数据，不需要得到对方复合站的允许

![图片-HDCL](HDCL.jpg)

# 物理设备

## 网桥

网桥至少有两个端口，每个端口与一个网段相连，接收到数据存储到缓存中，若为出错，则查找转发表从别的端口转发出去
- 优点：过滤通信量、扩大物理范围、提高可靠性、可连接至不同物理层、不同MAC层和不同速率的以太网上
- 缺点：存储转发增加了时延、在MAC子层并没有流量控制功能、具有不同MAC子层的网段桥接在一起时时延更大、适合用户数量不多，通信量小的局域网

| 分类       | 解释                                                         |
| ---------- | ------------------------------------------------------------ |
| 透明网桥   | 指不知道要经过哪几个网桥，自主学习转发表，新增或更新（源地址、进入的接口和时间） |
| 源选径网桥 | 对外广播，选择最佳路由                                       |

## 交换机

- 实质：多端口网桥
- 直通式交换：只检查帧的目的地址，收到后立马被转发出去
- 存储转发式交换：先存储在高速缓存中，检查数据是否正确，查找转发表，转发

## 网桥与交换机对比

- 网桥有两个端口，交换机多个
- 网桥连接到局域网网段，交换机连接主机或HUB
- 网桥一对计算机同时通讯，交换机允许多对
- 网桥存储转发，以太网有直通转发和存储转发

## 冲突域与广播域总结

![图片-冲突域与广播域](chongtu.jpg)

# 参考文献 

天勤计算机网络