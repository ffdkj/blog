---
title: "git学习"
date: 2025-12-8
draft: false
tags: ["学习", "git"]
categories: ["技术"]
description: "👍git太方便了"
---

# git使用

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

与远程github仓库关联

```
git remote add origin git@github.com:sdjf/git.git
```

将本地提交内容推送到远程仓库（master分支）里

```
git push -u origin master
```

