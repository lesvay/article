---
title: DNS域名解析过程
date: 2020-03-14 18:58:00
categories: 
    - 计算机网络
tags: 
	- dns
---

DNS域名解析过程大致分为两种：

# 迭代查询

所谓迭代查询是指：根域名服务器收到查询请求，要么给出查询结果，要么告诉本地域名服务器下一步向哪个域名服务器进行查询。

主要是本地域名服务器向根域名服务器查询信息时所采用的方式。

# 递归查询

所谓递归查询是指：本地域名服务器只请求一次，后面几次都是在其他几个域名服务器之间进行的。

主要是主机向本地域名服务器查询信息时所采用的方式。当主机需要查询IP时，本地域名服务器不知道域名所对应的IP地址，那么本地域名服务器就以DNS客户的身份，向其他根域名服务器发送查询请求报文，而不是让主机自己进行下一步查询。

# 访问度娘的过程

	①本机向local dns请求www.baidu.com
	②local dns向根域请求www.baidu.com，根域返回com.域的服务器IP
	③向com.域请求www.baidu.com，com.域返回baidu.com域的服务器IP
	④向baidu.com请求www.baidu.com，返回cname www.a.shifen.com和a.shifen.com域的服务器IP
	⑤向root域请求www.a.shifen.com
	⑥向com.域请求www.a.shife.com
	⑦向shifen.com请求
	⑧向a.shifen.com域请求
	⑨拿到www.a.shifen.com的IP
	⑩localdns返回本机www.baidu.com cname www.a.shifen.com 以及 www.a.shifen.com的IP

# 参考文献

[CSDN-Crazw_jia](https://blog.csdn.net/crazw/article/details/8986504)

[CSDN-Daputao_net](https://blog.csdn.net/Daputao_net/article/details/81203531)

[博客园-皈依之路](https://www.cnblogs.com/qingdaofu/p/7399670.html)