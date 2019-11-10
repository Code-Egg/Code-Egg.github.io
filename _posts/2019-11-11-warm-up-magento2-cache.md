---
categories:
  - Scripting
tags:
  - Magento 2
  - Bash
---

如果網站已安裝 Cache Plugin 但沒有提供 warmup(crawler)功能, 此篇可以教學如何使用 script 去產生每一頁的快取. 這樣第一次訪問的客戶都將可以快入的載入頁面.

## 如何產生 Sitemap

Magento 2 已內建模組來快速的產生 sitemap. 產生方法 sitemap Navigate to **Magento Admin > Stores > Settings > Configuration > Catalog > XML Sitemap** ![](/assets/images/m2-4-1024x384.png) Set **Generation Settings > Enabled** to **Yes** ![](/assets/images/m2-5.png) 設定 Single Sitemap 給所有 Storefronts Navigate to **Magento Admin > Marketing > Seo & Search > Sitemap**

1.  Click the **Add Sitemap** button
2.  Enter values
3.  Filename: **sitemap.xml** Path: **/**
4.  Click the Save & Generate button

如果一切順利, 一個 sitemap.xml 將會自動產生於 Magento 2 document root.

## Crawler Script

[下載](https://www.litespeedtech.com/packages/litemage2.0/M2-crawler.sh)

<script src="https://gist.github.com/Code-Egg/188dd65ec4c69f517c50a66bedeb759d.js"></script>

## Script 如何使用

確認 script 擁有執行權限. -h = help -m = 支持 desktop+Mobile view -i = 修改每個頁面 request 間格 `sh M2_crawler.sh SITE-MAP-URL -m -i 0.2` Crawl 執行間格我們須多常執行呢? 得基於每次執行時間和 Public Cache TTL 設定.預設 TTL 為一天(24hr). .E.g. 每天執行兩次, at 3:30am/15:30:
```
30 3/15 * * * path_to_script/M2_crawler.sh SITE-MAP-URL -m -i 0.2
```
Note:  也可使用線上工具 [online crontab tool](https://crontab.guru/|online) 幫你確認 cron參數是否正確. Note: 如非 litespeed 網頁伺服器, 則需要修改 User-Agent 為一般 header即可使用

## How to Verify

當使用 browser developer tool, 開啟商品頁面時. 你會看到 X-LiteSpeed-Cache: hit,litemage 在 response header 裡. ![](/assets/images/m2-3-1024x633.png)
