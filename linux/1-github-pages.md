---
title: Github Pages 创建个人网站
layout: default
---


# Github Pages 创建个人网站
Github.com 是程序员存放代码的一个网站。Github Pages 是 Github 提供的一项服务
可以免费的帮助我们托管网站。




### 注册 Github 账号

点 github.com 首页的 Sign Up （注册）按钮，进行注册。

填写 username （用户名），小写英文字母，不要用空格。

Email 这一项，必须填写真实有效的邮箱，不然注册不了

Choose your personal Plan ? 选择你的付费方案


  -   免费版：无限使用权限，只能发布开源项目

  -   收费版：允许发布闭源项目


邮箱中点链接之后，就可以自动跳转回 github.com 的页面上，同时显示

> Your email was verified.

你的邮箱已经验证成功了。下一步就可以来创建项目了。

repository （仓库）这个词基本上等价于 project ，差别如下：

```bash
repository = project + history
```

### 搭建 Github 网站

创建一个仓库，仓库的名字是有严格规定的，

> username.github.io

把 username 替换成自己的自己的用户名。例如我叫 happypeter ，我要创建的仓库名就是

> hopeelephant.github.io

Description (optional) 项目描述（可选项）

- Public: 开源项目

- Private：闭源项目

- Initialize this repository with a README 初始化项目的时候，自动添加一个 README 文件

我们这里勾选上这一项。

到达项目页面后，现在来创建一个 index.html ，点 “Create A New File”

添加一些基本的 html 内容进 index.html ，然后点 “Commit New File” 进行保存。

```
注意：新添加的内容，不一定立刻能显示到 hopeelephant.github.io ，可能会有五六分钟的延迟。
```

### 用 Markdown 来记笔记

Markdown 跟 HTML 一样，是一种标签语言。但是 Markdown 语法特别简单，适合用来做笔记。

- [Markdown 语法参考](https://coding.net/help/doc/project/markdown.html)

Mardown 语法不是浏览器能直接支持的，所以需要先把 Mardown 语法写成的内容，编译成 HTML ，才能美观的显示出来。

那么 Github 就提供了这个编译环境。到 Github 上我们的项目中，有一个文件叫 README.md 这里 md 就是 markdown 的缩写。

在这个文件里面，我们去写 markdown ，就可以翻译成 html

例如，我们在 README.md 中填写

>\[百度](http://baidu.com)
>`<a href="http://baidu.com">百度</a>`

`<h1>我爱你<h1>`
