---
title: vue + typescript + lerna + webpack
date: 2019-12-27 12:00:00
categories: 
- Javascript
tags:
- vue
- typescript
- lerna
- eslint
- webpack4
- monorepo
---

## 写在前面

由于前端语言发展形势的影响，近期启动对基于 vue 的 monorepo 工程集成 typescript。涉及的语言及插件如下：

## vue

`vue` 从 `2.5x` 已经开始对 `typescript` 进行支持。本文是基于 `vue 2.6.10` 版本进行的升级动作。<br/>
现在 `vue` 已经发布了 3.0 版本源码，即 `vue-next`，可以查看[尤雨溪的宣讲]()即，有兴趣也可以到 `github` `star` 一下。地址：[`vue-next(3.0)`](https://github.com/vuejs/vue-next)。

## typescript

官方定义：JavaScript的超集。文档地址：
[英文官网](http://www.typescriptlang.org/)，[中文网](https://www.tslang.cn/docs/home.html)

### lerna

组件库使用 `lerna` 进行管理，[`点击前往 lerna 官网`](https://github.com/lerna/lerna)。

### 代码规范

使用 [`eslint`](http://eslint.cn/docs/user-guide/configuring) + [`prettier`](https://prettier.io/docs/en/options.html)

> tslint 已经官方宣布2019年停止维护，转向 eslint。

### 编译

使用 [`webpack4`](https://www.webpackjs.com/concepts/) 作为运行测试及打包工具。

## 配置

在 typescript 2.7 版本，属性定义需要指定 !:
```
@Prop({ default: false }) isGetBackPwdDisable!: boolean;
```
若不指定，编辑器会提示
```
Property 'isGetBackPwdDisable' has no initializer and is not definitely assigned in the constructor.
```
查看官方释义 [`Definite Assignment Assertions`](http://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-7.html#definite-assignment-assertions)，也可以通过以下配置方式解决
```
"strictPropertyInitialization": false
```
