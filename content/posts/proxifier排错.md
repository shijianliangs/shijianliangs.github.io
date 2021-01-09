---
title: "proxifier排错"
date: 2019-08-19
categories: ["other"]
tags: ["proxifier"]
draft: false 
---
## 环境

SSH Tunnel + Proxifier



## 报错

```bash
ssh root@192.168.1.5
ssh_exchange_identification: read: Connection reset by peer
```



## 解决

Proxifier 中配置了所有 Applications 都走代理，未排除 SSH Tunnel，导致ssh连接错误

新增 rule，让SSH Tunnel直接连接，不走代理

![image-20191113170940955](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191113170940955.png)