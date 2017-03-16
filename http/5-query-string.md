---
title: 查询字符串
---

开发者日常要解决的问题之一，就是如何把一定的数据传递给服务器端。方法列举出下面几种
- 最简单，最常用的，就是我们本节要介绍的通过“查询字符串”来传递数据
- 通过 html 表单穿数据
- 同 axios 这样的客户端传递数据
- 通过链接中的格式提取传递参数

### 介绍

GET 请求中携带一些数据到服务器端的方法并不唯一，但是一种非常简单也非常常用的方式就是，使用“查询字符串”来传递数据，或者叫传递参数。

查询字符串这个传输数据的方式，最早就是用来给搜索引擎传递“查询关键字”，这个就是”查询字符串“这个名字的由来。但是时至今日，通过这种方式传递的数据可以是任意数据，不一定非得是查询关键字。

虽然一般我们发送一个 GET 请求，就直接请求网站链接就可以了，例如访问 http://haoqicat.com 或者 http://haoqicat.com/http-with-peter 。但是有的时候，我们也希望 GET 请求能够携带一些更为详细的数据到服务器端，以便服务器更为精确的为我们提供相应内容。

格式

打开 chrome 浏览器，打开 chrome 开发者工具的 Network 标签。然后浏览器中访问

>http://haoqicat.com/?name=happypeter

上面的 ?name=happypeter 就是所谓的 **查询字符串**，这里面传递了一个参数，也就是 name ，参数值是 happypeter 。

此时，Network 标签下会看到，页面发出了多个请求，点第一个，也就是

>?name=happypeter

这个请求，在 chrome 开发者工具的右下角，可以看到：

>这个请求，在 chrome 开发者工具的右下角，可以看到：

```
Query String Parameters
name: happypeter
```

意思就是

```
Query String Parameters
name: happypeter
```

这些数据会作为请求的一部分，发送给服务器的。服务器端的框架，例如 express 有自己的办法去得到这些参数值， 至于服务器端代码如何使用这些参数，那就是自由的了。

传多个参数

传多组参数，用&隔开，比如

>http://haoqicat.com/?name=happypeter&email=peter@peter.com

Chrome 开发者工具右下角，此时就会看到两个参数了。

也可以这样来写

> ?order=desc&shoe[color]=blue&shoe[type]=converse
