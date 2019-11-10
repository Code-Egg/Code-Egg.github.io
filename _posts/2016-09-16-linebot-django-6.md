---
categories:
  - Scripting
tags:
  - Python
  - Linebot
---

**LINE BOT Message 初學者記錄(六) ** 

**Only $2.5 build LINE BOT platform** Due to RHC Openshift v2 platform going to closed on 9/30/2017\. 
只好租個每月 $2.5 美金的 VPS-[Vultr](https://www.vultr.com/). 選它的理由不外乎價位比較便宜且 bot 非商業用途, 硬體需求低. 

**$2.5 Vultr Plan Spec:**

*   20GB SSD
*   1 CPU
*   512MB Memory
*   500GB Bandwidth

**Setup:**

*   OS: CentOS 7
*   WebServer: OpenLiteSpeed
*   WSGI Server: Gunicorn
*   Language: Python3
*   Domain: Free source
*   SSL: Let's Encrypt

### Step1 - Create VPS and install OS:

Create vultr account then deploy the plan you want. Choose server with CentOS 7x64

You will get server IP and password from overview page

### Step2 - Install free web server:

```
yum update -y
rpm -ivh http://rpms.litespeedtech.com/centos/litespeed-repo-1.1-1.el7.noarch.rpm
yum install openlitespeed -y
```

### Step3 - Install Py3 and Django:
```
yum -y install https://centos7.iuscommunity.org/ius-release.rpm
yum -y install python36u python36u-devel
yum -y install python36u-pip
pip3.6 install django
django-admin startproject Djangoproject
python3.6 manage.py startapp trips
```

### Step4 - Install Gunicorn:
```
pip3.6 install gunicorn
```

#### Create three files for gunicorn setup:
```
cat <<EOF>> /etc/systemd/system/gunicorn.socket
Description=gunicorn socket
[Socket]
ListenStream=127.0.0.1:5003
[Install]
WantedBy=sockets.target
EOF

cat <<EOF>> /etc/systemd/system/gunicorn.service
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target
[Service]
PIDFile=/run/gunicorn/pid
User= root
Group=root
RuntimeDirectory=gunicorn
WorkingDirectory=/root/Djangoproject
ExecStart=/usr/bin/gunicorn --pid /run/gunicorn/pid   \
            --bind 127.0.0.1:5003 trips.wsgi
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s TERM $MAINPID
PrivateTmp=true
[Install]
WantedBy=multi-user.target
EOF

cat <<EOF>> /etc/tmpfiles.d/gunicorn.conf
d /run/gunicorn 0755 root root -
EOF

systemctl start gunicorn.socket
```

### Step5 - Web Server Settings:

**WebAdmin > Listensers**

1.  One Listener for port 80, the other one for 443
2.  Both listeners add "Virtual Host Mappings" with $your_domain
3.  **After Step6 setup**, you need to add SSL Key&Cert for port 443

*   Private Key:  <span style="background-color: #eeeeee;">/etc/letsencrypt/live/$your_domain/privkey.pem</span>
*   Certificate: <span style="background-color: #eeeeee;">/etc/letsencrypt/live/$your_domain/cert.pem</span>
*   CA Certificate: <span style="background-color: #eeeeee;">/etc/letsencrypt/live/$your_domain/chain.pem</span>

**WebAdmin > Server Configuration > External App > Add a "Web Server"** Name: _**gunicorn**_ Address:**_127.0.0.1:5003_** Max Connections:_**100**_ Initial Request Timeout: _**60**_ Retry Timeout: _**0**_ **WebAdmin console > Configuration > Virtual Hosts > "Virtual Host Name" > Rewrite** Rewrite set to **Yes** **<span style="background-color: transparent; color: black; font-family: 'arial'; font-size: 11pt; font-style: normal; font-variant: normal; font-weight: 400; text-decoration: none; vertical-align: baseline; white-space: pre-wrap;">Rewrite</span> **Rules: <span style="background-color: #eeeeee;">RewriteCond %{ORG_REQ_URI} !/static</span> <span style="background-color: #eeeeee;">RewriteRule ^/(.*)$ http://gunicorn/$1 [P]</span></div>

### Step6 - Apply for free Domain and SSL:

I choose [NCTU.me](https://nctu.me/) as my domain hosting, it's free, immediately effect, easy to use than e.g. [HE](https://dns.he.net/) I choose Let's encrypt - [certbot](https://certbot.eff.org/) as my SSL, it's free and LINE accept it, easy to use and popular. Choose "None of the above" on "CentOS 7" Let's Encrypt Install:

```
yum -y install yum-utils
yum-config-manager --enable rhui-REGION-rhel-server-extras rhui-REGION-rhel-server-optional
yum install certbot
certbot certonly
```

1.  Enter number
2.  Enter webroot /usr/local/lsws/Example/html
3.  Enter your domain name


### Step7 - WebHook:

[Line Developer](https://developers.line.me/) change your Webhook URL and click VERIFY

That's it

Welcome forward with cite source
