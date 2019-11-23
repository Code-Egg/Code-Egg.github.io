---
categories:
  - Tools
tags:
  - Grafana
  - Slack
---

繼上一篇 "[伺服器效能監控Prometheus 與 Grafana 安裝教學](https://code-egg.github.io/tools/Prometheus-grafana-install/)". 
此篇介紹如何設定 [Alert](http://docs.grafana.org/alerting/rules/) 直接先看結果. 
當 Server CPU 高於設定值, 則 send to [Slack](https://slack.com/)  一張 CPU screenshot. 
當 CPU 平均值降回正常, 則會再寄一張 CPU screenshot. ![](/assets/images/grafana-57.png) 

### 1\. 設定 Alert Notification 方法

開啟 Grafana -> Alerting -> Notification Channels 開啟一個新 Channel. 
選擇 Alert 平台, LINE, Slack, 或是 E-Mail ![](/assets/images/grafana-50.png) 我選擇 Slack, 輸入 slack words pace URL, Channel 名稱 和 token 即可完成.
![](/assets/images/grafana-61.png) 

按一下 Send test, Slack 收到一張測試用的圖片 

![](/assets/images/grafana-62.png)

### 2\. 設定 Alert Metrix

先找出一條想要的 rule 於 Prometheus 上, e.g. `100 - (avg by (instance) (irate(node_cpu{instance="SERVER_IP:9100",job="Benchmark server",mode="idle"}[5m])) * 100)` 
顯示出此伺服器 CPU idle 最後五分鐘使用量的百分比 

![](/assets/images/grafana-64-1024x683.png)
進入 Grafana Panel 點選 CPU->Edit->Metrix 挑選任意 Array , e.g. I . 放入剛使用的指令並儲存 
![](/assets/images/grafana-63-1024x233.png)

### 3\. 設定 Alert Rule

點選 CPU->Edit->Alert 來編輯 Alert Config 下圖顯示為預設設定值, 如果直接套用只會顯示 Error. 因為預設值並不能抓到後端正確值 
![](/assets/images/grafana-53-1024x838.png) 
此時須點選 query (A -> 會成我們編輯過的 Metrix -> Array e.g. I 應該就沒問題了. 點選 Test Rule **Firing = False, state = ok** 
![](/assets/images/grafana-65.png)
使 CPU 忙碌超過限值 **Firing  = True, state = alerting** 
![](/assets/images/grafana-54.png)

### 4\. Alert Notification 驗收

開啟 Slack, 驗收 CPU 忙碌時與回復正常值的圖 

![](/assets/images/grafana-58-1.png)  

### 5\. Note

*   最麻煩的地方大概就是找出各個適用的 Metrix 參數吧!
*   Alert Firing 和回復的圖示不是很明顯, 綠色/紅色 CPU 愛心 ...
*   Config 部分提供彈性非常大, 容易客製化
*   目前並非所有串接平台都支援 Image 接收, e.g. LINE. 不然好想用看看
