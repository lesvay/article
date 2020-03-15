---
title: HTTP请求方法
date: 2020-03-14 11:19:21
categories: 
    - 计算机网络
tags: 
    - http
---

HTTP1.0 定义了三种请求方法： GET, POST 和 HEAD方法。

HTTP1.1 新增了六种请求方法：OPTIONS、PUT、PATCH、DELETE、TRACE 和 CONNECT 方法。

所以HTTP目前为止一共有九种请求方法。

# HEAD(获取报头)

> The **HTTP `HEAD` method** requests the headers that are returned if the specified resource would be requested with an HTTP `GET` method. Such a request can be done before deciding to download a large resource to save bandwidth, for example.
>
> A response to a `HEAD` method should not have a body. If so, it must be ignored. Even so, entity headers describing the content of the body, like `Content-Length` may be included in the response. They don't relate to the body of the `HEAD` response, which should be empty, but to the body which a similar request using the `GET`method would have returned as a response.

HEAD与GET方法类似，但是它不会返回消息体，用来获取报头，通常用来测试超链接的有效性、可用性。

# GET(查询)

> The **HTTP `GET` method** requests a representation of the specified resource. Requests using `GET` should only retrieve data.

HTTP协议规定GET是获取资源的方法，通过URL提交，在地址栏中可以看到，其所提交的数据最多只能有1024个字节。GET有利于资源的传播，其请求在Ajax环境下不会被缓存，有利于减轻服务器的压力。

# POST(新增)

> The **HTTP `POST` method** sends data to the server. The type of the body of the request is indicated by the Content-Type header.

HTTP协议规定POST是创建资源的方法，其内容是在HTTP请求的body里实现，POST传输数据时不会在URL里显示，可以传输较为大量的数据，在Ajax环境下会被缓存，非幂等的，多次访问都会产生影响。

# PUT(修改)

> The **HTTP PUT request method** creates a new resource or replaces a representation of the target resource with the request payload.
>
> The difference between `PUT` and `POST` is that `PUT`is idempotent: calling it once or several times successively has the same effect (that is no side effect), where successive identical `POST` may have additional effects, like passing an order several times.

HTTP协议规定PUT是更新资源的方法,`PUT`是幂等的方法，即调用一次与调用多次是等价的。

#  PATCH(修改)

>The **HTTP PATCH request method** applies partial modifications to a resource.
>
>The HTTP `PUT`method only allows complete replacement of a document. Unlike `PUT`, `PATCH` is not idempotent, meaning successive identical patch requests *may* have different effects. However, it is possible to issue `PATCH` requests in such a way as to be idempotent.
>
>PATCH (like PUT) may have side-effects on other resources.
>
> To find out whether a server supports `PATCH`, a server can advertise its support by adding it to the list in the Allow or Access-Control-Allow-Methods(for CORS) response headers.

HTTP协议规定PATCH是修改资源的方法，是对PUT方法的补充，用来对已知资源进行局部更新，但PATCH与POST一样是非幂等的。

# DELETE(删除)

> The **HTTP DELETE request method** deletes the specified resource.

HTTP协议规定DELETE是删除资源的方法.

# CONNECT(代理)

>The **HTTP `CONNECT` method** starts two-way communications with the requested resource. It can be used to open a tunnel.
>
>For example, the `CONNECT` method can be used to access websites that use SSL (HTTPS). The client asks an HTTP Proxy server to tunnel the TCP connection to the desired destination. The server then proceeds to make the connection on behalf of the client. Once the connection has been established by the server, the Proxy server continues to proxy the TCP stream to and from the client.

`CONNECT`在网页开发中一般不会被用到，其作用是将服务器作为代理(访问中介)，让服务器代替用户访问别的资源，然后再将该资源返回给用户，这样用户就可以访问到只有服务器才能访问的网站(比如翻墙 )，它直接使用TCP去连接。

#  TRACE(测试)

> The **HTTP `TRACE` method** performs a message loop-back test along the path to the target resource, providing a useful debugging mechanism.

回显服务器收到的请求，主要用于测试或诊断。

# OPTIONS(测试)

> The **HTTP `OPTIONS` method** is used to describe the communication options for the target resource. The client can specify a URL for the OPTIONS method, or an asterisk (*) to refer to the entire server.
>
>  For Example, to find out which request methods a server supports, one can use curl and issue an OPTIONS request.

通过该方法传回该资源所支持的所有HTTP请求，也可以测试服务器是否可以正常使用。

# 参考文献

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods)

[菜鸟联盟](https://www.runoob.com/http/http-methods.html)

[CSDN-kobejayandy](https://blog.csdn.net/kobejayandy/article/details/24606521)

[简书-5onghua](https://www.jianshu.com/p/93727598b564)

[知乎](https://www.zhihu.com/question/31640769)

[博客园-心田居士](https://www.cnblogs.com/liuzhenbo/p/11045048.html)