---
title: 直通全栈
layout: default
---


# 直通全栈

现在来将之前的内容来做一下总结，来看列表
- 最贴近用户的，是 React
- HTTP 请求，用 axios
- 后台，我们使用 express
- 最底层，海量数据，用 Mongodb

我们来讲下面的内容来实现一下

### 使用 Mongoose 来查询所有用户

首先，保证 mongodb 处于运行状态，然后，通过　mongo-express 查看一下， mongodb 中是否有多个用户

现在，我们再次来到后台的`index.js`的代码中，将db.once部分修改成下面这样

```js
db.once('open', function() {
  User.find().exec(function(err, users) {
    console.log(users);
  });
});
```

这样，我们到　express-backend 文件夹中，运行，可以看到如下输出结果

```js
$ node index.js
running on port 3000...
[ { _id: 584b62b830a2a2cbf4c4c3f6,
    username: 'hope',
    email: 'hope@hope.com' },
  { _id: 584bb045ff8f0f1c7ba4fe24,
    username: 'iwen',
    email: 'iwen@iwen.com',
    __v: 0 } ]
```

可以看到，终端中可以打印出所有数据文档。证明我们的　mongoose 的　find() 接口 使用正确。

但是，我们为什么不这样来写

```js
let users = User.find();
conole.log(users)
```
find() 接口是一个 **异步函数**，所以它的返回值　users 只能 在回调函数中使用。.exec 字面意思就是执行，我们把回调函数传给它做参数。

### API返回JSON

上面数据虽然拿到，但是如果想提供给客户端使用需要完成以下两步：
- 第一步，把它要封装成一个　API
- 第二步，数据格式转换为　JSON

第一步:下面再次来调整一下后台里面的`index.js`的代码

```js
db.once('open', function() {
  console.log('success');
});

app.get('/users', function(req, res){
  User.find().exec(function(err, users) {
    console.log(users);
  });
})
```

上面把　User.find() 代码封装到了一个　API ( Web API ) 。这样， 触发条件就变了。只有当客户端发出　GET /users 请求的时候，User.find() 代码才会被执行。

暂时，我们用　curl 来模拟一下客户端请求：

>curl -X GET http://localhost:3000/users

但是，此时，curl 请求不到任何返回信息，因为　console.log(users) 只会把 信息打印到后台终端。curl 请求不到信息，未来浏览器也就请求不到。所以要把这一行 改为

// res.send() 可以数据返回给客户端，但是我们要的是　json ，所以用下面接口
res.json()

也可以这样来写

```
app.get('/users', function(req, res){
  // res.json({"users": "happypeter"});
  User.find().exec(function(err, users) {
    res.json({users});
  });
})
```

此时，再用curl来请求一次，就可以在服务端得到数据了

```js
$ curl -X GET http://localhost:3000/users
{"users":[{"_id":"584b62b830a2a2cbf4c4c3f6","username":"billie66","email":"billie@billie66.com"},{"_id":"584b760498d7b520b68a05cd","username":"pppaaa"},{"_id":"584bb045ff8f0f1c7ba4fe24","username":"inCode","email":"inCode@incode.com","__v":0}]}
```

现在，后端代码就准备完毕了

### 后端代码展示

index.js

```js
const express =  require('express');
const app = express();
const cors = require('cors');
app.use(cors());
const mongoose = require('mongoose');
const User = require('./models/user');

mongoose.Promise = global.Promise;
mongoose.connect('mongodb://localhost:27017/express-hello');
// 执行此行代码之前，要保证 mongodb 数据库已经运行了，而且运行在 27017 端口



var db = mongoose.connection;
db.on('error', console.log);
db.once('open', function() {
  console.log('success');
});


// 下面三行就是我们实现的一个 API
app.get('/users', function(req, res){
  // res.json({"users": "happypeter"});
  User.find().exec(function(err, users) {
    res.json({users});
  });
})


app.listen(3000, function(){
  console.log('running on port 3000...');
});
```

models/user.js

```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

const UserSchema = new Schema(
  {
    username: { type: String },
    email: { type: String }
  }
);
module.exports = mongoose.model('User', UserSchema);
// `User` 会自动对应数据库中的　users 这个集合
// 如果这里是　Apple 那么就会对应　apples 集合
// 如果这里是　Person 那么就会对应　people 集合
```

package.json

```json
{
  "name": "express-backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "nodemon index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.1",
    "express": "^4.14.0",
    "mongoose": "^4.7.2"
  }
}
```

回到前台

### 前台书写　axios 请求

到　react-frontend/　修改生命周期函数如下：

```js
componentWillMount() {
  axios.get('http://localhost:3000/users').then((response) => {
    console.log(response);
      // this.setState({username: response.data.username});
  })
}
```

这样，就可以看出　response 中的数据结构了，我们想要的数据可以这样拿到

```js
constructor(){
  super();
  this.state = {
    users: []
  };
}
componentWillMount() {
  axios.get('http://localhost:3000/users').then((response) => {
      this.setState({users: response.data.users});
  })
}
```

### 用map展开数组

render 函数做如下修改：

```js
render(){
  const userList = this.state.users.map((user, i) => {
    return (
      <div key={i}>
         username:
        {user.username}
      </div>
    )
  });

  return(
    <div>
      { userList }
    </div>
  )
}
```

这样就可以显示所有用户的名字了

### 前端代码如下

src/index.js

```js
mport React, { Component } from 'react';
import ReactDOM from 'react-dom';
import axios from 'axios';


class App extends Component {
  constructor(){
    super();
    this.state = {
      users: []
    };
  }
  componentWillMount() {
    axios.get('http://localhost:3000/users').then((response) => {
      // console.log(response);
      this.setState({users: response.data.users});
    })
  }
  render(){
    const userList = this.state.users.map((user, i) => {
      return (
        <div key={i}>
           username:
          {user.username}
        </div>
      )
    });

    return(
      <div>
        { userList }
      </div>
    )
  }
}

ReactDOM.render(<App/>,document.getElementById('app'));
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

.babelrc

```
{
  "presets": ["env", "react"]
}
```

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>

  <div id="app"></div>
  <script src="./build/bundle.js" charset="utf-8"></script>
</body>
</html>
```

暂时完毕
