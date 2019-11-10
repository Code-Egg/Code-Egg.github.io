---
categories:
  - Web Server
tags:
  - Feature
  - Brotli
---

Brotli 壓縮

從 google 釋放的開源技術, Brotli 相對常見的 Gzip 可減少 20% 流量

瀏覽器支援:

*   Firefox v44+ 支援 Brotli
*   Chrome v51+ 支援 Brotli

平台支援:

*   支援 6 種平台 (Windows, Mac, Linux, Chrome OS, Android, and Android WebView).

Header 如何顯示: User agent 支持 Brotli 將以 **br** 方式顯示於 **accept-encoding** request header. 舉例來說 Chrome (53.0.2785.101 m): `accept-encoding:gzip, deflate, sdch, br` 缺點:

*   本身可以設定壓縮等級, 當然等級越高所耗的 CPU 也越高
*   需使用於 HTTPS 協定
