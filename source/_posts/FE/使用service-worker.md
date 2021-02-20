---
title: 使用 service-worker
date: 2019-12-16 14:23:31
tags:
---

## 注意事项

- 默认必须运行在 https 协议下，为方便开发，也允许 http://127.0.0.1/ http://localhost/ 下运行

## 安装与激活

- 用户首次访问 service worker 控制的网站或页面时，service worker 会立刻被下载
- 首次安装并激活后，下次安装会发生在 service worker 文件代码改动或者24小时后，但会在没有页面依赖旧的service worker 时激活

## 参考

- [MDN 使用 Service Workers](https://developer.mozilla.org/zh-CN/docs/Web/API/Service_Worker_API/Using_Service_Workers)
