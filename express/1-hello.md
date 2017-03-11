---
title: 安装react
layout: default
---


# Express 框架

### 上手Express

express是一个后端框架，身为一名合格的前端开发人员，掌握一点后端知识是很有必要的，所以就在介绍一下express

我们知道，实现后端的一些功能，我们需要用到nod.js

Express就是nodejs的一个框架

### 什么是API

说道Express,不得不说一下`API`,一直以来大家可能对api这个概念比较模糊，我也是比较模糊的，不过不要紧，我们来看看他的英文解释`Application`

Program Interface英文好的人可以简单的概括一下它，它就是个 **接口**，而express就是用来制作后台接口的，或者是用来制作后台api的

那么这些api制作好了是用来干嘛的呢，那就是来给前台用的，现在对后台和前台是不是又有了更多一点的了解呢

### 做一个小例子

第一步

```
mkdir express-hello
cd express-hello
npm init -y
```

npm init -y 之后就可以生成`package.json`文件,那么这个项目我们就可以称之为**nodejs**项目了

第二部

```
npm install --save express
```

装包的时候记得项目名不要和包名一样，要不然就会出现让你不舒服的效果

### 后台代码和es6

写前台代码现在一些浏览器对其还不是特别支持，所以需要用到`babel`,但是后台代码几乎对es6语法差不多都支持了，不过有一点需要主要的是，不能用import,(nodejs是不支持es6模块语法的)，所以我们就用`require`来代替import吧，`require`是commonjs模块语法，nodejs对其是支持的


### 开始了

首先在项目中创建一个`index.js`文件，做如下操作

```
const express =  require('express');
const app = express();

app.listen(3000);
```

上面的几句简单的代码，我们就实现了一个简单的服务器的功能。看代码中有一个`listen`指的是始终在监听客户端发送的请求

上面的`3000`是端口号，英文是`port`,简单的来说，一个服务器就想一座大楼，而3000就是大楼里面的一个门牌号

上面是用const声明的，我们就来说说`const`和`let`的区别，const是只读变量，而let是可修改变量

想让上面的程序执行，我们就字啊后台去运行一下，由于我们写的 `index.js`是`nodejs`程序，所以我们需要用`node`去执行

>node index.js

现在我们是没有办法输出内容的，现在我们来修改一下代码

上面的

>app.listen(3000);

修改成

```
app.listen(3000, function(){
  console.log('running on port 3000...');
});
```

现在我们再来

>node index.js

就会出现

>running on port 3000...

上面添加了一个回调函数，所谓回调函数就是程序会先执行一些操作，回过头再来执行回调函数，
回调函数的使用环境就是之前的操作耗时长或者是异步，我们就会用到回调韩数

### express服务器运行

服务器监听端口的作用就是根据端口传入的请求，执行特定代码

例如

我们在上面的 `index.js`中的app.listen中写上

```
app.get('/', function(){
  console.log('request come in...');
})
```

上面的`get('/')`是？
- get 是一个 http 请求的动词，，类似的还有 post/delete/put
- `/`很明显是一个路径

动词加上路径就有了**HTTP请求**，看下面

>request = verb + path + data

这里是服务端，是来接受请求的，发请求的当然是客户端

### 客户端发请求

> GET /

这个请求必须来自3000端口

可以发请求的方式不唯一，可以用浏览器地址栏，可以用页面的 form 发， 也可以用 axios 发，后者使用专门的 API 调试工具 curl/postman 来发。

我们现在在浏览器的地址栏来试一下

>http://localhost:3000/

localhost 就是我们自己机器的域名

上的请求，默认动词就是 GET ，同时 :3000 用来指定端口号。

请求之后，会发现浏览器里没有任何输出，这是因为，我们的 express 服务器根本就没有给前台返回任何字符串，回调函数中的 `console.log()` 只能把字符串打印到后台。

### 什么是前端和后端

什么是前端和后端就不聊了，我们来聊聊api,前端是 API 的使用，后端是 API 的生产者。后台 API 写好之后，默认不运行，只有当前端发送过请求来的时候才会触发后台 API 代码运行。

所以可以退出用`express`写的是后端代码，而`react`肯定就是前端代码了

### 让字符串出现在客户端

我们将上面app.get()中的代码修改成这样

```
app.get('/', function(req, res){
  res.send('Hello World');
})
```

上面代码中 req 是 request 请求的简写， res 是 response 响应的简写 。res.send('Hello World'); 的作用是从后端向前端浏览器返回字符串 Hello World


给出简单的例子做一下尝试

```js
// GET /title
app.get('/title', function(req, res){
    res.send('my title');
  }
)

// GET /content
app.get('/content', function(req, res){
  res.send('my content');
})
```

后端代码展示

  package.json

  ```json
  {
  "name": "express-hello",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.14.0"
  }
}
  ```

index.js

```js
const express =  require('express');
const app = express();


// 下面三行就是我们实现的一个 API
app.get('/', function(req, res){
  res.send('Hello World');
})

app.listen(3000, function(){
  console.log('running on port 3000...');
});
```

上面的两个文件都放在之前创建的`express-hello`文件中。

执行命令

```
cd express-hello
npm install
node index.js
```

跑起来了
