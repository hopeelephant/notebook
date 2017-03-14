---
title: HTTP 请求的格式
layout: default
---

# HTTP 请求的格式

前面我们看到了请求和响应的流程，现在我们来说说Request的具体格式

### 请求行

第一行的内容被叫做请求行 （ Request Line ） ，具体形式如下

>GET/POST [url] HTTP/[version]   GET / HTTP/1.1

这一行就是以HTTP 方法（ HTTP Method ）打头，一般是 GET 或者 POST ，当然还有其他不太常用的方法。 当我们用 GET 发请求的时候，一般我们就是想要从服务器上 GET （拿到）一些内容，而不是想去修改服务器数据。POST 正好就是用来修改服务器上的数据的。到底要 GET 或者要修改哪个资源，就是后面的 URL 这一项来指定了。上面例子中，请求的 URL 是 / 。最后就是跟 HTTP 字样，再跟上到底是使用的哪个版本的 HTTP 协议，目前一般都是 HTTP 1.1 了。

请求的头部 Headers

请求行下面的内容就是请求头部了，注意头部是复数，也就水说这一项可以有多个`header`

请求返回的格式是这样的

>[header 名]：[header 值]

上一节我们请求了三个头部

```
Host: baidu.com
> User-Agent: curl/7.50.1
> Accept: */*
```

看一下上面三项的特点
- 第一个，Host 代表被请求的主机，也就是 haoqicat.com
- 第二个，User-Agent 代表用户使用的客户端，我们这里用的是 curl
- 第三个，Accept 后面指明客户端可以接受的返回资源的类型，* 代表所有类型都接受

其他的 header 还有很多，可以参考 Wikepeida 上的列表 。

### 请求主体

请求主体其实严格的术语叫做请求的负载数据 payload 。

请求头之下，一个 request 中还可能包含负载数据（ payload ），GET请求不带负载数据，但是POST请求却会带，因为post请求是会改动服务器的数据的

比如我们填写的表单点击提交之后就会发出一个POST请求，而我们填写的数据， 就会作为 payload 成为请求的一部分。

### 总结

一个 HTTP 请求，第一会有一个请求行，然后会有几项 header ，最后，可能会有 payload 。这个就是任何一个 HTTP 请求的基本格式了。
