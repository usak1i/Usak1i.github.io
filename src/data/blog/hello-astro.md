---
author: Usak1i
pubDatetime: 2026-05-01T04:00:00+08:00
title: Hello Astro!
slug: hello-astro
featured: true
draft: false
tags:
  - astro
  - typescript
  - blog
  - github
description: 部落格正式上線！記錄為什麼選擇 Astro 來建立這個技術部落格。
---

歡迎來到 **Usak1i's Blog**，這是第一篇文章。

## 為什麼要建一個技術部落格？

寫作是整理思緒最好的方式。在學習新技術、解決問題的過程中，把過程記錄下來不只幫助自己回顧，也可能幫助到其他遇到相同問題的人。

這個部落格會記錄：

- 技術筆記與學習心得
- 踩坑記錄與解法
- 工具與工作流程分享

## 為什麼選擇 Astro？

在考慮部落格框架時，我評估了幾個選項：Next.js、Hugo、Hexo。最終選擇 [Astro](https://astro.build) 的理由很簡單：

**以內容為核心的設計哲學。** Astro 預設生成純靜態 HTML，只在真正需要互動的地方才送出 JavaScript。對於以文章為主的部落格來說，這是最理想的架構。

搭配 [AstroPaper](https://github.com/satnaing/astro-paper) 主題，幾乎開箱即用：

- 深色 / 淺色模式切換
- 標籤分類
- 全文搜尋（Pagefind）
- 自動產生 OG 圖片、RSS、Sitemap
- TypeScript 支援

## 部署到 GitHub Pages

整個部落格透過 GitHub Actions 自動部署到 GitHub Pages。每次 push 到 `main` branch，CI 就會自動建置並更新網站，完全不需要手動操作。

---

就這樣，開始了。後續會陸續分享更多技術文章，敬請期待。
