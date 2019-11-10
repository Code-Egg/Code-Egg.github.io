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

![](/assets/images/S__4808830-576x1024.jpg) 再來試試中文: e.g. 餐廳推推(不工作 XD) -> 餐廳推薦(工作) ![](/assets/images/S__4808852-169x300.jpg)  

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

 import os
import apiai
import json
import requests
import random

from flask import Flask, request, abort

from linebot import (
    LineBotApi, WebhookHandler
)
from linebot.exceptions import (
    InvalidSignatureError
)
from linebot.models import (
    MessageEvent, TextMessage, TextSendMessage,
    ImageSendMessage,
    LocationMessage,
    TemplateSendMessage, ButtonsTemplate, URITemplateAction,
)

app = Flask(__name__)

ACCESS_TOKEN = os.environ.get('ACCESS_TOKEN')
SECRET = os.environ.get('SECRET')
GOOGLE_API_KEY = os.environ.get('GOOGLE_API_KEY')
DIALOGFLOW_CLIENT_ACCESS_TOKEN = os.environ.get('DIALOGFLOW_CLIENT_ACCESS_TOKEN')

ai = apiai.ApiAI(DIALOGFLOW_CLIENT_ACCESS_TOKEN)
line_bot_api = LineBotApi(ACCESS_TOKEN)
handler = WebhookHandler(SECRET)

@app.route('/')
def index():
    return "<p>Hello World!</p>"

# 監聽所有來自 /callback 的 Post Request
@app.route("/callback", methods=['POST'])
def callback():
    # get X-Line-Signature header value
    signature = request.headers['X-Line-Signature']

    # get request body as text
    body = request.get_data(as_text=True)
    app.logger.info("Request body: " + body)

    # handle webhook body
    try:
        handler.handle(body, signature)
    except InvalidSignatureError:
        abort(400)

    return 'OK'

# ================= 客製區 Start =================
def is_alphabet(uchar):
    if ('\u0041' <= uchar<='\u005a') or ('\u0061' <= uchar<='\u007a'):
        print('English')
        return "en"
    elif '\u4e00' <= uchar<='\u9fff':
        #print('Chinese')
        print('Chinese')
        return "zh-tw"
    else:
        return "en"
# ================= 客製區 End =================

# ================= 機器人區塊 Start =================
@handler.add(MessageEvent, message=TextMessage)  # default
def handle_text_message(event):                  # default
    msg = event.message.text # message from user
    uid = event.source.user_id # user id
    # 1\. 傳送使用者輸入到 dialogflow 上
    ai_request = ai.text_request()
    #ai_request.lang = "en"
    ai_request.lang = is_alphabet(msg)
    ai_request.session_id = uid
    ai_request.query = msg

    # 2\. 獲得使用者的意圖
    ai_response = json.loads(ai_request.getresponse().read())
    user_intent = ai_response['result']['metadata']['intentName']

    # 3\. 根據使用者的意圖做相對應的回答
    if user_intent == "WhatToEatForLunch": # 當使用者意圖為詢問午餐時
        # 建立一個 button 的 template
        buttons_template_message = TemplateSendMessage(
            alt_text="Please tell me where you are",
            template=ButtonsTemplate(
                text="Please tell me where you are",
                actions=[
                    URITemplateAction(
                        label="Send my location",
                        uri="line://nv/location"
                    )
                ]
            )
        )
        line_bot_api.reply_message(
            event.reply_token,
            buttons_template_message)

    elif user_intent == "WhatToPlay": # 當使用者意圖為詢問遊戲時
        msg = "Hello, it's not ready"
        line_bot_api.reply_message(
            event.reply_token,
            TextSendMessage(text=msg))

    else: # 聽不懂時的回答
        msg = "Sorry，I don't understand"
        line_bot_api.reply_message(
            event.reply_token,
            TextSendMessage(text=msg))

@handler.add(MessageEvent, message=LocationMessage)
def handle_location_message(event):
    # 獲取使用者的經緯度
    lat = event.message.latitude
    long = event.message.longitude

    # 使用 Google API Start =========
    # 1\. 搜尋附近餐廳
    nearby_url = "https://maps.googleapis.com/maps/api/place/nearbysearch/json?key={}&location={},{}&rankby=distance&type=restaurant&language=zh-TW".format(GOOGLE_API_KEY, lat, long)
    nearby_results = requests.get(nearby_url)
    # 2\. 得到最近的20間餐廳
    nearby_restaurants_dict = nearby_results.json()
    top20_restaurants = nearby_restaurants_dict["results"]
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
    # 4\. 檢查餐廳有沒有照片，有的話會顯示
    if restaurant.get("photos") is None:
        thumbnail_image_url = None
    else:
        # 根據文件，最多只會有一張照片
        photo_reference = restaurant["photos"][0]["photo_reference"]
        thumbnail_image_url = "https://maps.googleapis.com/maps/api/place/photo?key={}&photoreference={}&maxwidth=1024".format(GOOGLE_API_KEY, photo_reference)
    # 5\. 組裝餐廳詳細資訊
    rating = "無" if restaurant.get("rating") is None else restaurant["rating"]
    address = "沒有資料" if restaurant.get("vicinity") is None else restaurant["vicinity"]
    details = "南瓜評分：{}\n南瓜地址：{}".format(rating, address)

    # 6\. 取得餐廳的 Google map 網址
    map_url = "https://www.google.com/maps/search/?api=1&query={lat},{long}&query_place_id={place_id}".format(
        lat=restaurant["geometry"]["location"]["lat"],
        long=restaurant["geometry"]["location"]["lng"],
        place_id=restaurant["place_id"]
    )
    # 使用 Google API End =========

    # 回覆使用 Buttons Template
    buttons_template_message = TemplateSendMessage(
    alt_text=restaurant["name"],
    template=ButtonsTemplate(
            thumbnail_image_url=thumbnail_image_url,
            title=restaurant["name"],
            text=details,
            actions=[
                URITemplateAction(
                    label='查看南瓜地圖',
                    uri=map_url
                ),
            ]
        )
    )

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
