---
title: "git学习"
date: 2025-12-8
draft: false
tags: ["学习", "git"]
categories: ["技术"]
description: "👍git太方便了"
---

# git使用

### 提交本地

git init 将当前目录变成Git可以管理的仓库

```
git init
```

使用git add 添加文件/文件夹到仓库

```
git add readme.txt
```

> git add . 添加当前目录所有文件

用命令`git commit`告诉Git，把文件提交到仓库,-m参数这是提交的文字说明

```
git commit -m
```

### 推送提交

与远程github仓库关联

```
git remote add origin git@github.com:sdjf/git.git
```

将本地提交内容推送到远程仓库（master分支）里

```
git push -u origin master
```

### 回退版本

使用git log确认日志，找到要回退的版本与当前head标在哪

```
git log
```

> 按“q”退出git log

使用git reset 回退版本HEAD标注的就是当前版本使用一个^回退一个版本，^^就是两个以此类推

```plain
git reset --hard HEAD^
```

往往提交时会遇到error: failed to push some refs to 'https:XXX'错误，这是因为git认为本地分支历史与远程分支历史产生了**分歧**，Git 拒绝了您的推送，以防止您不小心覆盖或丢失远程仓库上的提交。
可以使用--force-with-lease参数推送，它会检查远程分支是否在您上次拉取或查看后被他人更新过。如果远程分支被更新了，它会拒绝推送，从而避免覆盖其他人的工作。

```
git push --force-with-lease origin master
```

