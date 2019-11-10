---
categories:
  - Web Server
tags:
  - DirectAdmin
  - LiteSpeed Web Server
  - CloudLinux
---

## Direct Admin 如何設定 CustomBuild2 搭配 web server + PHP Version on CloudLinux

先安裝CustomBuild2, 有了它安裝其他網頁伺服器和 PHP 都很方便.　以下範例皆使用 CloudLinux + LSWS

### Method 1\. Command line install lsws via CustomBuild 2

Download [CustomBuild2](http://forum.directadmin.com/showthread.php?t=44743)   並解壓縮於DirectAdmin 預設路徑 `/usr/local/directadmin/` 

```
cd /usr/local/directadmin
wget -O custombuild.tar.gz http://files.directadmin.com/services/custombuild/2.0/custombuild.tar.gz
tar xvzf custombuild.tar.gz
cd custombuild
./build
```

安裝 litespeed web server: 
```
./build update
./build set webserver litespeed
./build set php1_mode lsphp
./build litespeed
./build php n
```

### Method 2\. Install through Plugin Manager

先下載檔案至電腦, 開啟 Plugin Manager then upload the file. 下圖顯示裝完 CustomBuild2 Plugin + CLoudLinux + CageFS's result 
![](/assets/images/da-1-1024x609.png) 
CustomBuild 2 Plugin Interface shows like this 
![](/assets/images/da-2-1024x778.png)   
下圖顯示讓 user 選擇 Domain + 搭配自己想要的PHP 版本 
![](/assets/images/da-4.png)

## 特色：

1.  支持多個網頁伺服器, e.g. Apache, Litespeed, Nginx
2.  支持多個 PHP 版本及設定
3.  支持多個 DB 選項及設定
4.  支持 CLoudLinux
5.  全面支持 Command Line

## CustomBuild2 Support in details:

*   Apache
*   AWstats
*   Autoconf
*   Automake
*   ClamAV
*   cURL
*   Dovecot
*   Exim configuration files
*   FreeType
*   GD
*   htscanner
*   suhosin
*   ionCube loaders
*   libiconv
*   libjpeg
*   libpng
*   libmcrypt
*   libmhash
*   libspf2
*   libsrs_alt
*   mod_ruid2
*   ModSecurity
*   nginx
*   MySQL
*   Zend opCache
*   pigeonhole
*   PHP (mod_php, php-fastcgi, PHP-FPM, suPHP, lsphp)
*   ProFTPD
*   Pure-FTPd
*   SpamAssassin
*   Webalizer
*   Zend Optimizer
*   Zlib

## Error logs:

1.  Direct Admin: `/var/log/directadmin/error.log`
2.  Apache: `/var/log/httpd/error_log`
3.  MySQL:  `/var/lib/mysql/{SERVER_NAME}.err`
