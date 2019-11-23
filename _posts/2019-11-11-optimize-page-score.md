---
categories:
  - Application
tags:
  - Optimize
  - Page Score
---

# 如何改善網站分數

### 分數　≠　速度

改善分數要點基本上直接使用 WordPress Plugin 即可改善大多數狀況. 以下列情形基本上透過一個 [LSCache plugin](https://wordpress.org/plugins/litespeed-cache/) 即可達成, 重點是 Free. ![](/assets/images/100-1024x579.png) 我的個人測試 woo-commerce 網站尚未使用 CDN 故YSlow 僅 99\. 但 PageSpeed Score 輕鬆可以達 100\. 此 woocommerce default theme 也有幾十張圖片仍可被優化使分數達滿分. 對大部分來請求幫助的 user 來說, 網站載入時間, 網站分數對他們生意有一定的影響.

#### 1\. Optimize images

只須點選 Update and Send button 即可開始優化. 更多內容參考 [LiteSpeed wiki ](https://www.litespeedtech.com/support/wiki/doku.php/litespeed_wiki:cache:lscwp:image-optimization)

#### 2\. Minify/Combine/Push CSS & JavaScript. Minify HTML

![](/assets/images/lscwp-settings-optimize-555x1024.png)

#### 3\. Leverage browser caching

基本上就是寫以下 rule 到 .htaccess file Default 2592000 秒. 可自行更改

    ### marker BROWSER CACHE start ###
    <FilesMatch "\.(pdf|ico|svg|xml|jpg|jpeg|png|gif|webp|ogg|mp4|webm|js|css|woff|woff2|ttf|eot)(\.gz)?$">

    ExpiresActive on
    ExpiresByType application/pdf A2592000
    ExpiresByType image/x-icon A2592000
    ExpiresByType image/vnd.microsoft.icon A2592000
    ExpiresByType image/svg+xml A2592000

    ExpiresByType image/jpg A2592000
    ExpiresByType image/jpeg A2592000
    ExpiresByType image/png A2592000
    ExpiresByType image/gif A2592000
    ExpiresByType image/webp A2592000

    ExpiresByType video/ogg A2592000
    ExpiresByType audio/ogg A2592000
    ExpiresByType video/mp4 A2592000
    ExpiresByType video/webm A2592000

    ExpiresByType text/css A2592000
    ExpiresByType text/javascript A2592000
    ExpiresByType application/javascript A2592000
    ExpiresByType application/x-javascript A2592000

    ExpiresByType application/x-font-ttf A2592000
    ExpiresByType application/x-font-woff A2592000
    ExpiresByType application/font-woff A2592000
    ExpiresByType application/font-woff2 A2592000
    ExpiresByType application/vnd.ms-fontobject A2592000
    ExpiresByType font/ttf A2592000
    ExpiresByType font/woff A2592000
    ExpiresByType font/woff2 A2592000

    ### marker BROWSER CACHE end ###

#### 4. Load JS Deferred / Load CSS Asynchronously 時常可提高分數

#### 5. Remove Query Strings/Remove Google Fonts/Remove WordPress Emoji

試著讓網站在優一丁點

#### 6\. 減少外部載入的資源

e.g. Youtube, TV, google map. 外部資源目前是無法被個人網站優化的.

#### 7\. HTTP Compression

使用 Server support [gzip](https://en.wikipedia.org/wiki/Gzip) or [brotli](https://en.wikipedia.org/wiki/Brotli) 使 static file 壓縮, 傳送時可減少網路頻寬

#### 附上測試 page score 網站

*   [GTMetrix](https://gtmetrix.com/)
*   [Pingdom](https://tools.pingdom.com/)
*   [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
