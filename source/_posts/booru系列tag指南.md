---
title: "booru系列图站tag指南"
date: 2026-1-23
draft: false
tags: ["ACG","Webooru","教程"]
categories: ["二次元"]
description: "pixiv的标签差别极大，请完整阅读指南否则几乎无法查询"
---

## 一、 基础搜索逻辑

在 Danbooru 中，标签之间默认是“与（AND）”的关系，多个标签以**空格**分割。

| 语法      | 说明                    | 示例                                |
| --------- | ----------------------- | ----------------------------------- |
| **空格**  | 同时包含多个标签（AND） | `blue_eyes blonde_hair`             |
| **`or`**  | 包含其中之一（OR）      | `cat_ears or dog_ears`              |
| **`-`**   | 排除某个标签（NOT）     | `solo -rating:e` (排除成人级)       |
| **`*`**   | 通配符，匹配模糊词      | `*reimu` (能匹配到hakurei_reimu )   |
| **`~`**   | 旧版 OR 运算符          | `~tag1 ~tag2` 等同于 `tag1 or tag2` |
| **`( )`** | 逻辑分组                | `(A B) or (C D)`                    |

## 二、 元标签 (Metatags) - 高级筛选

元标签可以筛选图片属性而非内容，格式通常为 `类别:值`。

### 1. 分级与状态 (Ratings & Status)

- **`rating:g / s / q / e`**：分级筛选（General全年龄 / Sensitive敏感 / Questionable问题 / Explicit暴露）。
- **`status:deleted / pending / flagged`**：图片状态（已删除 / 待审核 / 被举报）。
- **`is:sfw / nsfw`**：快捷筛选（安全 / 不安全）。

### 2. 用户与互动 (User & Interaction)

- **`user:用户名`**：搜索该用户上传的内容。
- **`fav:用户名`**：搜索该用户收藏的内容。
- **`score:>50`**：分数大于 50 的图片。

### 3. 画师与来源 (Artist & Source)

- **`artcomm:true`**：有画师评语。
- **`source:pixiv`**：来源包含 pixiv 的图片。
- **`pixiv:ID`**：直接通过 Pixiv 作品 ID 搜索。

## 三、 数值与范围筛选 (Range Qualifiers)

支持使用 `>`, `<`, `>=`, `<=`, `..` 等符号。

| 语法                    | 说明                  | 示例                                |
| ----------------------- | --------------------- | ----------------------------------- |
| **`id:100..200`**       | ID 在 100 到 200 之间 | `id:<1000`                          |
| **`date:2024-01-01..`** | 某日期之后上传        | `date:..2023-12-25`*2023-12-25之前* |
| **`age:<1w`**           | 上传时间在一周内      | 支持 s, mi, h, d, w, mo, y          |
| **`mpixels:>2`**        | 分辨率大于 200 万像素 | `order:mpixels`                     |
| **`ratio:4:3`**         | 宽高比                | ratio:<16:8 ~ ratio:>16:10          |

## 四、 排序方式 (Ordering)

使用 `order:` 改变结果排布。

- **`order:score` / `order:favcount`**：按分数 / 收藏数从高到低。
- **`order:id` / `order:id_desc`**：按上传顺序 正序 / 倒序。
- **`order:random`**：随机排序。
- **`order:rank`**：近期热门排序。
- **`order:filesize`**：按文件大小。

## 五、 关系与容器 (Parent/Child & Pools)

- **`parent:ID`**：搜索该 ID 的关联图（如同一张图的不同修剪版）。
- **`has:children`**：有子图的图片。
- **`pool:ID / 名字`**：搜索特定图集（Pool）中的内容。

## 六、 搜索限制 (Limitations)

> [!IMPORTANT] **免费用户限制**：
>
> - 每次搜索最多只能使用 **2个** 标签。搜索时间超过3秒会超时
> - 可使用age:<1month，limit:5（公网版本写死了limit为100无法更改），order:score等限制标签防止超时
> - 免费元标签（如 `rating:`, `status:`, `id:`, `score:` 等）不计入这 2 个标签的限制，可以自由叠加。

## 七、 收藏库标签 (Special Tags)

收藏库与车万图库尽量模拟实现booru系列的tag系统，复刻了些基础的。

- **比例筛选**：支持使用比较运算符，例如 `ratio:>=1:1` (搜索横图)。
- **排序逻辑**：
  - `order:random`：随机返回插画结果。
  - `order:score`：按评分高低排序。
- **排除逻辑**：支持使用减号 `-` 排除特定标签（例如 `-landscape` 排除风景图）。

## 八、 PIXIV 搜索指南 (Pixiv-style Searching)

由于 Pixiv 的标签体系与 Booru 系列差异较大，建议采用以下策略：

### 1. 标签获取技巧

> [!TIP] **查找Tag**：
>
> 建议通过**长按插画**进入详情页，直接点击对应的 Tag 进行跳转查询。
>
> ![](https://files.seeusercontent.com/2026/04/22/3qGt/image_106.png)
>
> *（以后想办法弄个pixiv的Tag对照表，先画个饼在这里）*

### 2. 绕过会员限制搜高赞图

由于 Pixiv 原生按分数/收藏筛选仅对会员开放，在本项目中请使用 **“users入り”** 关键词进行模糊匹配：

| **搜索关键词示例**                      | **说明**                     |
| --------------------------------------- | ---------------------------- |
| **`users`**                             | 搜索带有收藏数统计标签的作品 |
| **`1000users入り`**                     | 搜索收藏数超过 1000 的作品   |
| **`バーチャルYouTuber 10000users入り`** | 搜索一万赞以上的虚拟主播插画 |

>简易点用100user这样的就行啦