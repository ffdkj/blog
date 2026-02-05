---
title: "猴子也能会的tachidesk部署指南"
date: 2025-10-11
draft: false
tags: ["教程", "Hugo","Tailscale"]
categories: ["技术"]
index_img: https://s2.loli.net/2025/10/12/kqKaL5tDIHwWnzZ.png
description: "mihon/tachiyomi怎么没有ios版啊…………  <br>
老是被cloudflare墙掉很难受啊…………  <br>
多个设备的阅读记录不同步好烦啊…………  <br>
能不能像访问网站一样方便地看漫画啊？  <br>
有的兄弟，有的，tachidesk就是干这个的<br>"    
cover: https://s2.loli.net/2025/10/12/kqKaL5tDIHwWnzZ.png
---

> mihon/tachiyomi怎么没有ios版啊…………  
> 老是被cloudflare墙掉很难受啊…………  
> 多个设备的阅读记录不同步好烦啊…………  
> 能不能像访问网站一样方便地看漫画啊？  
> **有的兄弟，有的，tachidesk就是干这个的**    

***



### 1. 安装 <a href="https://www.cnblogs.com/phpnan/p/19092854" target="_blank" style="color: blue;">Docker</a>并部署 <a href="https://newzone.top/services/dockers-on-nas/tachidesk.html#配置指南" target="_blank" style="color: blue;">Tachidesk</a>

<a href="https://www.docker.com/products/docker-desktop/" target="_blank" style="color: blue;">下载Docker</a>

> *<a href="https://www.cnblogs.com/geekbruce/articles/18554682" target="_blank" style="color: blue;">不知道下 ARM 还是 AMD版本点这里</a>*
>
> *详细教程及报错解决参考<a href="https://www.cnblogs.com/yxysuanfa/p/19124346" target="_blank" style="color: blue;">Docker部署配置全流程（超详细——Windows和Linux） - 指南 - yxysuanfa - 博客园</a>*

