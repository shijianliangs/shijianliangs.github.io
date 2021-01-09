---
title: "mac的charles抓包"
date: 2020-04-11
categories: ["mac"]
tags: ["mac","charles"]
draft: false 
---
## 1.Mac端查看代理机IP & 端口

查看路径

Help>SSL Proxying>Install Charles Certificate on a Mobile Device or Remote Browser

![image-20191016130817726](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016130817726.png)

如下图查看到的代理机的ip:端口为`172.17.106.135:8888`
![image-20191016130842535](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016130842535.png)

## 2. Mac端设置抓取https
查看路径Proxy->SSL Proxy Settings->Add

Host：填*表示所有网站都抓

Port：443
## 3. 手机连接代理机同一局域网并设置好代理
## 4. 手机安装证书

浏览器访问`chls.pro/ssl`,安装证书
## 5.成功

证书安装成功后即可抓取手机的https请求