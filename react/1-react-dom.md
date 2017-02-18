---
title: 安装react
layout: default
---

# 安装 react

现在来走一边react需要用到的东西和信息

首选 `mkdir` 一个文件夹 `react-me`

然后在文件夹中创建需要的文件

```
src/index.js  .balbelrc index.html
```

另外在命令行中执行

```
npm init -y
```

初始化仓库来生成一个`package.json`文件来记录我们安装的包

现在来将`react`需要用到的包安装上

来看命令

>npm install webpack --save-dev 安装webpack包

>npm install babel-core --save-dev

>npm install babel-loader --save-dev

>npm install babel-preset-env --save-dev

>npm install babel-preset-react --save-dev

>npm install react react-dom --save

接着创建一个配置文件`webpack.config.js`

写上

```
module.exports = {
  entry: "./src/index.js",
  output: {
    path: "build",
    filename: "bundle.js"
  },
  devtool: "eval",
  module: {
    rules: [
      { test: /\.js$/, exclude: /node_modules/, use : "babel-loader" }
    ]
  }
};
```
然后敲命令

>npm run build

就会在项目中生成`build`文件夹，并且里面有一个`bundle.js`文件

在前面我们还创建了一个`.balbelrc`配置文件

在这个文件中我们敲

```
{
  "presets": ["env","react"]
}
```

此时我们就可以写`react`语法了

在写`react`语法之前我们先在`html`中引入`bundle.js`

此时我们就可以在`index.js`中写上`react`语法了，比如

```
import React from "react";
import ReactDOM from "react-dom";
function Hello(){

  return <div>
          <h1>hello</h1>
          <div>{a}</div>
        </div>;

}
let a = <h1>hello11111111s</h1>;
ReactDOM.render(
  <Hello />,document.getElementById("app")
)
```

代码中的两个`from`分别指向开始安装的`react`和`react-dom`包,接着我们就可以用`react`语法下的方法了

首先写一个`hello`函数,然后可以在函数里面写上`html`标签,标签里面放大括号的话，大括号里面可以放变量,

如同上面 `let`一个变量`a`,这个a可以写在函数的`<div>`标签中的大括号里面

最后，通过ReactDOM.render()方法,括号里面放

```
  <Hello />,document.getElementById("app")
```

显示

```
ReactDOM.render(
  <Hello />,document.getElementById("app")
)
```

`Hello`函数可以以结束标签的形式写在`.render`里面,当然可以写成`<hello></hello>`的形式

后面是逗号,第二个参数是document.getElementById("app"),这个是我们要寻找的`html`文件中id名为app的标签
