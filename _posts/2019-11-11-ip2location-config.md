---
categories:
  - Web Server
tags:
  - Feature
  - IP2Location
---

基於 IP 分辨使用者來源/國家, 並做出適當的回應. E.g. 德國來的 IP, 則直接回傳德文的網站網址. 都不符合則回傳英文網站網址. 更多使用, 如禁止某些國家的拜訪 本篇只介紹 **如何使用** 於LiteSpeed / Openlitespeed 上.

### 下載 DB

1.  [下載任何一個你要的 DB ](https://www.ip2location.com/developers#sample_ip2location_databases_bin)
2.  放置於網頁伺服器目錄, e.g. /usr/local/lsws/

### 設定

1.  於 LSWS Admin 介面, 進入 **Configuration > Server > General > General settings > [IP2Location DB](https://www.litespeedtech.com/docs/webserver/config/general#ip2locDBFile "https://www.litespeedtech.com/docs/webserver/config/general#ip2locDBFile")** 輸入 **DB File Path**:  /usr/local/lsws/IP-COUNTRY-SAMPLE.BIN並設定 **DB Cache Type** 為 `MemoryCache`![](/assets/images/ip2loc.png)
2.  進入** Configurations > Your Virtual Hosts > Rewrite** 新增 rewrite rules 來控制導向:
    1.  Set **Rewrite** to `Yes`
    2.  Rules: `RewriteCond %{ENV:IP2LOCATION_COUNTRY_SHORT} ^DE$ RewriteRule ^(.*)$ http://www.google.co.uk [L]`

更多範例,請參考 [Ip2location](https://www.ip2location.com/free/visitor-redirection#source-codes "https://www.ip2location.com/free/visitor-redirection#source-codes")

### 如何驗證
藉由 Proxy 來更改個人的來源 IP

連上 [此 Proxy 網站](https://hide.me/en/proxy "https://hide.me/en/proxy"), 我們可以簡單的選擇 (USA, Germany, Netherlands). 如需要更多國家選項, 則需要註冊帳號使用. ![](/assets/images/geo-3.png)

如果不會設定瀏覽器的 proxy IP . 參考這些 Chrome 的步驟教學設定:

1.  Click on **Settings**.
2.  Click **Show advanced settings**
3.  Scroll further down the list until you see **System**
4.  Click **Open proxy settings**
5.  Click the **<abbr title="Local Area Network">LAN</abbr> settings** button.
6.  On the **Internet Properties** window, click the **<abbr title="Local Area Network">LAN</abbr> settings** button.
7.  In the **<abbr title="Local Area Network">LAN</abbr> Settings**, uncheck the box that says **Automatically detect settings**.
8.  In the **Proxy Server** section, click the checkbox to enable `Use a proxy server for your <abbr title="Local Area Network">LAN</abbr>…`
9.  In the **Address** field, enter the IP Address and Port Number of your Proxy Server.
10.  Press the **OK** button and then press **OK** again to save your settings.
11.  Now when you surf the web, you will be surfing by using the Proxy Server.

## 如何除錯

*   確認 debug log
```
tail -f /PATH_TO_LSWS/log/error.log
```
    當使用 Germany IP:
```
[REWRITE] Rule: Match '/' with pattern '^(.*)$, result: 2
[REWRITE] Cond: Match 'DE' with pattern '^(DE)$, result: 2
[REWRITE] Source URI: '/' => Result URI: 'https://en.wikipedia.org/wiki/Germany'
```
    當使用 Netherlands IP:

```
[REWRITE] Rule: Match '/' with pattern '^(.*)$, result: 2
[REWRITE] Cond: Match 'NL' with pattern '^(DE)$, result: -1
```

*   當模組無法運作, 請確認權限 (e.g. `nobody`) 可以執行 IP2Location database

*   如果 IP2Location 變數無法顯示, 請確認來源 IP address 不是內網網路, 像是10.0.0.0/8, 172.16.0.0/12 or 192.168.0.0/16\. IP2Location 只能接受廣域網路

