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

说一下
