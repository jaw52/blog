---
title: package.json
tags:
- package.json
- npm
- yarn
categories: 
- 前端
- npm
---

# package.json

## main字段

`main`字段指定了加载的入口文件，`require`导入的时候就会加载这个文件。这个字段的默认值是模块根目录下面的`index.js`

## repository字段

指定一个代码存放地址，对想要为你的项目贡献代码的人有帮助

```json
"repository" : {
  "type" : "git", 
  "url" : "https://github.com/npm/npm.git"
}

```

## dependencies字段, devDependencies字段

`dependencies`字段指定了项目运行所依赖的模块，`devDependencies`指定项目开发所需要的模块

版本说明

固定版本: 比如`5.38.1`，安装时只安装指定版本

波浪号: 比如`~5.38.1`, 表示安装5.38.x的最新版本

插入号: 比如`ˆ5.38.1`, ，表示安装5.x.x的最新版本

latest: 安装最新版本

## private字段

如果这个属性被设置为`true`，`npm`将拒绝发布它，这是为了防止一个私有模块被无意间发布出去。

```json
"private": true
```

## publishConfig字段

用于设置发布用到的一些值的集合

通常`publishConfig`会配合`private`来使用，如果你只想让模块被发布到一个特定的`npm`仓库，如一个内部的仓库

```json
"private": true,
"publishConfig": {
  "tag": "1.0.0",
  "registry": "https://registry.npmjs.org/",
  "access": "public"
}
```

## peerDependencies

`peerDependencies`的目的是提示宿主环境去安装满足插件`peerDependencies`所指定依赖的包，然后在插件`import`所依赖的包的时候，永远都是引用宿主环境统一安装的npm包，最终解决插件与所依赖包不一致的问题
