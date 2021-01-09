---
title: "ubuntu+apache+php+mysql环境搭建"
date: 2018-08-05
categories: ["php"]
tags: ["php","ubuntu","apache"]
draft: false 
---
## 1. 安装apache2
```bash
apt-get install apache2
```
检查是否安装成功，浏览器输入服务器ip，出现下图即代表安装启动成功
![image-20191016131512869](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016131512869.png)

## 2. 安装php7.0
```bash
apt-get install php7.0
```
## 3. 安装apache的php7.0支持模块
```bash
apt-get install libapache2-mod-php7.0
```
## 4. 安装mysql-server
```bash
apt-get install mysql-server #过程会提示设置密码，正常设置即可
```
## 5. 校验mysql是否安装成功
```bash
mysql -u root -p #成功登录即可
```
## 6. 修改apache的php主目录
```bash
vim /etc/apache2/sites-available/000-default.conf
```
修改成/var/www
![image-20191016131608140](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016131608140.png)

## 7. 重启apache服务
```bash
service apache2 restart
```

## 8. 在/var/www写一个测试的脚本
index.php
```php
<?php
        echo "Hello World";
?>
```

## 9. Finish
![image-20191016131648901](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016131648901.png)