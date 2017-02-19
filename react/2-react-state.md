---
title: 安装react
layout: default
---

# react-state

今天来看一下`react`的状态思想，在之前的学习中，一直有一句话说的是，一切皆对象，那么现在来看一下`react`，他的核心思想是，一切皆装态`state`

首先一起来做一个`react`项目

我们现在复制一份昨天的react项目，记得将项目中的`build`和`node_modules`等一些东西给删除掉，只保留`.babelrc` `index.html`  `package.json`  `webpack.config.js`



保留的`package.json`文件中有我们上个项目所留下来的里面有之前项目所留下来的包记录，直接

>npm i

就可以将所有的包下下来了

另外`build`文件中记录了`build`文件，我们只需要

>npm run build

就可以在项目中生成`build`文件了

现在介绍一种新的更快的安装包的方式，那就是`cnpm`

首先进入网址

>https://npm.taobao.org

在里面找到命令

>$ npm install -g cnpm --registry=https://registry.npm.taobao.org

`-g`是全局安装的意思，不管在那个目录，那个项目下安装的`cnpm`都是可以在任何项目中随便使用的

安装好了`cnpm`之后我们以后就用`cnpm`安装包了，这样就快多了，不过其他的东西还是用`npm`去执行

好了需要做的前期工作几乎已经差不多了。

现在都实际项目中来看一下

首先创建一个`./src/index.js`文件，接着在建一个`./src/App.js`文件,注意这儿的`App`中的`A`我们需要大写

接着我们在`App.js`中写下一个例子

```
import React from "react";           //导入`react`
class App extends React.Component{            //这段代码是一个类，里面放了一些方法
  constructor(){                 //这是一个`constructor`方法，是一个固定的方法
    super();
    this.state = {                 
      num : 0,
      show : false
    }
  }
  handleAdd(){                   //这是自定义的一个方法
    this.setState({num:this.state.num+1})
  }
  handleCut(){                     //这也是自定义的一个方法     
    this.setState({show:!this.state.show})
  }
  render(){                        //render()这是一个固定的方法，用来渲染虚拟的`DOM`树

    return(
      <div>
        数字是：{this.state.num}<br />              //这个大括号里面的是一个变量
        <button onClick={this.handleAdd.bind(this)}>+1</button>
        <button onClick={this.handleCut.bind(this)}>{this.state.show?"show" : "none"}</button>
        <p style={{display: this.state.show?"block" : "none"}}>显示</p>
      </div>
    )
  }
}

export default App;                     //默认将`App`导出

```

再来看一下啊`index.js`文件

```
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
ReactDOM.render(
   <App />
   ,document.getElementById("app")
 )

```

首先将`react` `react-dom` `./App`文件导入进来，其实`./App`导入的就是`./App.js`只不过`.js`省略了

为什么省略了呢，我们可以打来配置文件`webpack.config.js`里面加入

```
resolve: {
    extensions:[".js", ".css", ".png", ".jpg" ]
  }
```

这样就可以在引入文件的时候省略以上带有`.js` `.css` `.png` `.jpg`的文件了

我们在来看一下配置文件来解释一下

```
module.exports = {
  entry: "./src/index.js",
  output: {
    path: "build",
    filename: "bundle.js",
    publicPath:"build/"
  },
  resolve: {
    extensions:[".js", ".css", ".png", ".jpg" ]
  },
  devtool: "eval",
  module: {
    rules: [
      { test: /\.js$/, exclude: /node_modules/, use : "babel-loader" },
      {test: /\.css/, use: ["style-loader","css-loader"]},
      {test: /\.(jpe?g|png)$/,use: 'file-loader'}
    ]
  }
};
```

在`rules`里面我们可以看到`babel-loader`,这个是编译`ES6`语法需要用到的东西，`css-loader`是可以让我们在外部写css语法的

我们只需要直接在`index.js`中引入`css`文件就可以了，如

>import "./main.css";

这样就可以在外部写css了

还有`file-loader`,这个是用来放图片的，由于图片是无法直接引入的，所以我们需要做的是

首先创建一个放图片路径的`js`文件，比如

```
 import React from "react";
 import img from "./images/yyy";
 class Logo extends React.Component{
   render(){
     let style = {width:"300",border:"3px solid #000"}
     return (
       <img src={img} alt="" style={style} />
     )
   }
 }

 export default Logo;
```

>import img from "./images/yyy";引入图片路径

>export default Logo;将组件`Logo`导出


在想要导入的文件中引入导出的`Logo.js`文件

>import Logo from "./Logo";
