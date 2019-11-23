---
categories:
  - Web Server
tags:
  - Web Server
---
--- categories: - Web Server tags: - Web Server ---

## What is Web Server?

當我們每天在瀏覽網頁的時候，有想過這些無數個網站是怎麼來的嗎？不論大小，其實每個網站都是架在網頁伺服器上的喔！那什麼是網頁伺服器(Web Server)呢？ 伺服器一般來說就是在服務的電腦，所以網頁伺服器就是主要作為架網站(Host Website)的伺服器。而網頁的溝通協定是HTTP Protocol，所以網頁伺服器至少都要是個HTTP server，能讓接收和傳送HTTP commands。 以上都還是非常廣義的說明，但狹義來說，所謂的Web Server我們一般指的是運行在硬體上的軟體，而且了解URLs(Web addresses) 和 HTTP，也就是說當你在瀏覽網頁的時候呢，你實際上是在和Web Server那隻程式做互動。

## How to choose Web Server?

若懂了以上非常high level的解釋後，也想要嘗試自己架網站並且架在自己的網頁伺服器上的話呢，現在市場上有一些免費和付費的服務。你可能會想說，Web Server不就只是要安裝在伺服器上做些主動或被動的協調嗎？怎麼還會分這麼多品牌？這是當然的囉，像是Facebook.com和小公司的內部網站甚至你的個人網站需要的資源就差異非常多，要能承受一次多少個存取(Access)就會差很多。以下我將會簡單介紹比較這些Web Servers。

#### Apache

Apache Web server 是最被廣泛使用的web server software而且是開源軟體(Open Source). 據說世界上的所有網頁伺服器有67%都是跑Apache的

#### NginX

NginX 是市佔率第二的開源軟體，因為沒有Apache那麼豐富的功能，NginX相較下速度較快且靈活。現在也發展了很多功能像是Load Balancing, etc., 但屬於付費功能，技術支援也是屬於付費項目。

#### Microsoft IIS

Microsoft （我們的微軟大大）也有自己的Web server software — IIS, Internet Information Services。相較於Apache一般是支援Linux系統，IIS 只能架在Microsoft Windows 作業系統(OS, Operating System)上，適合習慣Windows系統的用戶，使用門檻掉低。

#### LiteSpeed

最後要介紹在Web Server software裡的新興之秀 — LiteSpeed Web Server (LSWS)。主要優勢為較Apache輕量，因此速度快超過六倍，而且擴充性很強，可以隨意和Apache替換使用而無downtime，並可以比Apache同時服務更多用戶，讓硬體的效能最大化。 目前LSWS是付費軟體但支援cpanel等控制介面，也有OpenLiteSpeed (OLS)作為開源軟體，有community在服務使用用戶。
