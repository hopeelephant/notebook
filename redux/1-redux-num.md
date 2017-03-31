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

```js
import { createStore } from 'redux';

let comments = []

function commentReducer(state = [], action) {
  return state;
}

let store = createStore(commentReducer, comments);

export default store;

```

然后到 index.js 中

```js
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

### 后台 API

>curl http://redux-hello.haoduoshipin.com/comments

### 发起 API 请求

现在 store 中的数据是 [] ，现在我们肯定是要修改这个状态值了，那么要涉及到的是：

- 先发action

- 然后触发reducer

退一步思考，发出这里的这个 action 是没有必要让用户参与进来点按钮，那么如何触发呢？就用生命周期函数就行了。

所以需要到 App.js （刚刚从 index.js 中抽离的）中，添加

```js

import { fetchComments } from './actions/comment';

componentWillMount(){
 this.props.fetchComments();
}

```

这里，fetchComments 是一个 Action 创建器 ，在 actions/comment.js 中，它的定义先写成这样：

```js
export function fetchComments() {
  return dispatch => {
    console.log('fetchComments...');
  }
}
```

上面的代码是有 dispatch 的，也就是可以发异步请求的，直接运行上面代码肯定报错

>...middleware for aync operations

我们就知道，我们需要到 store.js 中加载 redux-thunk

到这里，我们能达成的效果是：App 组件一加载，终端中就可以打印

>fetchComments...

了。

代码:[use thunk](https://coding.net/u/hopeelephant/p/redux-num/git/commits/master/);

上面代码中也用了 react-redux 的接口，例如 Provider/connect ，都是迫不得已加上的，因为不加就报错了。

到目前，我们只是实现了对于 action 创建器 的调用，具体的 action 和 reducer 还都没写呢。

### axios 发请求

到 acitons/comments.js 中：

```js
import axios from 'axios';
export function fetchComments() {
  return dispatch => {
    axios.get('http://redux-hello.haoduoshipin.com/comments').then( res =>
      console.log(res.data.comments)
    )
  }
}
```

这样就可以在后台打印出总的评论数了

发起 action 触发 reducer

接下来数据到手了，可以发 action 了，具体就是使用 dispatch

到 acitons/comment.js 中添加

>dispatch({type: 'LOAD_COMMENTS', comments: res.data.comments});

这样就可以发出一个 action 了。下一步马上看 reducer 中能不能收到数据。

store.js 中，commentReducer 写成下面这样：

```js
function commentReducer(state = [], action) {
  switch(action.type){
    case 'LOAD_COMMENTS':
      console.log('commentReducer', action.comments);
      return action.comments;
    default:
      return state;
  }
}
```

现在就可以打印出总的评论数了，但是 App.js 还是用的 getState() 这个还是要换成

>this.props.comments

代码

[reducer code]

- (https://coding.net/u/hopeelephant/p/redux-num/git/commits/master/)
