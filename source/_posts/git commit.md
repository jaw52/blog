---
title: git commit
tags:
- git
- 工程化
categories: 
- 前端
---

给大家介绍下如何保障项目 `commit message` 的规范和格式化

<!-- more -->

#  格式

目前规范使用较多的是 [Angular 团队的规范](https://link.juejin.cn/?target=https%3A%2F%2Flink.zhihu.com%2F%3Ftarget%3Dhttps%3A%2F%2Fgithub.com%2Fangular%2Fangular.js%2Fblob%2Fmaster%2FDEVELOPERS.md%23-git-commit-guidelines), 继而衍生了 [Conventional Commits specification](https://link.juejin.cn/?target=https%3A%2F%2Flink.zhihu.com%2F%3Ftarget%3Dhttps%3A%2F%2Fconventionalcommits.org%2F). 它的 message 格式如下:

```bash
<type>(<scope>): <subject>
# 空行
<BLANK LINE>
<body>
# 空行
<BLANK LINE>
<footer>
```
占位标签解析：

- `type`：代表某次提交的类型，比如是修复一个bug还是增加一个新的feature。
- `scope`：commit影响的范围。scope依据项目而定，例如在业务项目中可以依据菜单或者功能模块划分，如果是组件库开发，则可以依据组件划分。如果一次commit修改多个模块，建议拆分成多次commit，以便更好追踪和维护
- `subject`：是commit的简短描述
- `body`：填写详细描述，主要描述改动之前的情况及修改动机，对于小的修改不作要求，但是重大需求、更新等必须添加body来作说明
- `footer`：如果代码的提交是不兼容变更或关闭缺陷，则Footer必需，否则可以省略。

所有的type类型如下：
-  feat[特性]:新增feature 
-  fix[修复]: 修复bug     
-  docs[文档]: 仅仅修改了文档，比如README, CHANGELOG, CONTRIBUTE等等
-  style[格式]: 仅仅修改了空格、格式缩进、都好等等，不改变代码逻辑
-  refactor[重构]: 代码重构，没有加新功能或者修复bug
-  perf[优化]: 优化相关，比如提升性能、体验
-  test[测试]: 测试用例，包括单元测试、集成测试等
-  chore[工具]: 改变构建流程、或者增加依赖库、工具等
-  revert[回滚]: 回滚到上一个版本

# 格式化工具

### Commitizen

`commitizen/cz-cli`, 我们需要借助它提供的 git cz 命令替代我们的 git commit 命令, 帮助我们生成符合规范的 commit message.

####  安装

首先，全局安装

```bash 
npm install -g commitizen
```

package.json中配置:

其中需要注意的是需要先手动`git add`更改文件，否则直接运行`git cz`会提示没有效果的

```json
"script": {
    "commit":"git add . && git cz",
},
"config": {
    "commitizen": {
    	"path": "cz-conventional-changelog"
    }
},
```

在对应的项目中执行 `git cz` or` npm run commit`

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/5/16/16369a14ec8704fc~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

根据提示依次填写

```bash
1.Select the type of change that you're committing 选择改动类型 (<type>)

2.What is the scope of this change (e.g. component or file name)? 填写改动范围 (<scope>)

3.Write a short, imperative tense description of the change: 写一个精简的描述 (<subject>)

4.Provide a longer description of the change: (press enter to skip) 对于改动写一段长描述 (<body>)

5.Are there any breaking changes? (y/n) 是破坏性修改吗？默认n (<footer>)

6.Does this change affect any openreve issues? (y/n) 改动修复了哪个问题？默认n (<footer>)

```

### webstorm

webstorm本身就集成了一个图形化的git提交系统，为了方便我们可以下载一个`Git Commit Template`的插件，可以帮助我们提交格式化的信息

# 校验你的 message

`commitlint`: 可以帮助我们 lint commit messages, 如果我们提交的不符合指向的规范, 直接拒绝提交

### 安装

```bash
npm i -D @commitlint/config-conventional @commitlint/cli
```

### 快速开始

同时需要在项目目录下创建配置文件 `.commitlintrc.js`, 写入:

```js
module.exports = {
  extends: [
    '@commitlint/config-conventional'
  ]
};

```
在`gitHooks`增加配置，提交时便可检查提交信息

```json
//package.json
"gitHooks": {
	"commit-msg": "commitlint -e $GIT_PARAMS"
},
```

### 自定义Type

以上会启用推荐配置，针对于前端项目，`type`可能不够，需要另外扩展

```js
module.exports = {
  rules: {
		'type-enum': [
			2,
			'always',
			[
				'build',
				'chore',
				'ci',
				'docs',
				'feat',
				'fix',
				'perf',
				'refactor',
				'revert',
				'style',
				'test',
			],
		],
	},
};
```

#### type-enum

- **condition**: 0为`disable`，1为`warning`，2为`error`

- **rule**:应用与否，可选`always`|`never`

# 自动生成 CHANGELOG

通过以上工具的帮助, 我们的工程 commit message 应该是符合 Angular团队那套, 这样也便于我们借助 `standard-version` 这样的工具, 自动生成 `CHANGELOG`, 甚至是 语义化的版本号(Semantic Version).

### 安装

```bash
npm i -D standard-version
```

package.json 配置，会按默认升级版本号更新`version`

```json
"scirpt": {
    "release": "standard-version"
}	
```

### 强制打一个静态版本号

```bash
"scripts": {
	"release-static": "standard-version --release-as 3.3.3",
}
```

### 第一个版本

```bash
npm run release -- --first-release
```

### 配置哪些commit消息写入changelog

默认情况下，*`standard-version`* 只会在 *CHANGELOG.md* 中记录 `feat` 和 `fix` 类型的提交。如果想记录其他类型的提交，需要如下步骤

根目录下创建一个名为 `.versionrc.js` 的文件

```js
module.exports = {
    "types": [
      { "type": "feat", "section": "✨ Features | 新功能" },
      { "type": "fix", "section": "🐛 Bug Fixes | Bug 修复" },
      { "type": "init", "section": "🎉 Init | 初始化", "hidden": true  },
      { "type": "docs", "section": "✏️ Documentation | 文档" },
      { "type": "style", "section": "💄 Styles | 风格" },
      { "type": "refactor", "section": "♻️ Code Refactoring | 代码重构" },
      { "type": "perf", "section": "⚡ Performance Improvements | 性能优化" },
      { "type": "test", "section": "✅ Tests | 测试", "hidden": true  },
      { "type": "revert", "section": "⏪ Revert | 回退", "hidden": true },
      { "type": "build", "section": "📦‍ Build System | 打包构建", "hidden": true  },
      { "type": "chore", "section": "🚀 Chore | 构建/工程依赖/工具", "hidden": true  },
      { "type": "ci", "section": "👷 Continuous Integration | CI 配置", "hidden": true  }
    ]
  }
```

- `"type"` commit 类型
- `"section"` 不同的 commit 类型所在 *CHANGELOG.md* 中的区域
- `"hidden"` 是否在 *CHANGELOG.md* 中显示
