---
title: VSCODE 前端开发格式化配置
date: 2019-08-30 16:56:21
categories: 
- 前端
tags:
- vscode
- prettier
- eslint
- vue
---

## 正文之前

作为开发，总是对代码风格有较高的追求，那就需要趁手的工具，这里介绍一下基于 VSCode 的代码风格管理插件。

> 文中插件及配置均基于 VSCODE，不作赘述。

## 基础配置

```
"editor.tabSize": 2,
"editor.wordWrap": "on"
```

## 使用 Prettier 进行格式化

作为前端开发，而且有工程需要团队协作开发的时候，代码格式化一直是个复杂的问题。之前也使用过的 Beautify 等插件，但是效果也不太理想，而 Prettier 的出现基本解决了此问题，详细配置如下：

```
"[html]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[javascript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[json]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[jsonc]": {
  "editor.defaultFormatter": "vscode.json-language-features"
},
"[typescript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

上面配置完成后，格式化 javascript 代码时会发现默认是双引号，所以修改引号规则为单引号
```
"prettier.singleQuote": true
```

## 使用 Eslint 检测代码风格

有了代码格式化，日常开发还可以配合代码风格实时检测工具，会使得开发效率和代码质量有显著提升。所以再贴下 eslint 的配置。

```
// "eslint.autoFixOnSave": true, // 全局自动修复配置
// eslint 实时检查语言列表
"eslint.validate": [
  "javascript",
  "javascriptreact",
  {
    "language": "vue",
    // "autoFix": true // 针对语言的自动修复配置
  },
  "typescript",
  "typescriptreact",
  "html"
],
// "eslint.alwaysShowStatus": true,
```

### 对 Vue 格式化

以上为基本配置，笔者目前使用的框架是 Vue，再贴下对应的配置。

```
"[vue]": {
  "editor.defaultFormatter": "octref.vetur"
},
// ---------- vetur ----------
"vetur.format.defaultFormatter.html": "prettyhtml",
"vetur.format.defaultFormatter.css": "prettier",
"vetur.format.defaultFormatter.postcss": "prettier",
"vetur.format.defaultFormatter.scss": "prettier",
"vetur.format.defaultFormatter.less": "prettier",
"vetur.format.defaultFormatter.stylus": "stylus-supremacy",
"vetur.format.defaultFormatter.js": "prettier",
"vetur.format.defaultFormatter.ts": "prettier",
"vetur.format.defaultFormatterOptions": {
  "js-beautify-html": {
    "wrap_attributes": "preserve-aligned"
  },
  "prettyhtml": {
    "singleQuote": false,
    "sortAttributes": false,
  },
  "prettier": {
    "singleQuote": true,
    "printWidth": 200
  }
}
```
