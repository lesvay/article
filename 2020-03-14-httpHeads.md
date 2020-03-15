---
title: HTTP的头信息
date: 2020-03-14 18:50:24
categories: 
    - 计算机网络
tags: 
    - http
---

HTTP头信息主要包括通用头、请求头、响应头、实体头。

![qingqiutou](qingqiutou.png)
![xiangyingtou](xiangyingtou.png)

# 通用头部

通用头域包含请求和响应消息都支持的头域，通用头域包含缓存头部Cache-Control、Pragma及信息性头部Connection、Date、Transfer-Encoding、Update、Via。

| 应答头            | 说明                                                     |
| :---------------- | :------------------------------------------------------- |
| Cache-Control     | 指定请求和响应遵循的缓存机制                             |
| Pragma            | 用来包含实现特定的指令                                   |
| Connection        | 表示是否需要持久连接                                     |
| Date              | 指定请求和响应遵循的缓存机制                             |
| Cache-Control     | 表示消息发送的时间                                       |
| Transfer-Encoding | 服务器表明自己对本响应消息体作了怎样的编码               |
| Upgrade           | 指定另一种可能完全不同的协议                             |
| Via               | 列出该响应经过了哪些代理服务器，他们用什么协议发送的请求 |

# 请求头部

请求头用于说明是谁或什么在发送请求、请求源于何处，或者客户端的喜好及能力。服务器可以根据请求头部给出的客户端信息，试着为客户端提供更好的响应。请求头域可能包含下列字段Accept、Accept-Charset、Accept- Encoding、Accept-Language、Authorization、From、Host、If-Modified-Since、If-Match、If-None-Match、If-Range、If-Range、If-Unmodified-Since、Max-Forwards、Proxy-Authorization、Range、Referer、User-Agent。对请求头域的扩展要求通讯双方都支持，如果存在不支持的请求头域，一般将会作为实体头域处理。

| 应答头              | 说明                                                         |
| :------------------ | :----------------------------------------------------------- |
| Accept              | 告诉WEB服务器自己接受什么介质类型                            |
| Accept-Charset      | 浏览器告诉服务器自己能接收的字符集                           |
| Accept-Encoding     | 浏览器申明自己接收的编码方法                                 |
| Accept-Language     | 浏览器申明自己接收的语言                                     |
| Authorization       | 客户端接收到服务器的WWW-Authenticate响应时，用该头部来回应服务器自己的身份验证信息 |
| If-Match            | 如果对象的ETag没有改变，即对象没有改变，才执行请求的动作     |
| If-None-Match       | 如果对象的ETag改变了，才执行请求的动作                       |
| If-Modified-Since   | 如果请求的对象在该头部指定的时间之后修改了，才执行请求的动作，否则返回代码304，告诉浏览器该对象没有修改 |
| If-Unmodified-Since | 如果请求的对象在该头部指定的时间之后没修改过，才执行请求的动作 |
| If-Range            | 浏览器告诉 WEB 服务器，如果我请求的对象没有改变，就把我缺少的部分给我，如果对象改变了，就把整个对象给我 |
| Range               | 浏览器告诉 WEB 服务器自己想取对象的哪部分                    |
| Proxy-Authenticate  | 代理服务器响应浏览器，要求其提供代理身份验证信息             |
| Host                | 客户端指定自己想访问的WEB服务器的域名/IP 地址和端口号        |
| Referer             | 浏览器向WEB 服务器表明自己是从哪个网页URL获得点击当前请求中的网址/URL |
| User-Agent          | 浏览器表明自己的身份                                         |

# 响应头部

响应头向客户端提供一些额外信息，比如谁在发送响应、响应者的功能，甚至与响应相关的一些特殊指令。这些头部有助于客户端处理响应，并在将来发起更好的请求。响应头域包含Age、Location、Proxy-Authenticate、Public、Retry- After、Server、Vary、Warning、WWW-Authenticate。对响应头域的扩展要求通讯双方都支持，如果存在不支持的响应头域，一般将会作为实体头域处理。

| 应答头        | 说明                                                         |
| :------------ | :----------------------------------------------------------- |
| Age           | 当代理服务器用自己缓存的实体去响应请求时，用该头部表明该实体从产生到现在经过多长时间了 |
| Server        | WEB 服务器表明自己是什么软件及版本等信息                     |
| Accept-Ranges | WEB服务器表明自己是否接受获取其某个实体的一部分的请求        |
| Vary          | WEB服务器用该头部的内容告诉 Cache 服务器，在什么条件下才能用本响应所返回的对象响应后续的请求 |

# 实体头部

实体头部提供了有关实体及其内容的大量信息，从有关对象类型的信息，到能够对资源使用的各种有效的请求方法。总之，实体头部可以告知接收者它在对什么进行处理。请求消息和响应消息都可以包含实体信息，实体信息一般由实体头域和实体组成。实体头域包含关于实体的原信息，实体头包括信息性头部Allow、Location，内容头部Content-Base、Content-Encoding、Content-Language、Content-Length、Content-Location、Content-MD5、Content-Range、Content-Type，缓存头部Etag、Expires、Last-Modified、extension-header。

| 应答头           | 说明                                                         |
| :--------------- | :----------------------------------------------------------- |
| Allow            | 服务器支持哪些请求方法                                       |
| Location         | 表示客户应当到哪里去提取文档，用于将接收端定位到资源的位置（URL）上 |
| Content-Base     | 解析主体中的相对URL时使用的基础URL                           |
| Content-Encoding | WEB服务器表明自己使用了什么压缩方法压缩响应中的对象          |
| Content-Language | WEB 服务器告诉浏览器理解主体时最适宜使用的自然语言           |
| Content-Length   | WEB服务器告诉浏览器自己响应的对象的长度或尺寸                |
| Content-Location | 资源实际所处的位置                                           |
| Content-MD5      | 主体的MD5校验和                                              |
| Content-Range    | 传送的范围                                                   |
| Content-Type     | WEB 服务器告诉浏览器自己响应的对象的类型                     |
| Etag             | 供WEB服务器判断一个对象是否改变了                            |
| Expires          | WEB服务器表明该实体将在什么时候过期，对于过期了的对象，只有在跟WEB服务器验证了其有效性后，才能用来响应客户请求 |
| Last-Modified    | WEB服务器认为对象的最后修改时间 |

# 参考文献

[CSDN-wangzhibo_csdn](https://blog.csdn.net/wangzhen_csdn/article/details/80776991)
[segmentfault-某熊猫桑](https://segmentfault.com/q/1010000010814115)