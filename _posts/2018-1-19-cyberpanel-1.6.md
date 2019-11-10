---
categories:
  - Web Server
tags:
  - OpenLiteSpeed
  - CyberPanel
---
After introducing the concepts of Web Server Software & hosting control panel, we are moving on to hands on and build our very first web server using an open source software, OpenLiteSpeech, and control panel, CyberPanel. The first thing to get started is to get a server. Here I purchase a CentOS server over Vultr. Vultr is handy because I can get a server on demand and the rate is very good. Once I get the server up and running, let's see how I can quickly deploy the web server using CyberPanel. Cyberpanel website has prepared a document teaching the installation. After checking the requirements, my vultr CentOS server ($5 plan) is ready to go. Remember, for your first time to login as a root user, change password using `passwd`. Then, enter the following commands to start installation
```
wget http://cyberpanel.net/install.tar.gz
tar zxf install.tar.gz
cd install
chmod +x install.py
python install.py [IP Address]
```
`wget` lets you to download the installation image from cyberpanel.net. 
After decompress `tar zxf`, use `python` to run the install script.  
The installation then will start and complete in about 10 mins. 
After successfully installed, CyberPanel is available for access on port 8090. 
Login page will be like below.( currently support 6 languages including English, Chinese and Japanese) 
![](/assets/images/Screen-Shot-2018-01-18-at-8.22.32-PM.png)   
The main page after logging displays a summary of real-time usage and HTTP Statistics. 
![](/assets/images/Screen-Shot-2018-01-18-at-8.27.12-PM-1024x624.png) 
In addition to monitoring webserver's status, CyberPanel also features website creation and even 1 click install wordpress with LiteSpeechCache. Here I will walk you through 1 click install wordpress with LSCache.
 ![](/assets/images/Screen-Shot-2018-01-18-at-8.54.18-PM-1024x624.png)

1.  Expand panel on the left and under 'MAIN' find 'Websites'. Click 'Create Website'

![](/assets/images/Screen-Shot-2018-01-18-at-8.56.37-PM-1024x624.png) 

2\. Select or enter fields in the website setting as the screenshot, but please note that in Domain Name, 
you should not include 'WWW.', but have to follow the format "example.com". 
Once new website being created, go to 'List Websites'. 
Click the icon under 'Launch' to enter the website's control panel. 
![](/assets/images/Screen-Shot-2018-01-18-at-9.03.14-PM-1024x616.png) 

The created website's control panel shows operation information regarding to this website. 

![](/assets/images/Screen-Shot-2018-01-18-at-9.04.50-PM-1024x624.png) 

Scroll down and you will find "WORDPRESS WITH LSCACHE" under APPLICATION INSTALLER.
 Click and you will be asked to decide 'Path' for Wordpress installation. 
 I will leave empty to use home directory, and click "Install Wordpress". 
 ![](/assets/images/Screen-Shot-2018-01-18-at-9.05.46-PM-1024x624.png) 
 
 At first, you may get this error message if you forget to clean up the install directory. 
 That means the installation of Wordpress has failed and you need to go to FILE MANAGER to empty the folder. 
 ![](/assets/images/Screen-Shot-2018-01-21-at-10.30.18-AM.png)   
 
 'FILE MANAGER' should be just above APPLICATION INSTALLER. 
 Click to enter, and you will see by default two folders have been created, and 'public_html' is the one we want to delete. 
 
 ![](/assets/images/Screen-Shot-2018-01-21-at-10.42.27-AM.png) 
 
 Once delete, the installation can be successfully completed. 
 The message also indicates that the hostname is now available to complete the wordpress setup. 
 
 ![](/assets/images/Screen-Shot-2018-01-21-at-10.44.35-AM.png) 
 
 Entering the website hostname, for example, `wjtest.cyber.com` in the browser, and then you will be automatically redirected to wordpress setup. 
 
 ![](/assets/images/Screen-Shot-2018-01-21-at-10.49.29-AM.png)
 
 That is it! You have used CyberPanel + LSCache to complete installation of webserver, OpenLiteSpeed, and Wordpress. 
 
 Very good job!   
 
 
 ** TIPS **
 Above walk through assume you have registered your host domain name in internet domain registrar, like GoDaddy, etc.
 But if you have not yet, and just want to play around with CyberPanel. 
 
 You will be faced with situation as below. 
 Because even though you installed the webserver using the host domain name, that does not mean you really own the host domain name and nobody really recognize that host domain name. 
 
 ![](h/assets/images/Screen-Shot-2018-01-21-at-11.01.35-AM.png) 
 
 But to test if the webserver really works, you can fool your computer to recognize that hostname and redirect that to your server IP address by adding `[Server IP addr] [Host domain name]` to `/etc/hosts`. 
 
 ![](/assets/images/Screen-Shot-2018-01-21-at-11.07.21-AM-1.png)
