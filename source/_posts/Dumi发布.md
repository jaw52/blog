---
title: dumi
tags:
- dumi
- umi
- 文档系统
categories: 
- 前端
- umi
---

# Dumi发布

## 初始化项目（dumi忽略）

首先在创建好的项目文件夹下面执行

``` bash
npm init

```

根据对应提示完成`package.json`文件初始化

*   **package name** 为你创建的npm包的名称，在发布后被安装使用即该名字，npm规定包名首字母需要为小写。如`import App from 'your-module';`

*   **version** 即为包版本。语义化版本号分为三位`0.0.0`。**主版本号**：当进行了大都改动或者对api有很多不兼容修改时应该进行版本号升级。**次版本号**：增加了部分特性或者优化时升级该版本。**修订号**：当修改了项目bug或者小的改动时升级该版本。

*   **entry point** 项目的入口路径，当用户使用包的时候，会根据该入口也就是`package.json`的**main**中的路径来进行索引

*   **git repository** 关联的git仓库

*   **keywords** 会在npm中展示你的项目关键字

## Demo

![](img/image_gCzkz_rJtT.png)

我们需要发布的文件，在demo中的引入可以直接写成包名，duim会自动构建

## 设置忽略项

我们不需要把所有文件或目录提交到npm包，可以看到antd发布的包仅包含了其中几项

``` json
{
    "files": [
       "dist",
        "lib"
  ],
}
```

如上配置，就只有`dist`和`lib`目录会被发布出去，不过，有些文件是npm不会忽略的，有些文件是npm一定会忽略的

```
// 不会被npm忽略的文件
package.json
README (and its variants)
CHANGELOG (and its variants)
LICENSE / LICENCE

// 一定会忽略的
node_modules
.*.swp
._*
.DS_Store
.git
.hg
.npmrc
.lock-wscript
.svn
.wafpickle-*
config.gypi
CVS
npm-debug.log
```

## 设置推送源

新建`.npmrc`，设置推送到哪个npm源

``` bash
registry=http://localhost:4873/
```

## 发布

运行`npm publish`。对于`dumi`项目来说，会自动运行`prepublishOnly`指令进行构建（构建工具是`father`），构建的产物会推送到设置的npm源。

## 说明

发布之后，需要检查一下react版本与目标项目是否匹配，否则可能出现hook之类的冲突
