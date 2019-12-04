## 初始结构

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

## theme

git clone https://github.com/theme-next/hexo-theme-next themes/next

## dev

```
$ hexo clean //清除静态页面缓存（清除 public 文件夹)         
$ hexo g     //在本地生成静态页面（生成 public 文件夹）        
$ hexo s     //启动本地服务 http://localhost:4000，进行预览调试           
$ hexo d     //远程部署，同步到 GitHub         

$ npm install hexo-deployer-git --save    //自动部署
$ hexo clean && hexo g && hexo d          //发布
```

## publish

```
sh publish.sh
```

## git repo

源代码存放在 doc-src 分支
发布至 master 分支

## git commit formatter

### git commit message

- feat：新功能（feature）
- fix：修补 bug
- docs：文档（documentation）
- style：格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改 bug 的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

### changelog

- Feature
- Bug Fix
- Breaking Changes
