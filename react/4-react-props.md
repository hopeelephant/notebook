---
title: 安装react
layout: default
---

# react props

上一节中说了下`react`中的`state`属性，今天来说一下另外一个比较重要的属性,那就是`props`属性

简单的来将`props`属性是一种用于沟通的媒介，是通过父级组件向子组件传递数据，当然，你也可以设置默认的`props`属性

来简单的看一下例子

```
import React from "react";
class Btn extends React.Component{
  render(){
    let styles = {
      padding:"5px",
      backgroundColor:this.props.bg,
      color:"#fff",
      boder:"1px solid red"
    }
    return(
      <button style = {styles}>{this.props.tittle}</button>
    )
  }
}
export default Btn;

```

在这儿我们在return()方法里面写了`<button style = {styles}>{this.props.tittle}</button>`一个按钮，但是我们却想传入三个不同的按钮，这个时

候就用到了`props`属性中的`tittle`属性，当然这个`tittle`是随便取得名字，还有我们定义的样式的方法`backgroundColor:this.props.bg`，这样就可

以改变你想要变换按钮的样式了，在这个文件中我们一共引入了两次`props`属性，当然你可以传入多次`props`属性来达到你想要的效果

接着我们在文件的父级将这个文件导入，我们就可以在父组件中来传入多个按钮

来看一下

```
import React from "react";
import Btn from "./Btn";
import "./main.css";
class App extends React.Component{
  render(){
    return(
      <div>
        <Btn  tittle="hello" bg="red" />
        <Btn  tittle="world" bg="yellow" />
        <Btn  tittle="wang"  bg="blue"/>
      </div>
    )
  }
}
export default App;

```
首先引入子组件中定义了`props`属性的文件，接着我们就可以来来编写我们在子组件中定义的`props`的值，我们在子组件中传入了两次值，所以就可以直接用

这个值来定义我们想要的数据和样式

再看一个例子

```
import React from "react";
class Card extends React.Component{
  render(){
    return(
      <div className="card">
        <h1>{this.props.index}</h1>
        <p>{this.props.text}</p>
      </div>
    )
  }
}
Card.defaultProps = {
  index:1,
  text:"苏苏"
}
export default Card;

```

在这个组件中我添加了

```
Card.defaultProps = {
  index:1,
  text:"苏苏"
}
```

这个对象里面写的是默认的数据，当我们在父组件中没有传入数据的时候，就采用默认的数据

在看看父级组件的写法

```
import React from "react";
// import Btn from "./Btn";
import Card from "./Card";
import "./main.css";
class App extends React.Component{
  render(){
    return(
      <div>
        <Card />
        <Card index="2" text="周慧敏" />
        <Card index="3" text="经文" />
        <Card index="4" text="牛逼" />
        <Card index="5" text="学习" />
        <Card index="6" text="很爱很爱" />
        <Card index="17" text="计算机世界" />
      </div>
    )
  }
}
export default App;

```

这样就可以来实现每一个`<Card />`结束标签能够传递不同的数据，

首先我们引入`./Card`文件，给他取名叫做`Card`,这样`Card`里面就储存了`./Card`文件中的数据，这样我们就可以通过`Card`结束标签的形式映入

`./Card`里面的内容
