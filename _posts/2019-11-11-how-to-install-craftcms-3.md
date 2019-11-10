---
categories:
  - Application
tags:
  - CraftCMS 3
  - CentOS 7
---
快速安裝教學 準備環境: CentOS7 + PHP72 + cPanel + LSWS/Apache 從 WHM/cPanel 建立 user "democraftcms" 並建立 mysql database + user SSH to server and run following command

## 安裝 Craft 3

經由 composer 方式下載

    composer create-project craftcms/craft /home/democraftcms/public_html/craft3

![](/assets/images/craft-2.png) 更改檔案權限

    chown -R democraftcms:democraftcms craft3/

經由 console 安裝並輸入資料庫資訊

    /home/democraftcms/public_html/craft3/craft setup

![](/assets/images/craft-3.png) 安裝成功後可以看到的預設前端介面 ![](/assets/images/craft-4-1024x681.png) 使用者後台 ![](/assets/images/craft-5-1024x496.png)

## 安裝第三方 Demo 資料 (Optional)

需準備 mysql 登入資訊 下載 happylager 資料

    git clone https://github.com/craftcms/demo.git happylager.test

安裝

    cd happylager.test
    composer install

匯入 sql 檔案

    mysql -u democraf_happylager -p democraf_happylager < happylager.sql

創建 .env 檔

    vi .env

    ENVIRONMENT="dev"
    SECURITY_KEY="GoplVO9SzWSYLIvNuDBQP9M-LEJN5EWA"
    DB_DRIVER="mysql"
    DB_SERVER="localhost"
    DB_USER="YOURDATA"
    DB_PASSWORD="YOURDATA"
    DB_DATABASE="YOURDATA"
    DB_TABLE_PREFIX=""
    DB_PORT="3306"

  更改檔案權限

    chown -R democraftcms:democraftcms happylager.test/

後臺登入帳號密碼

*   Username: admin
*   Password: password

## ![](/assets/images/craft-6-1024x602.png)

## Note: Craft 安裝需求

參考[官方資料](https://docs.craftcms.com/v3/requirements.html#server-requirements)

#### Craft requires the following:

*   PHP 7.0+
*   MySQL 5.5+ with InnoDB (or MariaDB 5.5+), or PostgreSQL 9.5+
*   A web server (Apache, Nginx, IIS)
*   At least 256MB of memory allocated to PHP
*   At least 200MB of free disk space

#### Craft requires the following PHP extensions:

*   ctype
*   cURL
*   GD or ImageMagick. ImageMagick is preferred.
*   iconv
*   JSON
*   Multibyte String
*   OpenSSL
*   PCRE
*   PDO MySQL Driver or PDO PostgreSQL Driver
*   PDO
*   Reflection
*   SPL
*   Zip
