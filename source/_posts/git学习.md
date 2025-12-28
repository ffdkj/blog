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

***

### 远程关联

```
git remote add <别名> <地址>:
```

将远程仓库的具体url与起的别名关联

>可以关联多个远程仓库

### [使用 git pull 拉取代码](https://blog.csdn.net/m0_45234510/article/details/120181503)

*git pull* 命令用于从远程仓库获取最新的提交记录并将其合并到本地分支。它实际上是 *git fetch* 和 *git merge* 的简写，先从远程仓库获取最新的提交记录，然后将这些提交记录合并到当前分支中。

基本用法

git pull [远程仓库名] [分支名]

示例

- **拉取远程仓库的代码并合并到当前分支**：

git pull origin master

- **更新远程仓库的代码为最新的**：

git fetch --all

git reset --hard origin/master

git pull origin master

git merge master

### 处理冲突

在拉取代码时，如果遇到冲突，需要先解决冲突再继续拉取，或者先保存本地代码再提交。

关联已有仓库并提交代码

- **克隆或拉取代码**：

git clone http://xxx.git

git pull http://xxx.git

- **创建和切换分支**：

git branch -a

git fetch

git checkout -b <远程分支名>

git pull origin <远程分支名>

- **上传并提交代码**：

git add xxx/

git commit -m "init-1.0"

git push origin feature

通过这些步骤，你可以轻松地使用 *git pull* 命令从远程仓库拉取代码并合并到本地分支，确保你的代码库始终保持最新。

***

### 推送提交

与远程github仓库关联

```
git remote add origin git@github.com:sdjf/git.git
```

> git remote -v  命令会列出目前关联的所有远程仓库

将本地提交内容推送到远程仓库（master分支）里

```
git push -u origin master
```

> -u 参数全面--set-upstream，设置一次后下次直接git push就会默认提交相关地址

***

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

***

### git分支

在开始工作前，你首先需要知道自己在哪个分支，以及有哪些分支可用。

- **`git branch`**：列出本地所有分支。当前所在的分支前会有一个 `*` 号。

- **`git branch -a`**：列出本地和远程仓库的所有分支。

- **`git branch <分支名>`**：创建一个新分支，但**不会**自动切换过去。

- **`git checkout -b <分支名>`**：【最常用】创建并立即切换到新分支。

  > *注：在较新版本的 Git 中，推荐使用 `git switch -c <分支名>` 代替。*

 分支切换与重命名

- **`git checkout <分支名>`**：切换到已有的分支。

  > *注：新版 Git 推荐使用 `git switch <分支名>`。*

- **`git checkout -`**：快速切换回上一个分支（类似电视遥控器的“回看”键）。

- **`git branch -m <旧名称> <新名称>`**：重命名分支。
