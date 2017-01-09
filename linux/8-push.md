---
title: Github Pages 创建个人网站
layout: default
---


# 上传代码到 Github.com

前面学会了如何在本地用 git 创建项目版本，本节咱们看看咋把新版本上传到 github.com 之上。

### 准备工作：删除第一天创建的项目

如何删除一个 github.com 的仓库呢？

首先到仓库页面：https://github.com/hopeelephant/hopeelephant.github.io

点 Settings（设置）这一个标签。打开的页面底部有一个 “Delete this repository” 按钮，意思是”删除这个仓库“，点击按钮。打开的界面中，输入一下这个仓库的名字 hopeelephant.github.io 就可以把这个仓库删除了。

删除仓库之后，我们要做的事情是：

>如何把本地的已有仓库，上传到 github.com

### 第一步：创建本地项目

项目名称是任意的，但是我们这里想做的事情是上传比较，所以，本地这个仓库名，也必须是：

```
mkdir hopeelephant.github.io
```

本地项目名要和 github.com 我们一会儿要创建的仓库名保持一致。

然后，我们就可以把我们想要上传的内容拷贝到这个文件夹内，并制作本地版本。

拷贝进来的内容，要符合第一天我们介绍的 github pages 的格式规范（其实最重要的一点就是每个 .md 文件中都要有头部，参考第一天我们的文档中的介绍）。

### 第二步：创建 github.com 上的同名仓库

到 github.com 上点 `New repository` 按钮，新建一个项目， 项目名叫做 `happypeter.github.io` 。

>注意，不要勾选任何选项，尤其是不能默认创建 README.md 文件。

创建完成之后，页面上有两个选择，其中第二个是

```
or push an existing repository from the command line
```

翻译：或者把一个已经存在的仓库从命令行推送上来

我们当前就属于这个情况。上传方式有两种 HTTPS 和 SSH ，我们推荐的方式是 SSH，点一下页面上 SSH 字样的按钮。

接下来就按照页面上显示的两步来走。

### 尝试推送 push

到本地命令行，进入我们的本地项目文件夹

```
cd hopeelephant.github.io
```

然后执行下面两步：

```
git remote add origin git@github.com:funnydeer/funnydeer.github.io.git
git push -u origin master
```

如上所示：

```
git@github.com:funnydeer/funnydeer.github.io.git
```

这个是远端仓库地址。第一个命令本身的意思是把远端仓库地址记录到本地仓库中。

下一步 `git push -u origin master` 就是真正进行上传代码的工作了。

但是执行结果是：

```
Please make sure you have the correct access rights
```

执行失败，解决方法就是添加 ssh 公钥到 github.com 。


### 第三步：添加 ssh key
