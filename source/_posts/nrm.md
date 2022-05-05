---
title: nrm
banner_img: /img/banner_img.png
tags:
- npm
categories: 
- 前端
- npm
---

# nrm

## nrm管理npm源

一般在本地会安装多个npm源，可以使用nrm对其进行管理与切换。

相当于

```bash 
npm set registry [url]
```

### 安装

```bash
npm install nrm -g
```

### 增加本地npm源

```bash
nrm add <名称> <地址>
```

### 删除npm源

```bash
nrm del <名称> <地址>
```

### 查看是否添加成功

```bash
nrm ls

// 源列表

- npm -------- [https://registry.npmjs.org/](https://registry.npmjs.org/)

    yarn ------- [https://registry.yarnpkg.com/](https://registry.yarnpkg.com/)

    cnpm ------- [http://r.cnpmjs.org/](http://r.cnpmjs.org/)

    taobao ----- [https://registry.npm.taobao.org/](https://registry.npm.taobao.org/)

    nj --------- [https://registry.nodejitsu.com/](https://registry.nodejitsu.com/)

    npmMirror -- [https://skimdb.npmjs.com/registry/](https://skimdb.npmjs.com/registry/)

    edunpm ----- [http://registry.enpmjs.org/](http://registry.enpmjs.org/)

    localnpm --- http://*.*.*.*:4873/
```

### 切换至本地源

```bash
nrm use <名称>

// 源列表

  npm -------- [https://registry.npmjs.org/](https://registry.npmjs.org/)

  yarn ------- [https://registry.yarnpkg.com/](https://registry.yarnpkg.com/)

  cnpm ------- [http://r.cnpmjs.org/](http://r.cnpmjs.org/)

  taobao ----- [https://registry.npm.taobao.org/](https://registry.npm.taobao.org/)

  nj --------- [https://registry.nodejitsu.com/](https://registry.nodejitsu.com/)

  npmMirror -- [https://skimdb.npmjs.com/registry/](https://skimdb.npmjs.com/registry/)

  edunpm ----- [http://registry.enpmjs.org/](http://registry.enpmjs.org/)

- localnpm --- http://*.*.*.*:4873/
```
