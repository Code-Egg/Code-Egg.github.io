---
categories:
  - Scripting
tags:
  - Python
  - Linebot
---
## **LINE BOT Message 初學者記錄(二)**

參考 LINE 官方網站提供新的 [API referense](https://devdocs.line.me/en/#messaging-api) Create LINE@ Manager account from LINE Business Center > Messaging API LINE Developer Set Webhook URL and get Channel Access Token

### **Process Picture:**

[![](https://2.bp.blogspot.com/-08akCoessy0/V_WuenRA73I/AAAAAAAAGPo/CWYiFBU1lrAUi10QCvmTJ_2b17U0DZWvACK4B/s640/LINE-BOT-DAVID.png)](http://2.bp.blogspot.com/-08akCoessy0/V_WuenRA73I/AAAAAAAAGPo/CWYiFBU1lrAUi10QCvmTJ_2b17U0DZWvACK4B/s1600/LINE-BOT-DAVID.png)

### **Code:**

views.py
<script src="https://gist.github.com/Code-Egg/3204f580cb15285d7f393d1c266bc50a.js"></script>

### **Result:**

Request: here 
Response : Hello, I am Nanguachumo.
Type 'w cityname' get weather! here Request: w london 
Response : Current country: GB Current weather: Rain Current tempearture: 12.12 
[![](https://1.bp.blogspot.com/-t4v75VQr1PU/V_WpR4PaLRI/AAAAAAAAGPY/bH0UO3ifXD8M5ZWxnSp9JiejP3S3rtrBACK4B/s200/240.jpg)](http://1.bp.blogspot.com/-t4v75VQr1PU/V_WpR4PaLRI/AAAAAAAAGPY/bH0UO3ifXD8M5ZWxnSp9JiejP3S3rtrBACK4B/s1600/240.jpg) <span style="font-family: 'arial' , 'helvetica' , sans-serif;"> </span>

### <span style="font-family: 'arial' , 'helvetica' , sans-serif;">**小撇步:**</span>

*   <span style="font-family: 'arial' , 'helvetica' , sans-serif;">練習時, 一樣先跑 local server, 透過 REST 發出 POST + content, 做初步判斷程式碼有錯誤否.</span>

### **Next:**

*   ㄧ些 Function 看起來不只做ㄧ件事呀!, 要讓 function 都可被重覆使用
*   圖片不知為何電腦 LINE 無法顯示
*   Template & Confirm 官方回應目前 IOS 無法正常顯示, 下ㄧ版更新後即可正常

### **<span style="font-family: 'arial' , 'helvetica' , sans-serif;">Reference:</span>**

*   [LINE Official API](https://devdocs.line.me/en/)
*   [Openweather API](https://openweathermap.org/current)
*   [syntaxhighlighter](http://lester116.blogspot.tw/2013/10/bloggerpython-syntaxhighlighter.html)

### **Get knowhow:**

*   Azure run Django 無法正常使用 Static. 故強制於 urls.py 直接指定 load picture.
*   Azure local Git 不知為何有時 Clone 會失敗...
*   Line official 晚上 9點 可能 server 繁忙無法正常發送訊息
*   Python - re module
*   Python - "'", """, """"" 有點不一樣
*   Python - NoneType not equal 'None'

### **心得:**

*   純練習寫小程式, 95% 時間花在debug
