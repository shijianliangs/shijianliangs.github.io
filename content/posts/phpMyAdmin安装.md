---
title: "phpMyAdmin安装"
date: 2018-02-02
categories: ["php"]
tags: ["php","phpmyadmin"]
draft: false 
---
## 1. phpMyAdmin官网下载
[https://www.phpmyadmin.net/downloads](https://www.phpmyadmin.net/downloads)

或者直接下载到/var/www
```bash
wget https://files.phpmyadmin.net/phpMyAdmin/4.8.5/phpMyAdmin-4.8.5-all-languages.tar.gz
```
## 2. 解压
```bash
tar -zxvf phpMyAdmin-4.8.5-all-languages.tar.gz
```
## 3. 删除压缩包
```bash
rm phpMyAdmin-4.8.5-all-languages.tar.gz
```
## 4. 改名
```bash
mv phpMyAdmin-4.8.5-all-languages phpmyadmin
```
## 5. 配置
```bash
cd phpmyadmin;mkdir tmp;chmod 777 tmp
```

## 6. 服务器访问

```bash
http://xxx.xxx.xxx.xxx/phpmyadmin
```

