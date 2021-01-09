---
title: "caddy+php环境搭建"
date: 2019-03-03
categories: ["php"]
tags: ["php","caddy"]
draft: false 
---
## 什么是caddy？
[Caddy服务器（或称Caddy Web）是一个开源的，使用 Golang 编写，支持 HTTP/2 的 Web 服务端。它使用 Golang 标准库提供 HTTP 功能。](https://zh.wikipedia.org/wiki/Caddy)

## caddy的特性
![image-20191016103202895](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016103202895.png)

## caddy的部署
### 1.安装php
```bash
brew install php@7.2
```

### 2.安装caddy
```bash
curl https://getcaddy.com | bash -s personal
```

### 3.配置Caddy文件
Caddyfile
```bash
# 域名解析方式
# caddy会自动帮助申请证书，可以https访问，无需配置
www.1019.fun {
    root /home/ubuntu/www.1019.fun
    log /home/ubuntu/www.1019.fun/access.log
    errors /home/ubuntu/www.1019.fun/errors.log
    
    # PHP-FPM Configuration for Caddy
    fastcgi / localhost:9000 php
}
# ip方式
:9001 {
    root /Users/shijl/GitBook/Library/Import/gbook1/_book
    log /Users/shijl/Downloads/gbook1_access.log
    errors /Users/shijl/Downloads/gbook1_errors.log

    # PHP-FPM Configuration for Caddy
    fastcgi / localhost:9000 php
}
```

### 4.启动caddy
在Caddyfile文件目录下启动
```bash
caddy
```

## 官方网址
[https://caddyserver.com](https://caddyserver.com)

