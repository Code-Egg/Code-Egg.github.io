---
categories:
  - Web Server
tags:
  - Feature
  - QUIC
---
在不需要任何修改的情況下就能提升 15% 以上的訪問速度 一般使用者基本上不太會考慮 QUIC [如何運作](https://read01.com/KLDM2J.html#.Wvn_e2gvxPY), [原理分析](https://hk.saowen.com/a/6f10e438e5b799cbfb715d085382adb1d6b7ff1c90031ef86f08f90f01f5e08f)...等等 本篇只介紹 **如何使用**. 目前已知 Web Server 支援 QUIC 功能的僅 LSWS Enterprise Version. 有興趣也可參與   [LiteSpeed QUIC Client Library](https://github.com/litespeedtech/lsquic-client)    from GitHub

### 如何使 QUIC 工作

1.  Running with LSWS
2.  HTTPS 使用合法憑證
3.  允許 UDP port 443

### 如何確認 UDP port 443

1.  確認 UDP 443 port 開啟

```
netstat -lupn | grep 443
```

2.  確認 UDP 443 出server
```
 nc -v -u your_server_ip 443
```
3.  確認 UDP 443 進 server
```
 nc -v -u www.google.com 443
```
### 如何確認 QUIC 工作

1.  確認標頭

```
alt-svc:quic=":443"; v="39,43,46", or "h3-Q046=":443""
```

2.  確認 QUIC 連線狀態
```
 chrome://net-internals/#quic
```
3.  用 Chrome extension 確認 ![](/assets/images/quic-1-300x131.png)

### Note

如果使用其它非支援 QUIC 的 Proxy 或是 CDN 將導致 QUIC 協定失效
