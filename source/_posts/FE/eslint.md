---
title: 深入 eslint
date: 2021-02-03 10:00:00
categories:

- fe
tags:
- eslint
- typescript
- vue
---

## 前言

eslint 想必大家都非常熟悉了，即代码规范检查，`Find and fix problems in your JavaScript code`，具有非常多的配置项，且支持自定义规则，是研发的好帮手。
东西确实是好东西，但配置太多同样又会很头疼，所以有些企业，或者框架的作者，或者爱折腾的开发又开源出来了很多规则包，让使用者拿去直接就行了，省去了折腾规则的过程。
然后就又出现了新问题，规则包太多了啊！该用哪个包？为什么要用这个包？所以多数情况下是靠搜索或者在某个包中摘抄了 eslint 配置，简化了头疼的过程。
所以痛定思痛，花时间挖了一次 eslint

先来看一份示例的 eslint 配置文件：

```javascript
module.exports = {
  parser: '@typescript-eslint/parser',
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

## 如何收敛团队 eslint 规则？

tl、基建同学往往会有疑问，日常团队开发，eslint 支持 extends，

### 第一步，给 eslint 包起个名

eslint 支持 extends，

eslint 官方约束命名规则：

```
eslint-config-xxx
eslint-plugin-xxx
```

可在 extends/plugins 中直接简写为：

```javascript
{
  extends: ['xxx'],
  plugins: ['yyy'],
}
```

详见：[Extending Configuration Files](https://eslint.org/docs/user-guide/configuring/configuration-files#extending-configuration-files)
