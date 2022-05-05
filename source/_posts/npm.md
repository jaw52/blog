---
title: npm
tags:
- npm
categories: 
- 前端
- npm
---
# npm
```bash
  //npm查看包的最新版本
  npm view <packagename> versions --json
  //指定版本安装
  npm install <packagename>@3.21.2
```

### npm install安装固定版本号以及package.json中版本号详解

在npm中安装固定的版本号package，只需要在其后加 ‘@版本号’

```bash
  npm install three@0.102.1
```

Node.js中package.json中库的版本号详解：

1.  \~ 匹配最近的小版本依赖包，比如\~1.2.3会匹配所有1.2.x版本，但是不包括1.3.0

2.  ^ 匹配最新的大版本依赖包，比如^1.2.3会匹配所有1.x.x的包，包括1.3.0，但是不包括2.0.0

3.  \* 意味着安装最新版本的依赖包

npm i的时候实际是执行以上规则，并不是直接安装有1.2.3，而是按具体符号匹配，有更新则更新。

# nvm指令

```bash
  nvm install stable   //安装最新稳定版 node
  nvm install <version> //安装指定版本，可模糊安装，如：安装v4.0.0，可nvm install v4.0.0 或者 nvm install 4.4
  nvm uninstall <version>       //删除已安装的指定版本，语法与install类似
  nvm use <version>           //切换使用指定的版本node
  nvm alias default <version>  //可以指定默认打开终端时的node版本
  nvm ls                             //列出所有安装的版本
  nvm ls-remote             //列出所有远程服务器的版本（官方node version list）
  nvm current      //显示当前的版本
  nvm alias <name> <version>        //给不同的版本号添加别名
  nvm unalias <name>     //删除已定义的别名
  nvm reinstall-packages <version>   //在当前版本 node 环境下，重新全局安装指定版本号的 npm 包

```
