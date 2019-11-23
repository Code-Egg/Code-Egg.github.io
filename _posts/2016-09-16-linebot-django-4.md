---
categories:
  - Scripting
tags:
  - Python
  - Linebot
---

**LINE BOT Message 初學者記錄(四)** 
由於初步功能完成後 Azure 試用也到期了. 忍痛轉移平台到 RHC. 
中間曾試過 AWS EC2(一年試用), 可惜 Domain & SSL 持續沒搞定 ORZ. 只好躲在朋友 RHC 裡佔一個位置. 
參考 [Openshift](http://www.indjango.com/deploying-django-app-on-openshift/) 安裝使用 Openshift + Django 1.8.2 + Python3 After installing, just execute runserver to make sure web http://domain:8080 display normally 參考 app-deployments/current/repo/README.md 說明動作. Clone git to RHC app-deployments/current/repo/wsgi/ Modify app-deployments/current/repo/wsgi/application project name and app name 需要 RHC 執行時可用 env | grep PYTHON 看到哪些是自己要的參數 如果自己在 RHC 上執行 runserver 是無法持久的(idle 就斷了就算跑背景也沒用).

### **Porcess:**

你的 Git 倉庫       Github 上的倉庫       rhc 上的倉庫    rhc 的佈署程式 
git add . 
git commit 
------------ push ----------> 
---------------------------------------- push ---------> 
--------trigger ------>

### **Reference:**

*   [openshift setup django](https://github.com/openshift/django-example)

### **Get knowhow:**

1.  Windows save ssh key in User/name/.ssh/
2.  Linux save ssh key in / .ssh/
3.  Line white list 一旦設定則只有寫入的 IP 可進入.
4.  個人ID 放入額外 conf 並新增.gitignore 使用避免被爬走
5.  所有路徑都要用完整路徑, 不然會錯誤.

### **心得:**

*   搞定, 竟然沒新增功能這麼久, 到時會被 python 之神拋棄  XD
*   RHC 與  Azure 還蠻相同的, PC push 上去後自動執行.

2016.10.16

下一篇:  [Line Bot - Django - Non-Blocking](https://code-egg.github.io/scripting/linebot-django-5/)