打开Terminal终端![	](https://s2.loli.net/2025/10/09/jPeIuJf29FwSGQz.png)



```powershell
docker run -d `
  --name tachidesk `
  -p 4567:4567 `
  ghcr.io/suwayomi/tachidesk
```

复制粘贴运行

（如果下载卡顿，可以用<a href="https://steampp.net/" target="_blank" style="color: blue;">Steam++</a>加速dockerhub，或<a href="https://zhuanlan.zhihu.com/p/1953242201254495256" target="_blank" style="color: blue;">配置国内镜像源</a>）

![](https://s2.loli.net/2025/10/09/q1ZwGDOdFajWuix.png)

***

### 2.配置Tachidesk 

docker运行tachidesk容器后浏览器打开http://localhost:4567便会出现tachidesk的界面

![image-20250821163929987](https://s2.loli.net/2025/10/09/FXqNxHY1LCGDSac.png)

语言在此更改

添加扩展库

![image-20250821163956487](https://s2.loli.net/2025/10/09/zUGvdDQ5alsuk2S.png)

设置——浏览——扩展库——添加源

```http
https://raw.githubusercontent.com/keiyoushi/extensions/repo/index.min.json
```

```http
https://raw.githubusercontent.com/LittleSurvival/copymanga-copy20/main/index.min.json
```

依次复制粘贴代码以添加图源仓库

![image-20250821164317580](https://s2.loli.net/2025/10/09/DT8rb1XQp2hLaHM.png)

再安装自己需要的图源即可（部分网站需要代理， 跳转到第5部分）

*如果只需要在电脑上运行，到此即可使用，以下是局域网内访问与远程访问与配置代理的进阶内容*

***

### 3.局域网内使用

#### 电脑开放防火墙4567端口

![image-20250821140436228](https://s2.loli.net/2025/10/09/Am42N1Vok7HJdDv.png)![image-20250821140438926](https://s2.loli.net/2025/10/09/b7X6WIQocY9Pai3.png)![image-20250821140442555](https://s2.loli.net/2025/10/09/PlI5zeOu26h1CZL.png)![image-20250821140444441](https://s2.loli.net/2025/10/09/C15id69AOgTvIG2.png)![image-20250821140445893](https://s2.loli.net/2025/10/09/TLU78mVXxPpFMN1.png)

#### 查询本机局域网ip

```
ipconfig 
```

在powershell/cmd运行命令查询本机局域网的IP地址,通常是192.168.x.x

![image-20260205132731813](https://s2.loli.net/2026/02/05/k2Z9zlWQGvx5fYi.png)

或访问192.168.1.1（通常预留的网关地址，账号密码在路由器背面）,直接找路由器分配的ip地址。

#### 固定分配ip （非必要）

由于路由器分配的ip是不固定的，经常会连不上得找新的ip地址，我们可以选择固定路由器分配的ip，但更**推荐**的是使用**tailscale**组网，tailscale将分配给设备永久固定的虚拟ip。

1. 打开 **控制面板** > **网络和共享中心** > **更改适配器设置**。
2. 右键点击你正在用的网卡（Wi-Fi 或以太网），选 **属性**。
3. 双击 **“Internet 协议版本 4 (TCP/IPv4)”**。
4. 点选 **“使用下面的 IP 地址”**：
   - **IP 地址**：输入你想固定的地址（如 `192.168.1.5`）。
   - **子网掩码**：通常是 `255.255.255.0`。
   - **默认网关**：你的路由器 IP（通常是 `192.168.1.1`）。

> 推荐教程[怎么设置固定ip? - 知乎](https://zhuanlan.zhihu.com/p/9780625923)

至此与电脑主机处于同一局域网的手机，平板等终端可以访问http://192.168.x.x:4567

如果需要远程访问，可以使用tailscale组网

> 因为局域网ip容易变动，即使只需求局域网使用仍然推荐使用Tailscale等虚拟组网软件，如<a href="https://www.radmin-lan.cn/" target="_blank" style="color: blue;">Radmin LAN</a>等

> 校园网可能也需要使用Tailscale，因为有的校园网会阻止设备互连

***

### 4.远程使用

#### <a href="https://tailscale.com/download" target=_blank>安装使用tailscale</a>

![image-20250821173314462](https://s2.loli.net/2025/10/09/uZFSLOs7JA8rUhB.png)

在所需要连接访问的设备下载安装tailscale（苹果设备需要美版apple ID）

并注册登录统一账号

一经注册tailscale会分配一个虚拟IP（永久）,右键托盘中的tailscale图标可以看到

![image-20250821174632187](https://s2.loli.net/2025/10/09/2WfgzjdEpMY9A8k.png)

或者运行命令

```powershell
tailscale ip
```

此时无论你身处何地，浏览器打开http://100.XX.XXX.XXX:4567/（X处填入分配的IP）即可安全地访问部署的tachidesk

> tailscale传文件也是把好手

***

### 5.使用<a href="https://www.wangwangit.com/Windows上的代理客户端Clash/index.html" target="_blank" style="color: blue;">Clash</a>代理

**（我无法提供任何节点，也不教怎么科学上网，只是教有条件的人配置代理）**

漫蛙，漫画柜等网站需要科学上网的，配置tachidesk即可

![image-20250821193752728](https://s2.loli.net/2025/10/09/xw6S4qPuv251Bsa.png)

![](https://s2.loli.net/2026/02/05/8Qpd4evLnMf5SqV.png)

host.docker.internal 是docker容器访问宿主机的ip，端口数自行查看clash配置（通常为7890或7891，7892）

>Linux系统部署的请使用docker0虚拟网桥的地址（ 通常默认是**`172.17.0.1`**）

![image-20250821194031606](https://s2.loli.net/2025/10/09/gxLKYaAo8lm6Pck.png)

clash需将**Allow LAN**打开

> 推荐使用<a href="https://clash-party.com/" target="_blank" style="color: blue;">Clash Party</a>，对小白更友好

***

### 6.使用<a href="https://github.com/FlareSolverr/FlareSolverr" target="_blank" style="color: blue;">FlareSolverr</a>绕过<a href="https://blog.csdn.net/qq_21050249/article/details/131571780" target="_blank" style="color: blue;">cloudflare</a> 

```powershell
docker run -d `
  --name=flaresolverr `
  -p 8191:8191 `
  -e LOG_LEVEL=info `
  --restart unless-stopped `
  ghcr.io/flaresolverr/flaresolverr:latest
```

powershell或cmd运行以上代码拉取flaresolverr镜像并运行容器

![image-20250907044116773](https://s2.loli.net/2025/10/09/v1iqgJbAEt4jkcB.png)

FlareSolverr服务器地址填入http://X.X.X.X:8191（X处填入tailscale分配的ip地址）

