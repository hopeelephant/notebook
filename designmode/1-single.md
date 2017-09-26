---
title: javascript设计模式之单例模式
layout: default
---

# 单例模式

### 概念解读

单例模式就是保证一个类只有一个实例，实现的方式是先判断实例是否存在，如果存在就直接返回，如果不存在就创建了在返回，这就确保了一个类只有一个实例对象，在js中,单例作为一个命名空间提供者，从全局命名空间里面提供一个唯一的访问点来访问该对象

### 作用和注意事项

作用
- 模块间通信
- 系统中某个对象的类只能存在一个
- 保护自己的属性和方法

注意事项
- 注意this的使用
- 闭包容易造成内存泄露，不需要的赶快抛弃
- 注意少使用new（继承）

### 代码实战和总结