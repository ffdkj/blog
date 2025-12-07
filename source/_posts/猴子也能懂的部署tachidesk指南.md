---
title: "猴子也能会的tachidesk部署指南"
date: 2025-10-11
draft: false
tags: ["教程", "Hugo","Tailscale"]
categories: ["技术"]
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

> *<a href="https://blog.csdn.net/m0_51290571/article/details/144635357" target="_blank" style="color: blue;">Windows装Docker至其他盘</a>*

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



如果只需要在电脑上运行，到此即可使用，以下是局域网内访问与远程访问的内容





### 3.电脑开放防火墙4567端口

![image-20250821140436228](https://s2.loli.net/2025/10/09/Am42N1Vok7HJdDv.png)![image-20250821140438926](https://s2.loli.net/2025/10/09/b7X6WIQocY9Pai3.png)![image-20250821140442555](https://s2.loli.net/2025/10/09/PlI5zeOu26h1CZL.png)![image-20250821140444441](https://s2.loli.net/2025/10/09/C15id69AOgTvIG2.png)![image-20250821140445893](https://s2.loli.net/2025/10/09/TLU78mVXxPpFMN1.png)

```powershell
ipconfig | Select-String "IPv4"
```

在powershell运行命令查询本机IP地址如192.168.1.100

或访问该网站<a href="https://ip.900cha.com/" target="_blank" style="color: blue;">IP地址查询</a>

至此与电脑主机处于同一局域网的手机，平板等终端可以访问http://192.168.1.100:4567

如果需要远程访问，可以使用tailscale组网

> 由于大部分情况下我们没有固定的ip，所以即使只需求局域网使用仍然推荐使用Tailscale等虚拟组网软件，如<a href="https://www.radmin-lan.cn/" target="_blank" style="color: blue;">Radmin LAN</a>等

> 校园网可能也需要使用Tailscale，因为有些校园网会阻止设备局域网联机





### 4.使用tailscale组网实现远程访问

![image-20250821173314462](https://s2.loli.net/2025/10/09/uZFSLOs7JA8rUhB.png)

在所需要连接访问的设备下载<a href="https://tailscale.com/download" target="_blank" style="color: blue;">安装tailscale</a>（苹果设备需要美版apple ID）

并注册登录统一账号

一经注册tailscale会分配一个虚拟IP（永久）,右键托盘中的tailscale图标可以看到

![image-20250821174632187](https://s2.loli.net/2025/10/09/2WfgzjdEpMY9A8k.png)

或者运行命令

```powershell
tailscale ip
```

此时无论你身处何地，浏览器打开http://100.XX.XXX.XXX:4567/（X处填入分配的IP）即可访问部署的tachidesk

> tailscale传文件也是把好手

***

### 5.使用<a href="https://www.wangwangit.com/Windows上的代理客户端Clash/index.html" target="_blank" style="color: blue;">Clash</a>代理转发tachidesk浏览

**（我无法提供任何节点，也不教怎么科学上网，只是教有条件的人配置代理）**

漫蛙，漫画柜等网站需要科学上网的，配置tachidesk即可

![image-20250821193752728](https://s2.loli.net/2025/10/09/xw6S4qPuv251Bsa.png)

![image-20250821193802384](https://s2.loli.net/2025/10/09/xw6S4qPuv251Bsa.png)

host.docker.internal 是docker容器访问宿主机的ip，7891是clash用与socks代理的端口

![image-20250821194031606](https://s2.loli.net/2025/10/09/gxLKYaAo8lm6Pck.png)

clash也需将Allow LAN打开，设置端口7891

以下是流量转发的路径

![image-20250821192834285](https://s2.loli.net/2025/10/09/JWMso87Lwa6DFYT.png)

> 推荐使用<a href="https://clash-party.com/" target="_blank" style="color: blue;">Clash Party</a>，对小白更友好

> 漫蛙

### 6.使用<a href="https://github.com/FlareSolverr/FlareSolverr" target="_blank" style="color: blue;">FlareSolverr</a>绕过<a href="https://blog.csdn.net/qq_21050249/article/details/131571780" target="_blank" style="color: blue;">cloudflare</a>

```powershell
docker run -d `
  --name=flaresolverr `
  -p 8191:8191 `
  -e LOG_LEVEL=info `
  --restart unless-stopped `
  ghcr.io/flaresolverr/flaresolverr:latest
```

powershell或cmd运行以上代码拉取flaresolverr库并运行容器

![image-20250907044116773](https://s2.loli.net/2025/10/09/v1iqgJbAEt4jkcB.png)

FlareSolverr服务器地址填入http://X.X.X.X:8191（X处填入tailscale分配的ip地址）

![image-20250907044410980](https://s2.loli.net/2025/10/09/kHzJdrf5SGPxjDg.png)
