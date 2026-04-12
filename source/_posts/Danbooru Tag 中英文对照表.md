---
title: "Danbooru Tag 中英文对照表"
date: 2026-2-5
draft: false
tags: ["Webooru","ACG"]
categories: ["二次元"]
description: "点击输入文本"
---

# Danbooru Tag 中英文对照表 

![Tag Count](https://count.getloli.com/@nayun?name=nayun&theme=booru-lewd&padding=7&offset=0&align=center&scale=1&pixelated=1&darkmode=auto&num=155000) 

## ***每日更新 !***

收录所有post_count>=10的tag,使用人工智能gemini-3-flash-preview翻译+能工智人校对,如使用过程中遇到翻译错误可以提issue或骚扰2624696826a@gmail.com

## 数据库结构：

| 字段名 (Column)  | 类型 (Type) | 约束 (Constraint) | 描述 (Description)                                           |
| ---------------- | ----------- | ----------------- | ------------------------------------------------------------ |
| **`name`**       | `TEXT`      | `PRIMARY KEY`     | **英文标签名**。Danbooru 原始标签（单词间以下划线 `_` 分隔）。 |
| **`category`**   | `INTEGER`   | -                 | **标签分类 ID**。例如：0-常规, 1-艺术家, 3-版权/作品, 4-角色, 5-元数据。 |
| **`cn_name`**    | `TEXT`      | -                 | **中文翻译**。由gemini-3-flash-preview翻译+能工智人校对的结果。 |
| **`post_count`** | `INTEGER`   | -                 | **引用数量**。该标签在 Danbooru 上的帖子总数，反映标签的热门程度。 |

![image-20260206044100331](https://s2.loli.net/2026/02/06/2dYgTl1bUVsqQJa.png)



