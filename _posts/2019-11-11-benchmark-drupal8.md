---
categories:
  - Benchmark
tags:
  - Drupal 8 
  - Varnish
---

直接跑 ab benchmark (Request per seconds) 結果為:

*   Varnish Cache: **21827.58 **
*   Internal Page Cache: **1222.77**

Varnish 約為 Internal Page Cache **19 倍**

#### 測試需先安裝以下項目

CentOS7 -> Web Server(e.g. Apache 2.4.6) ->PHP 7.1 ->  Drupal 8 -> Varnish -> Purge setup

### Install Varnish

```
yum install -y epel-release pygpgme yum-utils 
```

edit /etc/yum.repos.d/varnishcache_varnish5.repo
```
[varnishcache_varnish5] 
name=varnishcache_varnish5 
baseurl=https://packagecloud.io/varnishcache/varnish5/el/7/$basearch 
repo_gpgcheck=1 
gpgcheck=0 
enabled=1 
gpgkey=https://packagecloud.io/varnishcache/varnish5/gpgkey sslverify=1 
sslcacert=/etc/pki/tls/certs/ca-bundle.crt metadata_expire=300 
[varnishcache_varnish5-source] 
name=varnishcache_varnish5-source baseurl=https://packagecloud.io/varnishcache/varnish5/el/7/SRPMS 
repo_gpgcheck=1 
gpgcheck=0 
enabled=1 
gpgkey=https://packagecloud.io/varnishcache/varnish5/gpgkey 
sslverify=1 
sslcacert=/etc/pki/tls/certs/ca-bundle.crt 
metadata_expire=300 
```
```
yum -q makecache -y --disablerepo='*' --enablerepo='varnishcache_varnish5' 
yum -y install varnish
```

#### 驗證 Varnish 安裝版本

`varnishd -V` 設定內建Cache 最短時間, e.g. 1 day ![](/assets/images/varnish10-1024x642.png)   此時驗證可經由網頁開發者工具的回傳 header 包含 varnish. ![](/assets/images/varnish-8-1024x584.png)  

#### Benchmark


簡易使用 ab tool 即可開始測試 Default varnish port 為 6081 HTTPD port 預設為 80 故測試不同 port 即可知道  Drupal 8 內建 Cache 與 Varnish 速度個多少 
```
ab -k -n 10000 -c 10 -H "Accept-Encoding: gzip,deflate" $SERVER_IP:6081/ ab -k -n 1000 -c 10 -H "Accept-Encoding: gzip,deflate" $SERVER_IP:80/
```  

#### Varnish Purge on Drupal

對於純粹 Cache 可能會造成不少使用者的困擾e,g. 更新後, 頁面仍返回一樣的內容. 以下提供三種剛學的 purge 方式

1.  這裡就來安裝 [**Advance Varnish**](https://www.drupal.org/project/adv_varnish) Cache plugin on Drupal 吧.

安裝後直接進入操作介面選擇與後端 varnish admin 連線方式, e.g. 127.0.0.1:6082 ![](/assets/images/varnish9-1024x649.png) 2\. 有些人也推薦 http purge cache tool, 但沒特別使用過不確定 Purge 情形 ![](/assets/images/varnish-7-1024x626.png) 3\. 使用 Varnish config language 去設定那些 tag 必須被 purge 未使用過  - . -   如你習慣看到回傳 header 包含 **Miss** or **Hit,** 可以於 /etc/varnish/default.vcl 設定以下 rule 即可. 
``` php
sub vcl_deliver { 
# Happens when we have all the pieces we need, and are about to send the 
# response to the client. 
# 
# You can do accounting or modifying the final object here. 
if (obj.hits > 0) { 
set resp.http.X-Cache = "HIT"; 
} else { 
set resp.http.X-Cache = "MISS"; 
} 
}
```

####  Note:

1.  Debug varnish 時可用 varnishtop -b  or varnishlog 看到後端的所有 log
2.  Varnish port 可隨時更換為 80 來取代預設 http port
3.  Varnish 本身似乎不支援 https, 乃缺點. 如還是可以使其成功. (Nginx as an SSL Termination Proxy to make HTTPS possible with Varnish)
4.  由於 Varnish Cache is a caching HTTP reverse proxy. Varnish 與 web server 可完全分開兩台 server 為優點.
5.  網站的 purge 於 ecommerce 尤為重要. 如網站不常更新是可使用 Varnish 的

### Refer

*   [Install Varnish 5 on CentOS 7](https://www.evernote.com/OutboundRedirect.action?dest=https%3A%2F%2Fwww.tecmint.com%2Finstall-varnish-cache-on-centos-7-for-apache%2F)
*   [Advanced Varnish plugin](https://www.drupal.org/project/adv_varnish)
