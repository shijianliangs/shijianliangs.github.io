---
title: "proxychains让你的terminal健步如飞"
date: 2019-10-15
categories: ["mac"]
tags: ["mac","proxychains"]
draft: false 
---
## 安装前
```bash
shijl:~ shijl$ wget www.google.com
--2019-06-20 11:29:15--  http://www.google.com/
Resolving www.google.com (www.google.com)... 69.171.248.128
Connecting to www.google.com (www.google.com)|69.171.248.128|:80... failed: Operation timed out.
```
## 安装
```bash
brew install proxychains-ng
```
## 配置
编辑`/usr/local/etc/proxychains.conf`文件,最后一行添加
```bash
socks5  127.0.0.1 1080
```

## 测试
```bash
shijl:~ shijl$ proxychains4 wget www.google.com
[proxychains] config file found: /usr/local/etc/proxychains.conf
[proxychains] preloading /usr/local/Cellar/proxychains-ng/4.14/lib/libproxychains4.dylib
[proxychains] DLL init: proxychains-ng 4.14
--2019-06-20 11:37:50--  http://www.google.com/
Resolving www.google.com (www.google.com)... 224.0.0.1
Connecting to www.google.com (www.google.com)|224.0.0.1|:80... [proxychains] Strict chain  ...  127.0.0.1:1080  ...  www.google.com:80  ...  OK
connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: ‘index.html’

index.html                                                              [ <=>                                                                                                                                                                ]  11.91K  --.-KB/s    in 0s

2019-06-20 11:37:51 (42.8 MB/s) - ‘index.html’ saved [12194]
```

## 其他
有的机器无法启动命令，需至恢复模式执行
```bash
csrutil disable
```