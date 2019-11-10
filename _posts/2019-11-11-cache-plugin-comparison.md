---
categories:
  - Web Server
  - Tools
tags:
  - Cache
  - WordPress
---
WordPress Caching Plugins 至少有以下常見的六種可使用. 但哪個 WordPress Cache plugin 最快最適合我呢? Benchmark 分別約多少? 我們將可以由下圖看出哪一項提供最快的服務, 同時也介紹附加功能. ![](/assets/images/cache-compare-1024x597.png) 以上測試於 AWS 上使用兩台 [lightsail](https://aws.amazon.com/lightsail/) 最便宜 $5 機型完成簡易測試

*   [ab](https://httpd.apache.org/docs/2.4/programs/ab.html) (ab -n 1000 -c 100 -H "Accept-Encoding: gzip,deflate" $URL)
*   對 blog post page + 50+ images + data generate

WebServer 配置

*   LSCache 與 LSWS + PHP71 搭配測試
*   其他所有 Cache 與 Apache 2.4 + PHP71 搭配測試

#### 優劣分析:

LSCache 最快, 適合流量較大或是電子商務的網站使用, 與 LSWS/OLS 搭配使用才有 Cache 效果. [WP Rocket](https://wp-rocket.me/) 也很快, 但要收費(1年 $39), 願意花錢且為 Apache 使用者仍是好選擇. [W3 Total](https://wordpress.org/plugins/w3-total-cache/) 附加功能也很多, 用 Apache 並且不打算花錢的好組合. 其餘 WP Super/WP Fatest/WP Simple plugin 數據較低不列入個人考慮選單 不使用 Cache 每秒僅能服務 3.5 requests, 可見 Cache 對於服務多個 visitor 非常重要

#### 功能分析:

LSCache, WP Rocket W3 total 皆提供

*   JS/CSS Minify 等功能
*   JS/CSS differ 服務
*   CDN 整合服務
*   Image Lazy load
*   Google Fonts Optimization
*   Browser Cache

LSCache, W3 total

*   Object Cache

#### 相容性:

LSCache, WP Rocket W3 total 分別提供不同 plugins 的相容性

#### 更多:

[How to optimize your site](https://site-optimize-note.tk/how-to-optimize-your-site-page-score/) – Page Score
