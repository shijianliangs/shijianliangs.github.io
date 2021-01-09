---
title: "ubuntu安装haproxy加速"
date: 2017-10-28
categories: ["other"]
tags: ["haproxy"]
draft: false 
---
## 1. 下载 haproxy
```bash
sudo apt-get install haproxy
```

## 2. 配置 haproxy
打开`/etc/haproxy/haproxy.cfg`文件，删除原有内容。新增以下配置：
```bash
global
        ulimit-n  51200

defaults
        log global
        mode    tcp
        option  dontlognull
        contimeout 1000
        clitimeout 150000
        srvtimeout 150000

frontend ss-in
        bind *:8388 #加速服务器端口
        default_backend ss-out

backend ss-out
        server server1 111.112.113.114:2222 maxconn 20480 #ss服务器ip、端口
```
## 3. 启动 haproxy
```bash
sudo service haproxy restart
```



SS客户端连接加速服务器的ip，其他与直接连SS服务器配置一致

