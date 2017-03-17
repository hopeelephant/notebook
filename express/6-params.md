---
title: 前台向后台传递参数
layout: default
---

本节要做的事情就是，前台在发 axios 的 http 请求的时候，我们要携带一个参数到服务器端。这里，参数的本质就是字符串。所以这一集的就是把一个任意字符串，从前台传到后台。

比如，我们现在想把一个 “123456” 这个字符串，传递一下。

### 前台发出请求

在前台我们这样写

```
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import axios from 'axios';

class App extends Component {
  handleClick(e){
    e.preventDefault();
    console.log('handleClick......');
    axios.get('http://localhost:3000/users/123456').then((response) => {
      console.log(response);
    })
  }
  render(){
    return(
      <div onClick={this.handleClick.bind(this)}>
         clickme
      </div>
    )
  }
}

ReactDOM.render(<App/>,document.getElementById('app'));

```

说一下,这里虽说传递的是123456，但是未来还右可能是任意的字符串

来看看后台代码

```
const express =  require('express');
const app = express();
const cors = require('cors');
app.use(cors());


app.get('/users/:id', function(req, res){
  console.log(req.params.id)
})

app.listen(3000, function(){
  console.log('running on port 3000...');
});
```

req 是 request 请求的缩写，express 用这个变量来接收前台发过来的请求。 res 是 response 响应的缩写，用来响应前台发过来的请求，实际作用就是往前台发送数据。

前台的请求是：

>GET /users/123456

后台API如果写成这样：

>app.get("/users"...)

是匹配不上的，因此可以写成

>app.get('/users/123456'...)

但是这样前台能传递的字符串就限制死了。所以最好就是使用 express 的 params （param 是英文参数的简写） 机制来进行处理，也就是写成如上的

>app.get('/users/:id')

注意：上面的id写成其他的单词也是可以的，关键点是前面的冒号，这样写之后，前台请求中的字符串，就可以在后台通过req.params.id这个变量拿到了

总结，前台向后台传递数据的方式右很多中，但是axios算是最简单的一种
