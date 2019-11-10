---
categories:
  - Scripting
tags:
  - Python
  - Linebot
---
**LINE BOT Message 初學者記錄(八) ** 
**Casual template: Yelp restaurant + Location** 
為了能在各國旅遊時可以方便找到優質餐廳, 結合 Location 和 Yelp 即可輕鬆達成 先看作品完成圖: 不管德國, 台灣, 美國... 都可輕鬆取得優質餐廳資訊 
[![](https://4.bp.blogspot.com/-sehqkln3Em0/Wc-6EaYZcII/AAAAAAAAGXc/i4COmXlMovkLKh9ijteHblBUr0niBxGeACK4BGAYYCw/s320/S__2736206.jpg)](http://4.bp.blogspot.com/-sehqkln3Em0/Wc-6EaYZcII/AAAAAAAAGXc/i4COmXlMovkLKh9ijteHblBUr0niBxGeACK4BGAYYCw/s1600/S__2736206.jpg)    [![](https://2.bp.blogspot.com/-8p7-TlByBm8/Wc-6ERK3OOI/AAAAAAAAGXU/QcnUS4nL0twgADetb4HutMgQJJ-yslM2gCK4BGAYYCw/s320/S__2736207.jpg)](http://2.bp.blogspot.com/-8p7-TlByBm8/Wc-6ERK3OOI/AAAAAAAAGXU/QcnUS4nL0twgADetb4HutMgQJJ-yslM2gCK4BGAYYCw/s1600/S__2736207.jpg)    [![](https://1.bp.blogspot.com/-GZQ7KJcoSow/Wc-6ERry-VI/AAAAAAAAGXY/_tpwFPXIha4ahqVodk8dxw5flH77VJLVwCK4BGAYYCw/s320/S__2736208.jpg)](http://1.bp.blogspot.com/-GZQ7KJcoSow/Wc-6ERry-VI/AAAAAAAAGXY/_tpwFPXIha4ahqVodk8dxw5flH77VJLVwCK4BGAYYCw/s1600/S__2736208.jpg)

### Step1 - Distinguish message from user is Location or Text:

[![](https://2.bp.blogspot.com/-Tu64eKvkzK0/Wc-8knwGLcI/AAAAAAAAGXo/2MJ2JO3B668fyUoqblyy6qSImxT_T0chACK4BGAYYCw/s320/location.png)](http://2.bp.blogspot.com/-Tu64eKvkzK0/Wc-8knwGLcI/AAAAAAAAGXo/2MJ2JO3B668fyUoqblyy6qSImxT_T0chACK4BGAYYCw/s1600/location.png) 
從上圖看出使用者輸入 location 會有一個 type: location, 因此我們只需要在 main function 裡判斷來源字串的 message_type 即可 
`if message_type == 'location':`

### Step2 - Yelp function:

我們 github 可看到現成的 yelp api in Python language. 並將吃進去的 address 最後 filter 出我們要的 'name', 'address', 'photo', 'url'

 <script src="https://gist.github.com/Code-Egg/80125648021df66164eded7fec938e93.js"></script>

### Step3 - Apply Yelp result to LINE:

使用 [LINE BOT Message 初學者記錄(三)](http://ericlinebot.blogspot.com/2016/10/line-message-bot-with-django.html)   
News 相同 casual template 方法 可以先檢查一下 payload data 符合我們預期的 
[![](https://2.bp.blogspot.com/-naD3D9Jn5LQ/Wc_MH8DZchI/AAAAAAAAGX4/AmOlDklM1QYlbFwDWAEAhswfivDUjRaIQCK4BGAYYCw/s320/payload.png)](http://2.bp.blogspot.com/-naD3D9Jn5LQ/Wc_MH8DZchI/AAAAAAAAGX4/AmOlDklM1QYlbFwDWAEAhswfivDUjRaIQCK4BGAYYCw/s1600/payload.png) **就完成喽!!** **現在只要丟出 Location 就可得到附近優質餐廳推薦!!** [![](https://3.bp.blogspot.com/-RB6Z9cXZkO8/WdKwFTrRTXI/AAAAAAAAGhw/x6TrgZ8AcXABucPgUIc6Fhy_509kA3QhgCK4BGAYYCw/s320/location.png)](http://3.bp.blogspot.com/-RB6Z9cXZkO8/WdKwFTrRTXI/AAAAAAAAGhw/x6TrgZ8AcXABucPgUIc6Fhy_509kA3QhgCK4BGAYYCw/s1600/location.png)  

### 南瓜出沒 掃描 QR Code 專區

[![](https://2.bp.blogspot.com/-pIqUfg3kypU/Wcm44xn7dNI/AAAAAAAAGW4/l8ikxu0e8pQHJbeQ0BDIyKgbKTqtmSdNACK4BGAYYCw/s200/QR.png)](http://2.bp.blogspot.com/-pIqUfg3kypU/Wcm44xn7dNI/AAAAAAAAGW4/l8ikxu0e8pQHJbeQ0BDIyKgbKTqtmSdNACK4BGAYYCw/s1600/QR.png) 剛好看到有興趣試試可以加入玩一下

### What's next:

1.  <span style="text-decoration: line-through;">結合 GPS 定位找飲料店</span>
2.  學別人上傳照片到 Google Cloud
3.  <span style="text-decoration: line-through;">結合 Spread Sheet 來記帳看起來不錯, 但我不記帳的 >< </span>
4.  <span style="text-decoration: line-through;">英文選擇題練習給認真的學生, 可惜沒看到 Free API</span>
5.  結合 ML 套件玩分析

2017/9/30
