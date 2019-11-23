---
categories:
  - Tools
tags:
  - Jenkins
  - Docker
  - Blue Ocean
  - CentOS 7
---
How to setup Jenkins + Docker + Blue Ocean 架設於 CentOS 7

安裝流程:

*   Docker >  Portainer  > Jenkins+Blue Ocean

## Install Docker CE Version[](https://docs.docker.com/engine/installation/linux/docker-ce/centos/#docker-ee-customers)

[Docker CE version](https://docs.docker.com/engine/installation/linux/docker-ce/centos/#docker-ee-customers)

```
yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum-config-manager --enable docker-ce-edge
yum-config-manager --enable docker-ce-test
yum install docker-ce 
systemctl start docker
```  

## Install Docker GUI - Portainer

[Portainer](https://portainer.io/install.html) 
```
docker run -d -p 9000:9000 --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data portainer/portainer
```
瀏覽器輸入 IP:9000 即可導入以下網頁 
![](/assets/images/jen-6.png) 

打算跑 Docker 與 Portainer 於同一台 Server 就選 Local 

![](/assets/images/jen-7.png) 

介面簡潔俐落 

![](/assets/images/jen-8-1024x363.png)

## Install Jenkins

透過 Docker 安裝 Jenkins + Blue OceImage 輸入 Image name: jenkinsci/blueocean 關閉 Access Control ![](/assets/images/jen-9-1024x473.png) 設定 Port:

*   Jenkins 網頁 Port 8080
*   Jenkins Port 5000 備用

設定 Volume:

*   Container(Bind)                          Host(Writable)
*   /var/run/docker.sock               /var/run/docker.sock
*   /var/jenkins_home                    /opt/jenkins

![](/assets/images/jen-10-1024x651.png) 瀏覽器輸入 IP:5000 ![](/assets/images/jen-1-1024x562.png) 如何取得 Jenkins Password?

1.  透過 IP:9000 連入方才建立的 Portainer
2.  點擊 Jenkins container > Console > Connect
3.  `cat /var/jenkins_home/secrets/initialAdminPassword`
4.  將密碼貼入並繼續執行

![](/assets/images/jen-11-1024x538.png) 選擇建議的套件安裝 ![](/assets/images/jen-2-1024x561.png) ![](/assets/images/jen-3-1024x559.png) 可以看到 Open Blue Ocean 於左列選項中 ![](/assets/images/jen-4-1024x428.png) ![](/assets/images/jen-5-1024x481.png) Follow 官方文件整體安裝算是簡單快速 UI 做的也都非常漂亮又不花俏 透過以上安裝可以讓每次生成的環境都相同
