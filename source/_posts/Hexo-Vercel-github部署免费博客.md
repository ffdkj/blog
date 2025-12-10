---
title: "Hexo+Vercel+github部署免费博客"
date: 2025-12-9
draft: false
tags: ["教程", "Hexo", "blog"]
categories: ["技术"]
description: "可惜访问Vercel分配的域名还是得科学上网"
---

### 本地环境准备

**安装 Git 和 Node.js：** 确保您的电脑上已安装 Git 和 Node.js。
**安装 Hexo CLI：** 运行以下命令：

```
npm install -g hexo-cli
```

### 本地初始化博客项目：

```
# 终端进入希望部署项目的文件夹
# 创建并进入项目文件夹
hexo init my-gitee-blog
cd my-gitee-blog
# 安装依赖
npm install
```

撰写博客： 将需要上传的Markdown文件存放在 `source/_posts`文件夹中。

###  托管到github远程仓库

1. **创建 GitHub 账号和新仓库：**

   - 在 **GitHub** 上注册并登录。
   - 点击右上角的 **“+”** -> **“New repository”**。
   - 仓库名称随意（例如 `my-vercel-blog`），设置为 **Public**。
   - **不要**勾选初始化 README 等选项。

2. **将本地代码推送到 GitHub：** 在您的本地博客项目 (`my-gitee-blog`) 文件夹中运行以下 Git 命令：

   Bash

   ```
   # 初始化 Git
   git init
   # 关联远程仓库地址（请替换为您的实际仓库地址）
   git remote add origin <您的 GitHub 仓库 URL>
   # 添加所有文件
   git add .
   # 提交
   git commit -m "Initial Hexo setup"
   # 推送 (默认分支通常是 master 或 main)
   git push -u origin main
   ```

> 推送前可以在项目文件夹目录终端执行hexo server 本地部署，先看看效果及不及格再推送

### 连接 Vercel 自动部署

1. **注册 Vercel 账号：**
   - 访问 [Vercel 官网](https://vercel.com/)。
   - 点击 **“Sign Up”**，推荐使用 **GitHub 账号**直接登录和授权。
2. **导入项目：**
   - 登录后，点击 **“Add New”** -> **“Project”**。
   - 选择 **“Import Git Repository”**，找到您刚才创建的 GitHub 仓库 (`my-vercel-blog`)，点击 **“Import”**。
3. **配置构建设置 (关键)：** 在配置页面，Vercel 会自动检测项目类型。由于我们使用的是 Hexo，需要确保构建命令正确： | 配置项 | 默认值 (Hexo) | | :--- | :--- | | **Framework Preset** (框架预设) | **Other** 或 **Hexo** (如果 Vercel 识别出来) | | **Build Command** (构建命令) | `hexo generate` | | **Output Directory** (输出目录) | `public` |
   - **注意：** 如果 Vercel 自动识别出 Hexo，这些命令可能会被自动填写。
4. **部署：** 点击 **“Deploy”**。Vercel 将自动从 GitHub 拉取代码，执行 `hexo generate` 命令，并将 `public` 文件夹的内容托管到 CDN 上。
5. **完成：** 部署成功后，Vercel 会提供一个默认的域名（例如 `my-vercel-blog-xxxx.vercel.app`）。点击访问，您的博客就上线了！

### 后续更新博客

一旦设置完成，您只需要执行以下两步来更新博客：

1. 在本地 `source/_posts` 文件夹中编写或添加新的Markdown文件。

2. 将本地代码推送到 GitHub：

   ```
   git add .
   git commit -m "New blog post"
   git push
   ```

> Vercel 会自动检测到 GitHub 仓库的变动，并重新构建和部署博客。

> 文件名中最好不要包含+，#，&，?等的非法字符，会引发404错误                                                                                               发发