---
categories:
  - Web Server
tags:
  - Feature
---
WebP 是一種圖片檔案格式,  與 jpg 相同品質但檔案更小

透過一些 plugin 轉檔使Chrome 和 Opera 瀏覽器使用者載入更輕巧的圖檔, 降低頻寬使用. 替換後可以由 Dev tool 觀察 Type 由 jpeg -> webp ![](/assets/images/webp-1.png)   ![](/assets/images/webp-3.png)   檔案大小可以透過 console 進去查: `PATH_TO_WORDPRESS/wp-content/uploads/YEAR/MONTH`

```
ls -alh | grep accessories-300
```
```
9.1K accessories-300x300.bk.jpg
8.6K accessories-300x300.jpg
6.0K accessories-300x300.jpg.webp
```
範例可以看出 webp 減少約 30% 圖片檔案大小
