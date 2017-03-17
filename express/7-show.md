---
title: 显示一个用户的信息
layout: default
---


这一节将前面的知识点总结了一下，包括以下的几个方面：
- MongoDB 数据库基本操作
- Mongoose 这个 JS 库的使用
- 前台向后台传递参数：涉及 axios 和 express 配合
- React 基本操作

我们要完成的任务是，用户在浏览器中点按钮，发　axios 请求访问这个链接：

>http://localhost:3000/users/一个真实的用户 id

页面上能显示用户名和邮箱

前台代码，我们线打开`mongo-express`,拷贝一个真是的id出来，然后粘到前台的`axios`中去

```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import axios from 'axios';

class App extends Component {
  constructor() {
    super();
    this.state = {
      user: {}
    };
  }
  handleClick(e){
    e.preventDefault();
    axios.get('http://localhost:3000/users/584dfb6fd5aa1c13955d5cca').then((response) => {
      console.log(response);
      this.setState({
        user: response.data
      });
    })
  }
  render(){
    return(
      <div>
        <div onClick={this.handleClick.bind(this)}>
           clickme
        </div>
        <div>
          username:
          { this.state.user.username }
        </div>
      </div>
    )
  }
}

ReactDOM.render(<App/>,document.getElementById('app'));
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

### 总结

就这样就可以点击`click me`,就会在页面上显示从后台mongodb中拿到想要的数据了
