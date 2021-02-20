---
title: fe-points
date: 2020-11-09 09:27:26
categories: 
- fe
tags:
- html5
- js
- css
- node.js
---

## html

## javascript

### 概念

#### mvvm

MVVM 模式，即 Model-View-ViewModel 模式，本质上是 MVC 的改进版。最早的 MVVM 框架：knockout。

**重点：双向绑定(data-binding)**

**React(单向数据流) 和 Vue(VM) 都不是纯正的 MVVM。但是完整的项目中，React、Vue 可以理解为 MVVM 模型**

简述：
- Model: 域模型，用于持久化
- View: 作为视图模板存在
- ViewModel: 作为视图的模型，为视图服务

详细说明：
- Model 层，对应数据层的域模型，它主要做域模型的同步。通过 Ajax/fetch 等 API 完成客户端和服务端业务 Model 的同步。在层间关系里，它主要用于抽象出 ViewModel 中视图的 Model。
- View 层，作为视图模板存在，在 MVVM 里，整个 View 是一个动态模板。除了定义结构、布局外，它展示的是 ViewModel 层的数据和状态。View 层不负责处理状态，View 层做的是 数据绑定的声明、 指令的声明、 事件绑定的声明。
- ViewModel 层把 View 需要的层数据暴露，并对 View 层的 数据绑定声明、 指令声明、 事件绑定声明 负责，也就是处理 View 层的具体业务逻辑。ViewModel 底层会做好绑定属性的监听。当 ViewModel 中数据变化，View 层会得到更新；而当 View 中声明了数据的双向绑定（通常是表单元素），框架也会监听 View 层（表单）值的变化。一旦值变化，View 层绑定的 ViewModel 中的数据也会得到自动更新。

一句话总结 Web 前端 MVVM：操作数据，就是操作视图，就是操作 DOM（所以无须操作 DOM ）。

开发者在 View 层的视图模板中声明数据绑定、事件绑定 后，在 ViewModel 中进行业务逻辑的数据处理。事件触发后，ViewModel 中数据变更， View 层自动更新。因为 MVVM 框架的引入，开发者只需关注业务逻辑、完成数据抽象、聚焦数据，MVVM 的视图引擎会帮你搞定 View。因为数据驱动，一切变得更加简单。

#### module.exports vs export

| | node.js | es6 |
| --- | --- | --- |
| 使用方法 | module.exports | export |
| 加载机制 | 同步运行时 | 异步、编译时 |
| 适用场景 | 服务端 | 浏览器、服务端 |

| | AMD | CMD | UMD |
| --- | --- | --- | --- |
| 全称 | Asynchronous Module Definition | Common Module Definition | Universal Module Definition |
| 代表 | RequireJS | SeaJS | |
| 加载机制 | 异步、前置 | 异步、就近 | 集合 AMD & CMD |
| 适用场景 | 浏览器 | 浏览器 | 浏览器、服务端 |

参考：
- [还傻傻分不清 module.exports 和 export default 吗？](https://juejin.im/post/6844903955282165773)

#### event loop

#### promise 原理

[es6 promise源码实现](https://segmentfault.com/a/1190000006103601)

三种状态：
- pending
- fulfilled
- reject

#### call apply bind 的区别

```javascript
call(this, p1, p2, p3);
apply(this, [p1, p2, p3]);
const fn = bind(this, p1, p2, p3);
fn();
```

### 技能

#### 地理位置

```
navigator.geolocation.getCurrentPosition(callback)
```

### 算法、技巧

#### array 去重

## css

## node.js

### generator 实现原理

[generator（生成器）原理、使用及常见问题集锦](https://blog.csdn.net/juse__we/article/details/88912300)

### koa

### egg.js

[结合源码解密 egg 运行原理](https://zhuanlan.zhihu.com/p/29102746?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)

## 框架

## vue

### 原理、生命周期、vuex

### 双向绑定

- 数据劫持：Object.defineProperty
- 发布者-订阅者模式：属性发生变化，通知订阅者 Watcher 检测否需要更新

监听器 Observer：对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者

订阅者 Watcher：对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数

解析器 Compile：作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图

### watch 原理

### Array 的处理

## react

### 原理、生命周期、redux
