---
title: http简介
layout: default
---

# HTTP 简介

HTTP 全称就是“超文本传输协议”，超文本就是 HTML 。 我们的浏览器和服务器进行通信，就是通过 HTTP 来进行的

### http之前

对于浏览者来说，我们在搜索网站的时候一定是会输入3个大不留，http，等一系列我们并不懂的字符，我们就可以在电脑上接收信息了，那么这些内容是怎么来的，对于浏览者来说显得没有那么重要。但是对于我们开发者来说，就显的很重要了

### Web 客户端和服务器端

先来说一下web和internet的区别，他们二者都是网的意思，nternet 是由多台计算机互联组成的网络，Web 是由多个网页通过超级链接组成的网。Internet 主要通过 tcp/ip 来连接，Web 通过 http 协议来连接。

Web 内容都是存储在 Web 服务器上的，Web 服务器都是用 HTTP 协议的，因此也被称为 HTTP 服务器。HTTP 服务器存储了各种类型的数据，如果 HTTP 的客户端发出请求的话，服务器就会返回数据给客户端，叫做响应。请求（ request )和响应（ response ）都是重要的术语

HTTP 的服务器和客户端是万维网（ World Wide Web ）的基本单元。其实我们每天都在使用 HTTP 的客户端，最常见的客户端就是浏览器。浏览一个页面的时候，浏览器会向服务器发出一个 HTTP 请求。等到服务器响应返回之后，浏览器再去处理响应数据，以美观的形式展示给用户。

### HTTP 的请求和响应

HTTP 协议最重要的两个概念就是请求（ request ）和响应（ response )。请求是由浏览器发出的，响应是由服务器给出的。

请求由 **请求头** 和 **请求主体** 组成。响应由 **响应头** 和 **响应主体** 来组成。

### 代码演示

简单http服务器跑起来

看代码

index.js

```js
const express = require('express');
const app = express();

app.get('/', function(req, res){
  console.log('hello');
  res.send('hello world');
})

app.listen(3000, function(){
  console.log('running on port 3000...');
});
```
然后,在后台

>nodemon index.js

启动后台服务器，泡在3000端口上面,可以看到`hello world`,我们也可以在`hello-world`上面添加`html`标签来显示不同的大小

### 请求响应

前台用浏览器发请求，也可以看到数据，但是看不到底存数据，所以现在我们用curl请求一次

>curl -X GET localhost:3000 -v

上面的-v表示的是显示详情，现在看一下输出结果

```
* Rebuilt URL to: localhost:3000/
* Hostname was NOT found in DNS cache
*   Trying ::1...
* Connected to localhost (::1) port 3000 (#0)
> GET / HTTP/1.1
> User-Agent: curl/7.37.1
> Host: localhost:3000
> Accept: */*
>
< HTTP/1.1 200 OK
< X-Powered-By: Express
< Content-Type: text/html; charset=utf-8
< Content-Length: 11
< ETag: W/"b-XrY7u+Ae7tCTyyK7j1rNww"
< Date: Sat, 17 Dec 2016 01:40:49 GMT
< Connection: keep-alive
<
* Connection #0 to host localhost left intact
hello world
```

### 解释输出结果

我们可以看一下箭头的指向的方向

请求头

```
> GET / HTTP/1.1
> User-Agent: curl/7.37.1
> Host: localhost:3000
> Accept: */*
```

请求主体：没有。一般 GET 请求，是没有请求主体的。POST 一般是有主体的。

响应头

```
< HTTP/1.1 200 OK
< X-Powered-By: Express
< Content-Type: text/html; charset=utf-8
< Content-Length: 11
< ETag: W/"b-XrY7u+Ae7tCTyyK7j1rNww"
< Date: Sat, 17 Dec 2016 01:40:49 GMT
< Connection: keep-alive
```

响应主题

>hello world

通常我们请求，就是请求一个 html 页面，那么响应主体就是：html 代码。
