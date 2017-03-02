---
title: 安装react
layout: default
---

### localhost:8080

如何实现手机和电脑在同一无线网的情况下在｀localhost:8080｀上都可以访问

先说一下这样做的好处，以后我们修改了代码之后保存下来就可以直接实现自动刷新，这样在调试的时候就大量的节约了时间

和以往的项目不同的是，以往的项目只有一个配置文件`webpack.config.js`，现在我们来新增加一个配置文件，取名叫做

`webpack.dev.config.js`,哪两个配置文件有什么不同的，有小小的不同，新的配置文件中`output`中的`path`和｀publicPath｀

中的值必须得用两个`/`给包起来

接着我们得安装一个包，包名叫做`webpack.dev.server`另外在 `package.json`文件中加入

```
"dev": "./node_modules/.bin/webpack-dev-server --config webpack.dev.config.js"
```

这样就可以通过执行｀npm run dev｀实现自动刷新了


### ifconfig

ifconfig查看电脑ip，服务器ip,回环网络ip

### 组件生命周期

react的生命周期是个比较复杂的问题，且听我一一到来

1 初始化

```
constructor
componentWillMount
render
componentDidMount
```
首次实例化我们回执行５步，那就是

- `getDefaultProps` 获取默认`props`属性

- `getInitialState` 获取初始`state`值

- `componentWillMount`　首次将要更新

- `render`    渲染

- `componentDidMount`　首次更新完毕

2 存在期

 组件存在时的状态改变

- componentWillReceiveProps

- shouldComponentUpdate

- componentWillUpdate

- render

3 销毁

- componentWillUnmount 最直接的好处就是将用完或者不想要的东西删除掉，是直接在DOM节点中删除
