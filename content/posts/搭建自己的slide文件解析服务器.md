---
title: "搭建自己的slide文件解析服务器"
date: 2019-10-08
categories: ["go"]
tags: ["go"]
draft: false 
---
## 1.安装golang
```bash
apt install golang
```
## 2.安装talksapp
```bash
go get github.com/golang/gddo/talksapp
```
## 3.下载google sdk并解压
```shell
wget https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-245.0.0-linux-x86_64.tar.gz
tar -zxvf google-cloud-sdk-245.0.0-linux-x86_64.tar.gz
```
## 4.执行自动安装程序
```bash
./google-cloud-sdk/install.sh
```
## 5.初始化
```bash
./google-cloud-sdk/bin/gcloud init
```
## 6.执行talksapp安装脚本
先进入子目录再执行安装，否则会报错
```bash
cd go/src/github.com/golang/gddo/talksapp/;./setup.sh
```
## 7.启动服务
```bash
google-cloud-sdk/bin/dev_appserver.py go/src/github.com/golang/gddo/talksapp/
```

这个时候就可以解析托管在github的.slide文件了

[https://www.shijianliang.cn/github.com/shijianliangs/gotalks/demo.slide](https://www.shijianliang.cn/github.com/shijianliangs/gotalks/demo.slide)

# 参考
[https://tonybai.com/2015/07/27/make-a-mirror-of-gotalks-appsport-app](https://tonybai.com/2015/07/27/make-a-mirror-of-gotalks-appsport-app)