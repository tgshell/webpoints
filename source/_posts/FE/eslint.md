---
title: eslint 的玩法
date: 2021-02-03 10:00:00
categories:
- fe
tags:
- eslint
---

## 前言

eslint 想必大家都非常熟悉了，即代码规范检查，`Find and fix problems in your JavaScript code`，具有非常多的配置项，且支持自定义规则，是研发的好帮手。
东西确实是好东西，但配置太多同样又会很头疼，所以有些企业，或者框架的作者，或者爱折腾的开发又开源出来了很多规则包，让使用者拿去直接就行了，省去了折腾规则的过程。
然后就又出现了新问题，规则包太多了啊！该用哪个包？为什么要用这个包？所以多数情况下是靠搜索或者在某个包中摘抄了 eslint 配置，简化了头疼的过程。
痛定思痛，所幸花时间挖了一次 eslint 的基本玩法。

先来看一份示例的 eslint 配置文件：

```javascript
module.exports = {
  extends: [
    'airbnb-base',
    'plugin:@typescript-eslint/recommended',
  ],
  plugins: ['@typescript-eslint'],
  parserOptions: {
    parser: '@typescript-eslint/parser', // 指定 eslint-plugin-vue parser
    ecmaVersion: 2018,
    sourceType: 'module',
    extraFileExtensions: ['.vue'],
    ecmaFeatures: {
      jsx: true, // 支持 tsx
    },
  },
  env: {
    browser: true,
    es6: true,
    node: true,
  },
  globals: {
    window: true,
    history: true,
    Promise: true,
  },
  rules: {
    indent: ['error', 2],
    ...
  },
};
```

从上面的文件可以看出来，有 `extends`、`plugins`、`parserOptions`...`rules` 等等很多配置属性，配置属性又有对应的配置项，今天就来彻底搞懂这些配置的玩法及作用。

## 配置项

### extends

用来继承其他的规则包，如 `airbnb-base` = 继承了 `eslint-config-airbnb-base` 规则包的配置。
有两种写法：
```
extends: 'airbnb-base' // 只继承单个规则包
extends: ['airbnb-base', 'eslint:recommended'] // 继承多个规则包，需要注意顺序，后面的规则包会合并/覆盖前面规则包的同属性配置。
```

### plugins

用来自定义规则，引用官方的示例：

```javascript
module.exports = {
  rules: {
    'dollar-sign': {
      create: function (context) {
        // rule implementation ...
      },
    },
  },
};
```

这样就导出了一个名为 `dollar-sign` 的 `rule`。

详情可参见 [working-with-plugins](https://eslint.cn/docs/developer-guide/working-with-plugins)

### parserOptions

要支持的 JavaScript 语言选项配置。

示例：

```javascript
{
  parserOptions: {
    ecmaVersion: 6, // ECMAScript 版本
    sourceType: 'module', // ECMAScript 模块
    ecmaFeatures: { // 设置额外的语言特性
      jsx: true, // 启用 jsx
    },
  },
}
```

### env

预定义的全局变量。示例：

```javascript
{
  env: {
    browser: true,
    node: true,
  },
}
```

### globals

定义全局变量，避免撞上 `no-undef` 规则。示例：

```javascript
{
  globals: {
    Promise: true,
  },
}
```

### rules

示例：

```javascript
{
  rules: {
    'arrow-parens': ['error', 'as-needed'], // 箭头函数单个参数无括号
  },
}
```

## 如何收敛团队 eslint 规则？

### 第一步，给 eslint 包起个名

```
eslint-config-xxx
eslint-plugin-xxx
```

使用方可在 extends/plugins 中直接简写为：

```javascript
{
  extends: ['xxx'],
  plugins: ['yyy'],
}
```

详见：[Extending Configuration Files](https://eslint.org/docs/user-guide/configuring/configuration-files#extending-configuration-files)

### 第二步，填充基础/公共配置项，如最上面的示例配置

### 发布为 npm 包
