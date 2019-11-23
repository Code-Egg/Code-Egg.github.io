---
categories:
  - Tools
tags:
  - CodiMD
  - docker
---

Quick install Codimd locally in few commands

## Install Docker

```
curl -fsSL https://get.docker.com/ | sh
systemctl start docker
systemctl enable docker
usermod -aG docker root
```

## Install <span class="pl-c1">docker-compose</span>
```
curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
## Install CodiMD
````
git clone https://github.com/hackmdio/codimd-container.git 
cd codimd-container 
docker-compose up
```
## <span class="pl-c1">Change Port from 3000 to 80(HTTP)</span>
```
sed -i -r 's/"3000:3000"/"80:3000"/g' codimd-container/docker-compose.yml
```
### <span class="pl-c1">Run with production mode</span>
```
docker-compose up -d
````
## View CodiMD with your hostname

![](/assets/images/codi-1024x696.png)
