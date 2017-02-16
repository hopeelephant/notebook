---
title: Github Pages 创建个人网站
layout: default
---


# nodejs 安装

nodejs 的模块分为 3 类，核心模块，第三方模块，以及自定义的模块


```
// 通过 module.exports 导出模块，require 导入模块。

// 导入核心模块p
var fs = require('fs')

// 导入第三方模块
var $ = require('jquery')

// 导入自定义的模块
var test = require('./test')

// 导出模块
module.exports.test = 'test';
```

我们的前端开发会用到 es6 的模块，需要用 webpack 来打包我们的代码。

```
/ 创建项目文件夹
mkdir webpack-demo && cd webpack-demo
// 初始化项目
npm init -y
// 安装 webpack
npm i -D webpack
// 编写我们的 npm 脚本，使用项目内的 webpack
"scripts": {
  "build": "./node_modules/.bin/webpack"
}
// 增加 webpack 的配置文件 webpack.config.js
module.exports = {
  entry: './index.js',
  output: {
    filename: 'bundle.js'
  }
}
```

npm install webpack 装包的时候会生成node_modules文件,包名在这个文件夹里面；
npm install webpack --save-dev或者npm install webpack -D将下载的包保存在package.json中

npm init会生成package.json来记录装的包名;

webpack是一个打包的工具，例如我们在项目中先写一个`demo.js`,这个是用来导出代码的，看代码

```
function a(x,y){
  return x+y
}
module.exports = a;

```
导出了a这个函数;

接着我们在来建一个`index.js`,这个是用来导入代码的,看代码

```
var a = require("./demo");
console.log(a(5,10));
```

接着在命令行中输入`node index.js`

就可以打印出结果，但是在浏览器中会出错误，。这个时候我们就得在命令行中再生成一个js文件，。

在命令行中敲

```
./node_modules/.bin/webpack index.js bundle.js
```
这样在项目中就生成了bundle.js,现在在html中引用  

```
<script src="bundle.js"></script>
```
这样就可以在浏览器中打印出结果了，。

下面说一下生成bundle.js的目的,在做webpack项目的时候我们可能会导入和导出很多的js,但是这些js无法直接被浏览器识别，

我们就需要把这些js给打包起来，这个时候我们就生成`bundle.js`,这样在html中引入`bundle.js`,就可以被浏览器识别了

在来看一下`package.json`,在这个文件中有一个可以让我们偷懒的东西，这个东西就是

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "./node_modules/.bin/webpack index.js bundle.js -p"
  }
```
我在scripts的里面添加了

```
"build": "./node_modules/.bin/webpack index.js bundle.js -p"
```

在没有添加这行代码的时候，那么每一次我们推送我们新打包的js,和修改js，我们都需要在命令行中敲

`./node_modules/.bin/webpack index.js bundle.js`

但是添加了之后就只需要直接npm run buildz就可以了

另外我们还可以在里面放入别的快捷功能

比如我们可以在`scripts`里面添加一个

```
"push":"git add -A && git commit -m'111' && git push"
```

这样在推送代码的时候就可以直接用`npm run push`进行偷懒了

另外我们在

```
"build": "./node_modules/.bin/webpack index.js bundle.js -p"
```

后面的`-p`的作用是让bundle.js压缩，另外还可以加上`-watch`,它是实时监听的意思，。等等，-d就是在检查代码的时候显示源代码在

编辑器中的行数

###  配置文件

在项目上创建`webpack.config.js`文件，这个的作用是来存放webpack打包的一些配置信息

在配置信息中显示的代码

```
module.exports = {
  entry: "./index.js",
  output: {
    path: "build",
    filename: "bundle.js"
  }
};
```

添加了配置信息后，我们就样将`"build": "./node_modules/.bin/webpack index.js bundle.js -p"`中的

`index.js bundle.js -p`给删除掉，只保留`"build": "./node_modules/.bin/webpack"`就可以。
