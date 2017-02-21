---
title: 安装react
layout: default
---

# 一些state例子


### 标签页切换

```
import React from "react";
import Tab1 from "./Tab1";
import Tab2 from "./Tab2";
import Tab3 from "./Tab3";
class SelectBar extends React.Component{
  constructor(){
    super();
    this.state = {
      show : 0
    }
  }
  handleClick(num){
    console.log(num);
    this.setState({show:num})
  }
  render(){
    return(
      <div>
        <button onClick = {this.handleClick.bind(this,0)}>选项1</button>
        <button onClick = {this.handleClick.bind(this,1)}>选项2</button>
        <button onClick = {this.handleClick.bind(this,2)}>选项3</button>
        {this.state.show===0 ? <Tab1 /> : this.state.show===1 ? <Tab2 /> : <Tab3 />}
      </div>
    )
  }
}
export default SelectBar;
```

首先我们引入选项卡1,2,3,当点击`button`按钮的时候来看`handleClick`函数，函数里面的`num`值是有`button`按钮里面的bind()里面`this`后面的值决

定的，比如我们点击第一个按钮`handleClick`函数里面的`num`参数就是0，点击第二个按钮`handleClick`函数里面的`num`参数就是1，点击第三个按

钮`handleClick`函数里面的`num`参数就是2

`handleClick`函数里面的对象`show`的属性值发生变化，从二`constructor`函数里面的`show`的值也会发生变化，这样就可以在`render`函数里面插入

```
{this.state.show===0 ? <Tab1 /> : this.state.show===1 ? <Tab2 /> : <Tab3 />}
```

这个三目运算符指的是当`show`的值全等于0的时候显示的是<Tab1 />,这个三目运算符指的是当`show`的值全等于0的时候显示的是<Tab1 />,否则显示<tab3 />

### 抽奖

```
import React from "react";
let data = ["保存","hah","shhshsh","sjisiis","kskskks"];
class EatWhat extends React.Component{
  constructor(){
    super();
    this.state={
      start : false,
      data,
      text:""
    }
  }
  select(){
    let result = this.state.data[Math.floor(Math.random()*this.state.data.length)]
    this.setState({text:result})
  }
  handleClick(){
    if(this.state.start){
      this.setState({start:false});
      clearInterval(this.interval);
    }else{
      this.interval = setInterval(() => this.select(),100);
      this.setState({start:true});
    }
  }
  render(){
    return(
      <div>
          <p>今天吃什么：{this.state.text}</p>
          <button onClick = {this.handleClick.bind(this)}>{this.state.start ? "停止" : "开始"}</button>
      </div>
    )
  }
}
export default EatWhat;

```

来解释一下，当点击`button`的时候执行`handleClick`函数,这个函数里面是个条件判断语句，如果状态是`true`的话，点击之后，就将状态变成`false`

并且清除计时器，如果状态是`false`的话，点击之后，就将状态变成`true`,并且开始执行计时函数，计时函数里面返回两个值，一个是`select`函数，一个

是`100`，指的是每`100`毫秒执行一次`select`函数

### 动画

```
import React from "react";
class Trans extends React.Component{
  constructor(){
    super();
    this.state = {
      show:true
    }
  }
  handleClick(){
    this.setState({show : !this.state.show})
  }
  render(){
    let styles = {top:this.state.show ? "35%" : "2%"}
    let height = {height:this.state.show ? "200" : "0"}
    return(
      <div className="container" style = {styles}>
        <button onClick = {this.handleClick.bind(this)}>{this.state.show ? "上" : "下"}</button>
        <div className="blog" style = {height}>
          <h1>博客</h1>
          <h1>博客</h1>
          <h1>博客</h1>
          <h1>博客</h1>
        </div>
      </div>
    )
```
这是一个简单的动画效果，也是用点击按钮的时候来控制组件的`状态`来实现的
