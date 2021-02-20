---
title: Vue原理
date: 2020-12-28 10:10:00
categories: 
- fe
tags:
- vue
---

## 概念

### 对 Array 的特殊处理

表现：改变数组的索引，不会触发视图更新，可使用 `Vue.set(vm.items, indexOfItem, newValue);` 达到触发视图更新的效果

原因：Vue 没有使用 `Object.defineProperty` 去监听数组索引的变化，因为作者认为性能消耗太大，于是在性能和用户体验之间做了取舍

实现：拦截数组的原型中7个能够改变数组自身的几个方法，重写的方法中会手动触发通知该数组的所有依赖进行更新

### Dep

订阅管理

### Observer

1. 遍历 data 下的每一个属性，若是对象，则执行 new Observer(), 在对象上新增 __ob__ 属性,该属性的值为 Observer 的实例
2. 劫持对象属性的变化，在 getter 的时候，拿到 Observer 实例的dep实例，执行 dep.depend()

### Watcher

实例化 Watcher 时,会执行 Dep.target = this，然后执行 this.vm[exp], 也就是取一次值，那么会触发 getter,将自身（Watcher实例）添加到 dep 的订阅者数组内

### compile

模板解析是 Vue 模板编译的第一步，即通过模板得到 AST（抽象语法树 abstract syntax tree）
