---
title: redux-thunk 显示一个数字
layout: default
---

# redux-thunk 显示一个数字

来看一下redux-thunk的一个简单案例，怎样的不用组件中的state来显示一个评论数

一起来看看

### 基本环境配置

- [show 0 comment](https://coding.net/u/hopeelephant/p/redux-num/git/commit/87ff9cd2ce135ea122f3b15585d54902564bbfe3)

来看看具体思路

### 页面显示“0 评论”

现在走 redux 的全套思想，让页面上显示一个 store 中存储的初始值 0 。

首先要安包：

>npm i --save redux

然后创建 store.js 数据：

```
import { createStore } from 'redux';

let comments = []

function commentReducer(state = [], action) {
  return state;
}

let store = createStore(commentReducer, comments);

export default store;

```

然后到 index.js 中

```
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import store from "./store";
class App extends Component {
  render(){
    return(
        <div>
          {store.getState().length}
        </div>
    )
  }
}
ReactDOM.render(<App />, document.getElementById('app'));

```

好了，这样我们就显示了一个最为简单的读数据的操作
