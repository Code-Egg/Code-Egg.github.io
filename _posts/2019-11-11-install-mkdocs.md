---
categories:
  - Application
tags:
  - Mkdocs
---

MkDocs 快速安裝教學 準備環境: Ubuntu 18.0.4 + Web Server (LiteSpeed or OpenLiteSpeed) Ubuntu 18 已內建 Python3 可方便安裝 mkdoc 新版(>1.0) 並支援更多語法

### Step 1\. 安裝 pip3

    sudo apt-get python3-pip

### Step 2\. 安裝 mkdocs

    pip3 install mkdocs

### Step 3\. 於網頁伺服器 doc root  創建 project
``` bash
cd /usr/local/lsws/Example/html/
mkdocs new my-project
```
### Step 4\. build 預設資料
```
cd my-project
mkdocs build
```
### Step 5\. Verify

Visit **http://Server_IP/my-project/site** ![](/assets/images/Screen-Shot-2019-01-14-at-10.12.49-PM.png) 基本上佈建就完成了, BUT , 預設資料看起來不夠美 [下篇將介紹 MkDocs 快速上手](https://code-egg.github.io/tools/mkdocs-start/)
