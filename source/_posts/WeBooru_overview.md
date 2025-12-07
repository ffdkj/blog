---
title: "Webooru食用教程"
date: 2025-12-7
draft: false
tags: ["教程", "Docker","Tailscale"]
categories: ["技术"]
cover:
    image: "https://s2.loli.net/2025/10/12/kqKaL5tDIHwWnzZ.png"
    alt: "网络错误"
    caption: "pid:130947439"

---



# WeBooru

WeBooru 是一个轻量级、高性能的 **Web 服务端程序**，基于 FastAPI 框架构建。它旨在提供一个稳定、功能丰富的私有客户端，浏览和管理Danbooru等图站的内容。

>目前版本支持Danbooru，Gelbooru，Safebooru，Koanchan，Yande，Rule34

通过在您的服务器上部署 WeBooru，您可以利用 **任何设备**（PC、手机、平板）的浏览器，通过局域网（或内网穿透）随时随地访问您的专属图站浏览使用。

> 所有帖子数据请求严格遵循图站的**官方API规范**进行获取，完全避非法的爬虫行为，**基本不会对目标网站造成异常负荷**。

### ✨ 主要特性

- **无缝浏览**：基于瀑布流的插画展示，瀑布式自动加载。
- **智能书签**：书签将记录您的阅读进度，随时从上次中断的地方继续浏览。
- **本地代理**：服务器配置代理，解决客户端的代理问题。
- **纯净体验**：无广告、无干扰的沉浸式插画阅览器。

------

### 📥 安装与部署

#### Docker 部署

Bash/cmd

```cmd
docker run -d --name webooru -p 100.65.203.30:8000:8000 20off/webooru:latest
```

***

> 如果你根本不知道docker啊，tailscale是什么东西，请移步隔壁[猴子也能会的tachidesk部署指南 | Hexo](https://blog-ffzz.vercel.app/2025/10/11/猴子也能懂的部署tachidesk指南/)

***

### 📷 截图

**帖子列表 (瀑布流模式)：** 简洁的网格视图，支持按标签搜索和无限滚动。

![](https://s2.loli.net/2025/12/06/S6F3eNXv8yWAVsI.webp)

**设置与历史记录面板：** 管理您的代理设置和站点源配置等。

![](https://s2.loli.net/2025/12/06/gFXvGykQsDal7fb.webp)

------

### 📜 许可证

本项目采用 **GPLv3** 许可证。 您可以自由地使用、修改和分发此软件，但必须保留原作者版权声明。