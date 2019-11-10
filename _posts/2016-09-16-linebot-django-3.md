---
categories:
  - Scripting
tags:
  - Python
  - Linebot
---
**LINE BOT Message 初學者記錄(三)** 
參考 LINE 官方網站提供新的 [API referense](https://devdocs.line.me/en/#messaging-api)
加入不同 Messaging API 功能並做出: Weather, Eats, News

### **構思與結果:**

#### **Step1.**

Input word: Test Output: Pumpkin picture with three buttons and Echo test in description [![](https://3.bp.blogspot.com/-22m29wWnhus/V_tkw31SwZI/AAAAAAAAGP8/v2LAhlVNfFkzK-tNzRfeAmT2nmKJmgGSACK4B/s320/punpkin.png)](http://3.bp.blogspot.com/-22m29wWnhus/V_tkw31SwZI/AAAAAAAAGP8/v2LAhlVNfFkzK-tNzRfeAmT2nmKJmgGSACK4B/s1600/punpkin.png)

#### **Step 2.**

Input: Click "Weather" button Output:Text "Enter a city name" Input:Text "Taipei" Output: Text "It's "25.5"C and "Rain" in "TW"" and a weather picture [![](https://4.bp.blogspot.com/-HBiY_p-VIro/V_tmBU1pVDI/AAAAAAAAGQI/PMWgUNb7Mp0-udbPDAc0oEQupX-xMvI1gCK4B/s320/weatherbutton.png)](http://4.bp.blogspot.com/-HBiY_p-VIro/V_tmBU1pVDI/AAAAAAAAGQI/PMWgUNb7Mp0-udbPDAc0oEQupX-xMvI1gCK4B/s1600/weatherbutton.png)

#### **Step 3.**

Input: Click "Eat" button Output: Confirm message Input: Click "Delicious" button Output: Random "Delicious food" picture PS. Allow click buttons again and again. [![](https://1.bp.blogspot.com/-Nb8C0aITyAY/V_tnwUni30I/AAAAAAAAGQc/ciPkQqbAH74qfDTwpWB9SBax5jDVDvoYQCK4B/s400/eatpicture.png)](http://1.bp.blogspot.com/-Nb8C0aITyAY/V_tnwUni30I/AAAAAAAAGQc/ciPkQqbAH74qfDTwpWB9SBax5jDVDvoYQCK4B/s1600/eatpicture.png) 

#### **Step 4.**

Input: Click "News" button Output: Four "News template" with Title, Description, and HyperLink. [![](https://2.bp.blogspot.com/-ewa7fSqNm0M/V_tot-_F5TI/AAAAAAAAGQo/dXM2TfsA5-8hvgOPvtMCV10YHSOhhrvYQCK4B/s320/newspicture.png)](http://2.bp.blogspot.com/-ewa7fSqNm0M/V_tot-_F5TI/AAAAAAAAGQo/dXM2TfsA5-8hvgOPvtMCV10YHSOhhrvYQCK4B/s1600/newspicture.png)

### **Code:**

views.py
<script src="https://gist.github.com/Code-Egg/2a0581622160783eda45f0099f3c3139.js"></script>

### **Reference:**

*   [Google_News_API](https://newsapi.org/google-news-api)
*   [Python skill](https://pythonnote.wordpress.com/2014/04/03/python%E6%8A%80%E5%B7%A7%E6%BC%82%E4%BA%AE%E5%8F%88%E9%80%9A%E9%A0%86%E7%9A%84%E7%A8%8B%E5%BC%8F%E7%A2%BC/)
*   [世界各國流行 APP](http://www.inside.com.tw/2016/05/30/worldwide-messaging-apps)

### **Get knowhow:**

*   Python: List and Dictionary "add" or "del"
*   LINE 多筆資訊放於同個 payload 內.
*   Global variable
*   Function 引數 "Request" 再替 client 送出需含 http header and content 才用到

### **Wait to fix:**

*   Weather 功能只取下一個參數, 當有兩個字以上的城市名會無法取得完整.
*   尚未做出迴圈提醒功能, 執行在記憶體內. 怎 kill.
*   Azure ㄧ個月到期, 是否要轉換平台.
*   Eat data 還太少.
*   此 Openweather 雖免費. 但有些國家判斷的溫度好像不太準...
*   News 內容是否需可直接顯示內容無需開啟新網頁(還不可佔我伺服器流量)

### **心得:**

*   搞定, 頭有點暈, 後面寫出的 function 很少能被重複使用 XD

2016.10.10

下一篇:  [Line Bot - Django - Platform to RHC](https://code-egg.github.io/scripting/linebot-django-4/)
