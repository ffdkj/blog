---
title: "用Tailscale和Ech0搭建自己的私人博客"
date: 2025-10-16
draft: false
tags: ["教程", "Tailscale","Ech0","博客"]
categories: ["技术"]
cover:
    image: "https://s2.loli.net/2025/10/16/17AL6bomh4tCj9w.jpg"
    alt: "网络错误"
    caption: "source：www.artstation.com/artwork/b5bxvE"
---

# 用<a href="https://tailscale.com/download" target="_blank" style="color: blue;">Tailscale</a>和<a href="https://github.com/lin-snow/Ech0" target="_blank" style="color: blue;">Ech0</a>搭建自己的私人博客

!['Ech0的UI'](https://s2.loli.net/2025/10/16/dKy4qoup167zcNU.png "Ech0的UI")

***

*在服务器端运行Ech0，使其绑定在tailscale分配的虚拟ip上，这样将只允许tailscale私网中的设备访问*

***



推荐使用docker安装使用

> *<a href="https://www.cnblogs.com/yihuyuan/p/18773255" target="_blank" style="color: blue;">安装Docker与Docker Compose</a>* 

> *<a href="https://tailscale.com/download" target="_blank" style="color: blue;">安装Tailscale</a>*  

新建docker-compose.yml文件填入以下内容

```
version: '3'
services:
  ech0:
    image: sn0wl1n/ech0:latest
    container_name: ech0
    ports:
      - "100.XXX.XXX.XXX:6277:6277"  
      - "100.XXX.XXX.XXX:6278:6278"
      #将100.XXX.XXX.XXX替换为部署主机的tailscale分配的ip
    volumes:
      - ./ech0/data:/app/data
    environment:
      - JWT_SECRET="Hello Echos"
      
    restart: unless-stopped   

```

命令行键入

```cmd
tailscale ip
```

或访问<a href="https://login.tailscale.com/admin/machines" target="_blank" style="color: blue;">Machines - Tailscale</a>查询允许Ech0的服务器端的tailscale虚拟ip地址以替换docker-compose.yml中的容器映射端口
终端运行(在docker-compose.yml所在目录下)

```
docker compose up
```

访问100.XXX.XXX.XXX:6277，Ech0注册的第一个账号将默认为管理员

至此，只有tailscale私网中的设备（下载并登录同一账号）才能访问100.XXX.XXX.XXX:6277的Ech0