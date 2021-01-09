---
title: "记录一次http升级https"
date: 2020-06-20
categories: ["other"]
tags: ["http"]
draft: false 
---
## 问题
![image-20191016103452344](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016103452344.png)

解决如图问题。ps:我的是 Nginx 服务器。

## 解决

### 1. 腾讯云申请一个免费的SSL证书

[https://buy.cloud.tencent.com/ssl?fromSource=ssl](https://buy.cloud.tencent.com/ssl?fromSource=ssl)
![image-20191016103521168](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016103521168.png)

接下来等待审核

等了大概20分钟，速度还是很快的...

### 2. 下载证书并上传服务器

注意下载的压缩包解压出来，只是用Nginx的

### 3. 配置Nginx
![image-20191016103549433](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016103549433.png)

### 4. 重启Nginx

## 成功
![image-20191016103615220](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016103615220.png)

## 参考
[https://cloud.tencent.com/document/product/400/35244](https://cloud.tencent.com/document/product/400/35244)