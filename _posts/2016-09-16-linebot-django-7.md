---
categories:
  - Scripting
tags:
  - Python
  - Linebot
---
**LINE BOT Message 初學者記錄(七) 

** **Rich Button: Dog, Beauty girl, Handsome men** 
LINE BOT redesigned LINE Developers site (9/21/2017)整個更新,換湯不換藥. 
但是 UI 變漂亮就是給個讚 LINE Developer login from: https://developers.line.me/console/ [![](https://4.bp.blogspot.com/-UzXr9jiLJ5w/WcUEMRirtRI/AAAAAAAAGWk/kqRd2d5Exk07C2xhh9WL301FxULQ6EwMwCK4BGAYYCw/s320/Untitled.png)](http://4.bp.blogspot.com/-UzXr9jiLJ5w/WcUEMRirtRI/AAAAAAAAGWk/kqRd2d5Exk07C2xhh9WL301FxULQ6EwMwCK4BGAYYCw/s1600/Untitled.png) Line git: https://github.com/line/ Line document: https://devdocs.line.me/en/#reply-message

### Step1 - Create Rich Button from LINE Business:

此功能需上官網開啟 >>> [https://admin-official.line.me/](https://admin-official.line.me/) <span style="background-color: white; color: #1b1e21; display: inline; float: none; font-family: 'roboto' , 'open sans' , 'helvetica neue' , 'helvetica' , 'arial' , sans-serif; font-size: 14px; font-style: normal; font-weight: normal; letter-spacing: normal; text-indent: 0px; text-transform: none; white-space: normal; word-spacing: 0px;">"You can display a rich menu by going to the "Rich menu" page under the "Create rich content" page in the </span>[LINE@ Manager](https://admin-official.line.me/)<span style="background-color: white; color: #1b1e21; display: inline; float: none; font-family: 'roboto' , 'open sans' , 'helvetica neue' , 'helvetica' , 'arial' , sans-serif; font-size: 14px; font-style: normal; font-weight: normal; letter-spacing: normal; text-indent: 0px; text-transform: none; white-space: normal; word-spacing: 0px;">. Click "Create New" to design the rich menu by uploading images to the LINE@ Manager and mapping them to text or URLs.</span>" Rich menu can choose: Image or Text+icons

### Step2 - Create button function:

目前先做三顆按鍵功能:

1.  小狗圖
2.  美女圖
3.  帥哥圖

作法可完全參照之前的 [LINE BOT - Django 初學者記錄(三)](https://code-egg.github.io/scripting/linebot-django-3/) 最大困難就是找到圖庫而已,找到後就爬蟲爬下來. 圖片來源: 小狗圖: pixabay.com 美女圖: PTT 帥哥圖: 帥呀

### Step3 - Result:

[![](https://2.bp.blogspot.com/-zm4-Z8VoDKM/WcPWJAAgXPI/AAAAAAAAGWE/A0qsz0SKZ3Elg_XMt06MKRmslm2FmxCBwCK4BGAYYCw/s320/S__2621571.jpg)](http://2.bp.blogspot.com/-zm4-Z8VoDKM/WcPWJAAgXPI/AAAAAAAAGWE/A0qsz0SKZ3Elg_XMt06MKRmslm2FmxCBwCK4BGAYYCw/s1600/S__2621571.jpg) [![](https://3.bp.blogspot.com/-28IORvfxD_o/WcPWNDXBN8I/AAAAAAAAGWU/hYxROs7CARkBoU4G58wyRWA5XJbp8E5kgCK4BGAYYCw/s320/S__2621568.jpg)](http://3.bp.blogspot.com/-28IORvfxD_o/WcPWNDXBN8I/AAAAAAAAGWU/hYxROs7CARkBoU4G58wyRWA5XJbp8E5kgCK4BGAYYCw/s1600/S__2621568.jpg) [![](https://4.bp.blogspot.com/-q8HbuCfBrdI/WcPWLlmUC4I/AAAAAAAAGWM/FvXNyi64oP08zPOxnbP7fzVIquIfJQUwACK4BGAYYCw/s320/S__2621567.jpg)](http://4.bp.blogspot.com/-q8HbuCfBrdI/WcPWLlmUC4I/AAAAAAAAGWM/FvXNyi64oP08zPOxnbP7fzVIquIfJQUwACK4BGAYYCw/s1600/S__2621567.jpg)

### 南瓜出沒 掃描 QR Code 專區

[![](https://2.bp.blogspot.com/-pIqUfg3kypU/Wcm44xn7dNI/AAAAAAAAGW4/l8ikxu0e8pQHJbeQ0BDIyKgbKTqtmSdNACK4BGAYYCw/s200/QR.png)](http://2.bp.blogspot.com/-pIqUfg3kypU/Wcm44xn7dNI/AAAAAAAAGW4/l8ikxu0e8pQHJbeQ0BDIyKgbKTqtmSdNACK4BGAYYCw/s1600/QR.png) 剛好看到有興趣試試可以加入玩一下

### What's next:

1.  結合 GPS 定位找飲料店
2.  學別人上傳照片到 Google Cloud
3.  結合 Spread Sheet 來記帳看起來不錯, 但我不記帳的 ><
4.  英文選擇題練習給認真的學生, 可惜沒看到 Free API
5.  結合 ML 套件玩分析

2017/9/21
