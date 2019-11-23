---
categories:
  - Application
tags:
  - WordPress
  - Multisite
---

(教學)建立多個 WordPress 於同一個站上 Follow [WordPress Doc](https://codex.wordpress.org/Create_A_Network) Install WordPress 就先不介紹了

1.  開啟 network 的設定

```
vi wp-config.php
```
新增於以下於 `/* That's all, stop editing! Happy blogging. */` 之上 
```
/* Multisite */ 
define( 'WP_ALLOW_MULTISITE', true ); 
WebAdmin->Tools->Network Setup
```

2\. 創建新的 subdomain
`
vi wp-config.php
```
```
新增以下於 `/* That's all, stop editing! Happy blogging. */` 之上 
```
define('MULTISITE', true); 
define('SUBDOMAIN_INSTALL', false); 
define('DOMAIN_CURRENT_SITE', '10.10.86.147'); 
define('PATH_CURRENT_SITE', '/network/wordpress/'); 
define('SITE_ID_CURRENT_SITE', 1); 
define('BLOG_ID_CURRENT_SITE', 1);
```

新增以下於 .htaccess 檔案中
```
RewriteEngine On
RewriteBase /network/wordpress/
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
RewriteRule . index.php [L]
```
3\. 確認 admin settings 可以選擇多個 sites ![](/assets/images/multisites.png)
