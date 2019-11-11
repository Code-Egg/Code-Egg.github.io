---
categories:
  - Scripting
tags:
  - Prestashop
  - Cache
  - Bash
---

如果網站已安裝 Cache Plugin 但沒有提供 warmup(crawler)功能, 此篇可以教學如何使用 script 去產生每一頁的快取. 這樣第一次訪問的客戶都將可以快入的載入頁面.

## 如何產生 Sitemap

Prestashop 可使用 ”Google Sitemap Module“ 來產生方法 sitemap 

Download [https://github.com/PrestaShop/gsitemap/archive/master.zip | gsitemap]; then change the file name to `gsitemap.zip`.

Click the **Configure** button and you will see e.g. `xxx/1_index_sitemap.xml`(This is your main SITE-MAP-URL, ). 

## Crawler Script

[下載](https://www.litespeedtech.com/packages/prestashop/cachecrawler.sh)

<script src="https://gist.github.com/Code-Egg/ff6a3c26df3bc29c247a4e9eedb2692e.js"></script>

## Script 如何使用

確認 script 擁有執行權限. 

* -h, --help: Show this message and exit.
* -m, --with-mobile: Crawl mobile view in addition to default view.
* -c, --with-cookie: Crawl with site's cookies.
* -b, --black-list: Page will be added to blacklist if HTML status error and no cache. Next run will bypass page.
* -g, --general-ua: Use general user-agent instead of lscache_runner for desktop view.
* -i, --interval: Change request interval. ''-i 0.2'' changes from default 0.1 second to 0.2 seconds.
* -v, --verbose: Show complete response header under ''/tmp/crawler.log''.
* -d, --debug-url: Test one URL directly. as in ''sh cachecrawler.sh -v -d http://example.com/test.html''.
* -qs,--crawl-qs: Crawl sitemap, including URLS with query strings.
* -r, --report: Display total count of crawl result.

Crawl 執行間格我們須多常執行呢? 得基於每次執行時間和 Public Cache TTL 設定.預設 TTL 為一天(24hr). .E.g. 每天執行兩次, at 3:30am/15:30:
```
30 3/15 * * * path_to_script/M2_crawler.sh SITE-MAP-URL -m -i 0.2
```
Note:  也可使用線上工具 [online crontab tool](https://crontab.guru/|online) 幫你確認 cron參數是否正確. Note: 如非 litespeed 網頁伺服器, 則需要修改 User-Agent 為一般 header即可使用

## How to Verify

當使用 browser developer tool, 開啟商品頁面時. 你會看到 `X-LiteSpeed-Cache: hit` 在 response header 裡.
