---
title: 安装react
layout: default
---

# es6新的语法

es6的出现大大的减少了代码的数量；

### 箭头函数

es5

```
var selected = all.filter(function (data) {
      return data.isSelected();
    });
```

es6

```
 var selected = all.filter(data => data.isSelected());
```

仔细看一下，在es6语法中我们省略了`function` `{}` `return` ,极大的简便了代码的摄入量，箭头前面的代码的`data`代表的是函数的参数，一个参数可以

不要打上`()`,也可以打上`()`,但是多个参数就需要打上`()`了,如果是匿名函数的话直接打上`()`就可以了

  
