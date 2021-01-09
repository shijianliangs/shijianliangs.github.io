---
title: "ubuntu+nginx+php+mysql环境搭建"
date: 2018-03-07
categories: ["php"]
tags: ["php","ubuntu","nginx"]
draft: false 
---
## 1. 安装nginx
```bash
apt-get install nginx
```
检查是否安装成功，浏览器输入服务器ip，出现下图即代表安装启动成功
![image-20191016131424150](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016131424150.png)

## 2. 安装php7.0-fpm
```bash
apt-get install php7.0-fpm
```
## 3. 启动php7.0-fpm
```bash
service php7.0-fpm restart
```
## 4. 安装mysql-server
```bash
apt-get install mysql-server #过程会提示设置密码，正常设置即可
```
## 5. 校验mysql是否安装成功
```bash
mysql -u root -p #成功登录即可
```
## 6. 修改nginx配置
```bash
vim /etc/nginx/sites-enabled/default
```
```bash
server {
    listen 80;
    listen [::]:80;

    # listen [::]:443 ssl http2;
    # listen 443 ssl http2;

    # include ssl.conf;
    # ssl_certificate /path/to/crt;
    # ssl_certificate_key /path/to/key;

    root /var/www;
    index index.html index.htm index.php;

    server_name server_domain_or_IP;

    location / {
        try_files $uri $uri/ =404;
    }

    location /phpmyadmin {
       index index.php;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

## 7. 重启nginx
```bash
service nginx restart
```
## 8. 在/var/www写一个测试的脚本
index.php
```php
<?php
        echo "Hello World";
?>
```

## 9. Finish
![image-20191016131308029](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016131308029.png)