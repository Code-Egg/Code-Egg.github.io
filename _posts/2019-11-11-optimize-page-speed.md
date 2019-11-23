---
categories:
  - Web Server
tags:
  - Optimize
  - Page Speed
---

# 新手教學-改善網站速度

幫過一些網站管理者或是一般使用者改善網站速度的心得

## 檢查

先初步檢查載入慢的原因 查看使用者機器規格和目前 CPU / Memory 使用量, e.g. top 使用最大量的 Process, e.g. php, mysql, http..etc 目前連線數量, e.g. netstat -na | grep 80 | grep ESTA 使用哪種 Web Server 哪種 Application 需要改善, e.g. WordPress, Magento 最為常見 別的 Region visit 想改善, e.g. 從 US 訪問 日本的主機網站 檢查  error log

## 改善方式

### 改善 page loading:

1.  使用 full page cache plugin, 不會 hit back-end PHP 自然會快上許多倍
2.  Enable crawler, 使 user 第一次訪問即可 Serve with cache
3.  使用 HTTP2
4.  修正 resource status code 404

### 改善 php loading:

1.  使用 PHP 7.x instead of PHP 5.x
2.  使用 opcache, e.g. [Zend Opcache](http://pecl.php.net/package/ZendOpcache "http://pecl.php.net/package/ZendOpcache"), [xCache](http://xcache.lighttpd.net/ "http://xcache.lighttpd.net/")
3.  PHP child process increase
4.  確認無 PHP Fatal error

### 改善 database loading:

1.  使用 [Memcached](https://memcached.org/) or [Redis](https://redis.io/)

### 改善 http loading:

1.  是否正在使用 Apache, 可改為其他更輕量的網頁伺服器, e.g. LiteSpeedtech, Nginx
2.  DNS Prefetch, 預先解析給使用者. 可降低延遲

### 改善 Region 延遲:

1.  設定 CDN, 使訪問者由最近處取得 Static file.
    1.  [CloudFlare](https://www.cloudflare.com/) # Free, 個人覺得非正常 CDN, 介面容易使用, 免費版已提供很實用的基本功能. 推薦個人用戶可以使用
    2.  [CloudFront](https://aws.amazon.com/cloudfront/) # 市占率頗高
    3.  [Akamai CDN](https://www.akamai.com/) # 市占率頗高
    4.  MAXCDN # 無
2.  使用 Support [QUIC Protocol](https://en.wikipedia.org/wiki/QUIC) web server. 無須更改任何app 內容即可降低 15+% 速度. QUIC 於高延遲環境效果特別顯卓, e.g. 不同 region or 手機使用者

### 提升 TLS 速度

1.  使用 OCSP Stapling, 使瀏覽器跳過確認 Certificate 是否有效的步驟 #需 Web server and SSL 支持

### 改善 CPU Loading

1.  使用 top 確認是那些 process, 是否有被攻擊

### 改善 Memory Usage

1.  使用 Cache 可大幅改善現象
2.  停止使用 mod_pagespeed, 當沒快取時可以加速但同時消耗記憶體
