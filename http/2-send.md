---
title: 发送http请求
layout: default
---

# 发起 HTTP 请求

来说说发起http请求之后，表面那些事（用浏览器发起请求），和底层那些事（用 curl 工具发起请求）。这些我们观察到的现象就是后续我们进行深入的 HTTP 知识讨论的起点。

### 资源和 URL

HTTP 最开始是浏览器发出请求。但是请求的是什么呢？是服务器上的资源，英文叫 Resource 。

对应的每一个资源，都有一个 URL ，也就是 **统一资源定位地址**，指向这个资源。不过资源分两种：

打个比方

我们有 http://haoqicat.com/peter.txt ，这个 URL 就是指向一个静态资源的。如果是 http://haoqicat.com/username 这个可能就是指向动态资源的，后台对应的可能就是一个 API 。

### 浏览器的 HTTP 请求


发起一个 HTTP 请求很容易。比如你说你想用浏览器访问 百度 你所需要做的仅仅是启动浏览器然后在地址栏输入 http://baidu.com ，然后你就可以在页面中看到好奇猫网站的首页了

>GET http://baidu.com/

上面的GET是http的一个方法，（或者死http动词）

百度 的服务器收到请求后，给出响应。响应中带有各种数据，html/css/图片 等等，返回到浏览器。 浏览器是理解这些文件格式的，所以可以最终展示一个美观的网页给用户。

### 使用 curl 发起请求

因为浏览器给我们展示的是处理过的服务器响应，我们看不到服务器发给我们的响应的本来面目。怎么样才能看到原始的 HTTP 响应数据呢？

现在我们就可以用一个http的工具`curl`来进行测试，curl可以处理响应的数据，这样我们就可以看到原始请求和响应的数据

怎么做呢，执行命令

>$ curl  https://baidu.com -v

会有下面的显示

```
$ curl  https://baidu.com -v
* Rebuilt URL to: https://baidu.com/
*   Trying 220.181.57.217...
* Connected to baidu.com (220.181.57.217) port 443 (#0)
* found 173 certificates in /etc/ssl/certs/ca-certificates.crt
* found 696 certificates in /etc/ssl/certs
* ALPN, offering h2
* ALPN, offering http/1.1
* SSL connection using TLS1.2 / ECDHE_RSA_AES_128_GCM_SHA256
* 	 server certificate verification OK
* 	 server certificate status verification SKIPPED
* 	 common name: www.baidu.cn (matched)
* 	 server certificate expiration date OK
* 	 server certificate activation date OK
* 	 certificate public key: RSA
* 	 certificate version: #3
* 	 subject: C=CN,ST=beijing,L=beijing,O=BeiJing Baidu Netcom Science Technology Co.\, Ltd,OU=service operation department,CN=www.baidu.cn
* 	 start date: Sun, 10 Apr 2016 00:00:00 GMT
* 	 expire date: Tue, 11 Apr 2017 23:59:59 GMT
* 	 issuer: C=US,O=Symantec Corporation,OU=Symantec Trust Network,CN=Symantec Class 3 Secure Server CA - G4
* 	 compression: NULL
* ALPN, server accepted to use http/1.1
> GET / HTTP/1.1
> Host: baidu.com
> User-Agent: curl/7.50.1
> Accept: */*
>
< HTTP/1.1 302 Moved Temporarily
< Server: bfe/1.0.8.18
< Date: Sun, 12 Mar 2017 10:03:59 GMT
< Content-Type: text/html
< Content-Length: 161
< Connection: keep-alive
< Location: http://www.baidu.com/
<
<html>
<head><title>302 Found</title></head>
<body bgcolor="white">
<center><h1>302 Found</h1></center>
<hr><center>bfe/1.0.8.18</center>
</body>
</html>
* Connection #0 to host baidu.com left intact

```

使用 curl 工具，向 百度 发起了一个 HTTP 请求。请求方法为 GET 。如果看一下 man curl 也就是查看 curl 的手册，可以看到 -X 选项后面是专门用来指定 HTTP 方法的。最后的 -v 用来显示详情。所以我们才能看到比较详尽的后续输出内容。
