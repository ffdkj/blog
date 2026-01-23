---
title: "booru系列图站介绍及使用"
date: 2025-1-23
draft: false
tags: ["ACG","Webooru","教程"]
categories: ["二次元"]
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