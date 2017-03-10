---
title: 安装react
layout: default
---

# React 和Express的结合

有了 API ，功能还不完全。需要有前端来调用 API ，完成整个小功能

虽然前端和后端都是用 JS 来写，但是前端和后端是完全独立的两个项目，通过 API 来作为桥梁。其实，我们后端虽然是 Nodejs 写的，但是用 PHP/JAVA 也能写。

### 前端测试

现在在前端项目中要用的东西清单
- 页面最终显示出来的，就是你的用户名，例如 happypeter
- 要用到 react 的 state ，constructor ，生命周期
- 用 ES6/Babel/Webpack

`tip`创建 React 应用的脚手架项目 可以推荐的是 https://github.com/facebookincubator/create-react-app

创建一个前端的文件夹，最好是叫`react-frontend`

然后在src/index.js中写上

```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';


class App extends Component {
  constructor(){
    super();
    this.state = {
      username: ''
    };
  }
  componentWillMount() {
    this.setState({username: 'happypeter'});
  }
  render(){
    return(
      <div>
        {this.state.username}
      </div>
    )
  }
}

ReactDOM.render(<App/>,document.getElementById('app'));
```

package.json

```json
{
  "name": "react-frontend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "babel-core": "^6.23.1",
    "babel-loader": "^6.4.0",
    "babel-preset-env": "^1.2.1",
    "babel-preset-react": "^6.23.0",
    "react": "^15.4.2",
    "react-dom": "^15.4.2",
    "webpack": "^2.2.1"
  }
}
```

webpack.config.js

```js
var path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'src/index.js'),
  output: {
    path: path.resolve(__dirname, 'build'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: 'babel-loader'
      }
    ]
  }
};
```

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>

  <div id="app"></div>
  <script src="./build/bundle.js" charset="utf-8"></script>
</body>
</html>
```

.babelrc

```
{
  "presets": ["env", "react"]
}

```

安装 http-server

前端代码也是可以泡在服务器上面的

既然想跑在服务器上就需要装包了，开装

>npm install -g http-server

我们就有了一个简单的系统工具叫 http-server

```
cd react-frontend/
http-server .
```

这样就可以讲前端项目在`http`服务器上面启动了

warn:有时候会出现 bundle.js 更新了，但是刷新页面看不到效果的情况，可能是有缓存相关的问题。

### 两次设置state

再后面我们会用到`axios`来请求后台的数据，就可以知道为什么这么用了

### API实现

开发一个功能，好的做法是，先修改后端代码，也就是先实现 API ，然后下一步就是用 curl 这样的命令，来测试一下 API ，发现 API 没毛病，然后再动手去写前端代码。

打开后端项目，在`index.js`中添加下面的内容

```js
app.get('/username', function(req, res){
  res.send({username: 'happypeter'});
})

```

### 用 curl 来测试 API

测试的时候可能会出现连接 localhost:3000 失败，连接被拒绝。这个提示的英文，我翻译成英文了，那是因为没有启动后端，启动一下后端就可以了

### 安装 axios 发送 http 请求

axios是做什么的呢，它是专门用来发`http`请求的，axios 是常用的发 http 请求的工具，有了这个工具，一般就不在说ajax了

还是来装包

>npm install --save axios

将这个包装到前端项目中来，装好包之后。将包引入到`src/index.js`

import axios from 'axios';

我们当前的请求不希望是通过按钮来触发，而是希望，页面加载的时候，自动发出 http 请求，向服务要数据，所以，代码非常适合写到生命周期函数中：

```js
componentWillMount() {
  axios.get('http://localhost:3000/username').then( response =>{
      return console.log(response);
    }
  )
}
```

### 跨域请求 Access-Control-Allow-Origin

这是一个比较难搞的问题

代码运行到上面，在浏览器中会报下面的一些错

```js
XMLHttpRequest cannot load http://localhost:3000/. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'null' is therefore not allowed access.
```

XMLHttpRequest 是发 HTTP 请求的底层机制，是浏览器自带功能。上面的报错翻译如下：

```
无法加载后台 http://localhost:3000 . 被请求的资源中没有设置 Access-Control-Allow-Origin 头部。源头设置为 Null ，所以不允许 访问。
```

那么，如何开通服务器上的这个资源访问权限呢？就是要在服务器上做下面的设置

>Access-Control-Allow-Origin: *

有了这个设置，所有的第三方网站都可以访问服务器上的资源了。

### 跨域请求的解决方案

解决方案采用： https://github.com/expressjs/cors cors 是 Cross Origin Resource Share ，安装了这个包就可以完成

```
curl -I http://localhost:3000/
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: text/html; charset=utf-8
Content-Length: 11
ETag: W/"b-sQqNsWTgdUEFt6mb5y4/5Q"
Date: Thu, 08 Dec 2016 01:51:44 GMT
Connection: keep-alive

```

curl 的 -I 选项用来专门拿到服务器返回的 header 。命令返回的信息，就是服务器端被请求资源的的 header 。

上面很明显是没有 Access-Control-Allow-Origin 这一项的。下面我们安装 cors 这个包，就可以解决这个问题。

下面我们来添加两行简单的的代码，再来重启一下服务器看看，代码如下

```
const cors = require('cors')
app.use(cors());
```

我们再用 curl -I 看看输出如下：

```js
HTTP/1.1 200 OK
X-Powered-By: Express
Access-Control-Allow-Origin: *
Content-Type: text/html; charset=utf-8
Content-Length: 11
ETag: W/"b-sQqNsWTgdUEFt6mb5y4/5Q"
Date: Thu, 08 Dec 2016 02:17:23 GMT
Connection: keep-alive
```

现在，我们就可以看到Access-Control-Allow-Origin: * 了，刷新一下浏览器，错误就没有了
