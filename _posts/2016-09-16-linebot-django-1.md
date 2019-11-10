---
categories:
  - Scripting
tags:
  - Python
  - Linebot
---

**LINE BOT 初學者記錄(一)**
**1\. 申請 LINE BOT 帳號:**
[開放平台資源，LINE 提供 1 萬個免費「BOT API 試用」帳號申請](http://technews.tw/2016/04/07/line-begins-providing-10000-bot-api-trial-accounts-prior-to-opening-up-access-to-messaging-api/) 
可以得出包含以下三個值:

*   Channel ID
*   Channel Secret
*   MID

**2.準備 HTTPs Server** 一個 https 的 server 的選擇至少有:

*   [<span style="color: blue;">Azure](https://azure.microsoft.com/zh-tw/)      
*   heroku
*   RHCloud

## **3.<span style="background-color: white; color: #333333; font-family: 'arial' , 'helvetica' , sans-serif; font-size: 13px; line-height: 20.99px;">LINE config ** **<span style="background-color: white;">架好 HTTPS server 後至 LINE BOT 填入**

*   <span style="line-height: 20.99px;">Callback URL <span style="background-color: transparent; font-family: 'arial' , 'helvetica' , sans-serif; line-height: 20.99px;"><span style="line-height: 20.99px;">https://XXXX-server.azurewebsites.net:443/YYYY
*   <span style="background-color: transparent; line-height: 20.99px;">Server IP Whiltelist x.x.x.x

**4.軟體語言都可:** 目前只剛學過 Django 於是乎就選它, 選自己想要的程式語言  **5.參考 LINE [<span style="color: blue;">官方文件](https://developers.line.me/bot-api/api-reference):** 多看幾次不吃虧 找出 Request(Sending messages)  E.g. 需要代入的格式: Header

*   Content-Type: application/json; charser=UTF-8
*   X-Line-ChannelID: Channel ID
*   X-Line-ChannelSecret: Channel secret
*   X-Line-Trusted-User-With-ACL: Channel MID

Payload

*   toChannel
*   eventType
*   content Object

**6.我的流程圖** [![](https://4.bp.blogspot.com/-A4z3Wxc715o/V9vuJfD12WI/AAAAAAAAGOM/6nEHIKlEGCUvFZLHjithtX3PpevB5OArwCLcB/s400/linebot.png)](https://4.bp.blogspot.com/-A4z3Wxc715o/V9vuJfD12WI/AAAAAAAAGOM/6nEHIKlEGCUvFZLHjithtX3PpevB5OArwCLcB/s1600/linebot.png) A. 確認 Request

1.  先知 LINE Client MID
2.  Local 觸發 URL 發出 Request > LINE server
3.  LINE server > Line Client 確認收到訊息

B. 確認 Response value

1.  Line Client 發出 message(觸發 URL) > LINE server
2.  LINE server > Azure 傳送 Line Client message
3.  Azure > LINE server > Line Client print JSON object 用來確認值(雖然官方已寫清楚格式)
4.  完成要回傳的內容或想做的事

## **7.Code(views.py)**

<script src="https://gist.github.com/Code-Egg/313038264fc83ff95ed754332e1e4d86.js"></script>

## **7.成果, 自問自答機**

*   LINE request : Hello
*   HTTP response: Hello

## **8.小撇步**

*   練習時, 從自己 LINE 丟訊息並吐出於瀏覽器上, 查看 JSON內格式
*   開發機與服務機器的 Django 版本最好一致
*   安裝 Chrome [rest](https://chrome.google.com/webstore/detail/advanced-rest-client/hgmloofddffdnphfgcellkdfbfbjeloo?hl=zh-TW) 模擬 Line Client 發出的 POST

## **9.Next**

*   部分程式碼改為更彈性
*   結合其它系統始發送訊息至 LINE

## **10.Reference:**

*   <span style="color: blue; font-family: 'arial' , 'helvetica' , sans-serif;">[Json Parser online](http://json.parser.online.fr/)
*   <span style="color: blue; font-family: 'arial' , 'helvetica' , sans-serif;">[csrf](http://stackoverflow.com/questions/13567507/passing-csrftoken-with-python-requests)
*   <span style="color: blue; font-family: 'arial' , 'helvetica' , sans-serif;">[urllib.request](https://docs.python.org/3.0/library/urllib.request.html)
*   <span style="color: blue; font-family: 'arial' , 'helvetica' , sans-serif;">[Azure web service](https://github.com/Azure/azure-content-zhtw/blob/master/articles/app-service-web/web-sites-nodejs-develop-deploy-mac.md)
*   [<span style="color: blue;">Huli LINE BOT 教學](http://huli.logdown.com/posts/726082-line-bot-api-tutorial)
*   [<span style="color: blue;">Andy LINE BOT 教學](https://blog.ccjeng.com/2016/06/Line-BOT-API.html)

## **11.Get Knowhow:**

*   Process between HTTPS server with LINE server 
*   JSON decode & Encode
*   <span style="font-family: 'arial';">What is Object
*   <span style="font-family: 'arial';">What is REST
*   UTF8 << in most situation just use it
*   Study LINE BOT official article
*   Python - Tuple, Dictionary+List together
*   Python - Return and HTTPresponse
*   Python - One function do one thing

2016/09/16 _剛學會一些 django 一點 python 與朋友來練習做出 LINE BOT 挺有趣的, 比預期花了不少時間在 debug 和思考流程上. 同時也第一次接觸 git 和 Azure._ _ps.在咖啡廳弄這有宅氣換發的感覺_ _Remark_ Official published on 2016.10 Line BOT -> Deprecated !!! 只好改用新的 API 於下一篇記錄
