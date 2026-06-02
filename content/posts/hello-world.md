---
title: "Hello World"
date: 2026-06-02T10:00:00+08:00
draft: false
tags: ["Hugo", "博客"]
categories: ["随笔"]
---

## 你好，世界

这是我的第一篇博客文章，使用 Hugo + Even 主题搭建，部署在 GitHub Pages 上。

<!--more-->

### 为什么选择 Hugo

- 速度快：Go 语言编写，构建速度极快
- 主题丰富：社区提供了大量优质主题
- 部署简单：静态站点，配合 GitHub Actions 自动部署

### 写作流程

```bash
hugo new content post/my-new-post.md
hugo server -D
```

编辑 Markdown 文件，本地预览满意后推送到 GitHub，CI 自动构建部署。
