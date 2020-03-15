---
title: 计算机网络参考模型
date: 2020-03-15 10:41:22
categories: 
    - 计算机网络
tags: 
	- OSI
    - TCP/IP
	- 五层模型
---

将网络分层有利于让整个流程更加清晰，复杂的问题简单化。计算机网络参考模型常见的有三种：

![图片-三个参考模型](2020-03-15-networkReferenceModel\cankaomoxing.jpg)

[图片改编自百度文库](https://wenku.baidu.com/view/f7593b88974bcf84b9d528ea81c758f5f61f29f4.html)

# OSI七层参考模型

OSI（Open System Interconnect），即开放式系统互联。 一般都叫OSI参考模型，是ISO组织在1985年研究的网络互联模型。该体系结构标准定义了网络互联的七层框架（物理层、数据链路层、网络层、传输层、会话层、表示层和应用层），即OSI开放系统互连参考模型。

OSI 将计算机网络体系结构划分为七层，每层都可以提供抽象良好的接口，能够提供面向连接和无连接两种通信服务机制。是一种使各种不同的计算机和网络在世界范围内实现互联的标准框架。OSI 虽然层级多，由于功能细化，便于排障。不过由于种种原因，没有得以推行，只能作为一种适合学习的模型。

![图片-图解OSI](2020-03-15-networkReferenceModel\OSItujie.jpg)

[图片来自科来](http://www.colasoft.com.cn/download/document.php)

# TCP/IP四层参考模型

TCP/IP参考模型是计算机网络的祖父ARPANET和其后继的因特网使用的参考模型。ARPANET是由美国国防部DoD（U.S.Department of Defense）赞助的研究网络。逐渐地它通过租用的电话线连结了数百所大学和政府部门。当无线网络和卫星出现以后，现有的协议在和它们相连的时候出现了问题，所以需要一种新的参考体系结构。

这个体系结构在它的两个主要协议出现以后，即先有的TCP和IP协议，后有的模型，被称为TCP/IP参考模型（TCP/IP reference model）。基于TCP/IP的参考模型将协议分成四个层次，它们分别是：网络访问层、网际互联层（主机到主机）、传输层、和应用层，能够提供面向连接和无连接两种通信服务机制。由于出现的早，更为众人所采用，是偏向于实践的模型。



# 教学五层模型

为了便于学习，便出现了TCP/IP模型分化出来的模型，即教学五层模型。这个模型在工业界是没有的，主要是方便教学使用。

| 名称       | 对象                   | 单位                                 | 功能                                                         | 协议                                    |
| ---------- | ---------------------- | ------------------------------------ | ------------------------------------------------------------ | --------------------------------------- |
| 应用层     | 用户对用户             |                                      | 文件传输、访问和管理、电子邮件服务                           | FTP 、SMTP、POP3、HTTP、DNS、TFTP、SNMP |
| 传输层     | 应用对应用、进程对进程 | (segments段)报文段TCP、用户数据报UDP | 为端到端连接提供可靠的传输服务，为端到端连接提供流量控制、差错控制、服务质量等管理服务，提供应用进程间的逻辑通信，差错检测，提供无连接和面向连接的服务，复用和分用，TCP:连接管理 流量控制与拥塞控制 | TCP、UDP                                |
| 网络层     | 主机对主机             | Packets包：数据报                    | 组包和拆包、路由选择、分组转发、拥塞控制、异构网络互连       | ICMP、ARP、RARP、IP、IGMP               |
| 数据链路层 |                        | Frames帧                             | 链路管理、帧定界和帧同步、差错检测、透明传输                 | PHP、HDLC                               |
| 物理层     |                        | Bits比特                             | 提供传输数据的通路                                           |                                         |

以前学习的时候参考天勤做了一个思维大纲图，欢迎来看，[计算机网络](https://mubu.com/doc/5PAGbmxGYrg)

# 数据封装拆解过程

从应用层的数据到物理层的比特率，每向下一层数据都会被进一步封装，就像洋葱一样，只有它的芯才是真正的要表达的数据，那一层一层的是传输时的信息，比如下一步要传递给谁？它的地址是多少？

![图片-数据封装](2020-03-15-networkReferenceModel\fengzhuang.png)

[图片改编自百度文库](https://wenku.baidu.com/view/f7593b88974bcf84b9d528ea81c758f5f61f29f4.html)

现实生活中，我们不可能一根网线就可把数据发送给对方，中间要经过多个路由器、交换机。

![图片-数据流动过程](2020-03-15-networkReferenceModel\liudongguocheng.png)

[图片改编自百度文库](https://wenku.baidu.com/view/f7593b88974bcf84b9d528ea81c758f5f61f29f4.html)

每次需要经过交换机时MAC头部就会被拆解，并被更换为新的MAC头部。每次需要经过路由器时，MAC头部被拆解并向上提交至网络层，IP头部也会被拆解并更换为新的IP头部，然后向下提交加上新的MAC头部。以此类推，最后到达了目标主机。再逐层拆解最后洋葱被拨的只剩芯了，这也是我们真正想要发送的数据。

![图片-数据解封过程](2020-03-15-networkReferenceModel\jiefeng.png)

[图片改编自百度文库](https://wenku.baidu.com/view/f7593b88974bcf84b9d528ea81c758f5f61f29f4.html)

最后这是一张表述每一层所对应物理设备，当然这并不是绝对的，因为现实生活中也会有网络层交换机。

![图片-对应设备](2020-03-15-networkReferenceModel\shebei.png)

[图片改编自百度文库](https://wenku.baidu.com/view/f7593b88974bcf84b9d528ea81c758f5f61f29f4.html)

# 参考文献

[百度文库-01-计算机网络参考模型](https://wenku.baidu.com/view/f7593b88974bcf84b9d528ea81c758f5f61f29f4.html)

[百度百科-OSI参考模型]([https://baike.baidu.com/item/OSI%E5%8F%82%E8%80%83%E6%A8%A1%E5%9E%8B](https://baike.baidu.com/item/OSI参考模型))

[简书-计算机网络-参考模型](https://www.jianshu.com/p/348df1dde9bd)

[百度知道](https://zhidao.baidu.com/question/573470632.html)

[百度百科-TCP/IP参考模型]([https://baike.baidu.com/item/TCP%2FIP%E5%8F%82%E8%80%83%E6%A8%A1%E5%9E%8B](https://baike.baidu.com/item/TCP%2FIP参考模型))

[博客园-努力改个网名](https://www.cnblogs.com/lsdb/p/9564094.html)

[天勤计算机网络]()

