---
categories:
  - Scripting
tags:
  - Python
  - Linebot
  - Heroku
  - Diaglogflow
---
自 LINE 推出 API 後越來越多開發者分享, 今天就完全發落 pyladies 的[gitbook](https://pyladies-taiwan.gitbooks.io/line-bot-tutorial/content/) 練習做習題. 內容有趣且詳細, 搭配 Line SDK 寫出美美的程式碼 (根本不是新手寫的!!) 功能: 用 "機器學習" 了解你"是否詢問" 餐廳or肚子餓. 並依據你提供的地址回答隨機一間附近的美食

### 直接先看結果:

1.  1.  任意輸入英文或中文, e.g. lala is hungry
    2.  bot 回告訴我你在哪

1.  直接點送出位置
2.  bot 回隨機一間餐廳

![](/assets/images/S__4808830-576x1024.jpg) 

再來試試中文: e.g. 餐廳推推(不工作 XD) -> 餐廳推薦(工作) 

<img src="/assets/images/S__4808852-169x300.jpg" alt="" width="576" height="1024"/>

### 開啟 Heroku

創立一個新 app Settings -> Reveal config vars 輸入所有會用到四組的 API ![](/assets/images/bot-2-300x143.png)

*   ACCESS_TOKEN: [從 LINE Dev Manager 得到](https://developers.line.me/console/)
*   SECRET: [從 LINE Dev Manager 得到](https://developers.line.me/console/)
*   DIALOGFLOW_CLIENT_ACCESS_TOKEN: [從 DIALOGFLOW 得到](https://console.dialogflow.com/api-client)
*   GOOGLE_API_KEY: [從 Google 得到](https://developers.google.com/maps/documentation/javascript/get-api-key)

#### 使用 Heroku CLI 傳程式碼, 需下列四個檔案

*   **app.py, Procfile, requirements.txt, runtime.txt**

檔案與內容分別為: runtime.txt:

*   python-3.6.4

requirements.txt:

*   line-bot-sdk
*   flask
*   apiai

Procfile:

*   web: python app.py

app.py:

<script src="https://gist.github.com/Code-Egg/50283631ce6c04fe95d1303546c5b7f8.js"></script>

### 心得:

1.  藉由 LINE SDK 可以寫出簡約卻非常完整的程式, 但如果想了解架構可能得自己來弄一遍才行.
2.  對於 decoration 還是非常不熟悉
3.  Dialogflow 藉由親民的介面, 讓非專業人士"我"接觸些 machine learning.

### Todo:

1.  1.  雖然分開中文與英文輸入來對應 Training, 不過試驗起來中文好像很難有 ML 的 feel. 可能中文需要更多的資料筆來訓練, 暫且還是繼續輸入英文唄.

    2.  目前回復隨機的餐廳, 或許加個判斷 4 顆星以上的再推薦會更吸引人 XD.

## CUSTOMe choose rate >= 4
    res_num = (len(top20_restaurants)) ##20
    above4=[]
    for i in range(res_num):
        try:
            if top20_restaurants[i]['rating'] > 3.9:
                #print('rate: ', top20_restaurants[i]['rating'])
                above4.append(i)
        except:
            KeyError
    if len(above4) < 0:
        print('no 4 start resturant found')
    # 3\. 隨機選擇一間餐廳
        restaurant = random.choice(top20_restaurants)
    restaurant = top20_restaurants[random.choice(above4)]


2.  後續也可以幫忙 book 想要的餐廳或是再推薦下一間
