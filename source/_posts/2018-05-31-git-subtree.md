---
title: git subtree
date: 2018-05-31 17:17:03
tags:
  - git
categories:
  - code
---

# 为什么要用subtree
> 当多个项目需要用到同一部分代码时，有几种办法？

- 复制/粘贴，简直没法忍
- 发布npm包，每次发个新版本都得去npm up
- subtree

<!--more-->

# 结合sourcetree使用

## 初始化
假设git地址为`xxx.git`，本地路径为`xxx`， 分支为`master`

> 当`本地路径`不存在时，sourcetree会自动新建和关联subtree，否则需要执行代码来新建对应关系

在sourcetree中新增subtree，`仓库-添加/链接子树`，填写`URL`(xxx.git)和`本地路径`(xxx)即可在sourcetree中推送和拉取代码，勾选`Squash提交`，会在新建subtree同时拉取最新代码并新建一次提交
![附图](/images/20180531/subtree.png)

> 当`本地路径`已经存在时，执行以上操作会提示无法获取代码，需要手动执行以下命令，此命令也是官方介绍的新建subtree操作

```bash
git subtree add --prefix=xxx xxx.git master --squash
```

## 对已有subtree的项目

当subtree初始化并完成代码提交后，项目中已经有了目录`xxx`，其他组员需要在sourcetree中新增subtree的快捷方式，同样在`仓库-添加/链接子树`，填写`URL`(xxx.git)和`本地路径`(xxx)，会提示subtree已存在，选择创建链接即可
![附图](/images/20180531/link.png)


## subtree代码的维护

在左侧导航中会出现新建的子树，以本地目录`xxx`命名，右键可以进行各种操作
![附图](/images/20180531/update.png)

和普通项目一样,subtree更新过程中也会出现冲突，stash本地的代码即可，建议由专人统一维护此目录，其他组员直接使用即可

# 命令行
假设git地址为`xxx.git`，本地路径为`xxx`， 分支为`master`

> 初始化

```bash
git subtree add --prefix=xxx xxx.git master --squash
```

> 更新代码

```bash
git subtree pull --prefix=xxx xxx.git master --squash
```

> 推送代码

```bash
git subtree push --prefix=xxx xxx.git master --squash
```