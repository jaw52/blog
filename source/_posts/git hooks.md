---
title: git Hooks
tags:
- git
- 工程化
categories: 
- 前端

---

`git hooks`是一些自定义的脚本，对提交的代码和message进行检查，是否符合定义的规范

<!-- more -->

# 客户端钩子

#### pre-commit（常用）

在键入提交信息前运行

#### commit-msg（常用）

因此，可以用来在提交通过前验证项目状态或提交信息

# husky

Husky可以将git内置的钩子暴露出来，很方便地进行钩子命令注入，而不需要在.git/hooks目录下自己写shell脚本了。您可以使用它来lint您的提交消息、运行测试、lint代码等。当你`commit`或`push`的时候。husky触发所有git钩子脚本。

# yorkie

fork自husky

## 使用

安装 yorkie，它会让你在 `package.jso`n 的` gitHooks` 字段中方便地指定 Git hook：

```json
"gitHooks": {
    "pre-commit": "lint-staged",
    "commit-msg": "fabric verify-commit"
},
"lint-staged": {
    "*.{js,jsx,less,md,json}": [
    	"prettier --write"
	],
	"*.ts?(x)": [
		"prettier --parser=typescript --write"
	]
},
```
# 跳过hooks

```bash
git commit -m 'xxx' --no-verify
```