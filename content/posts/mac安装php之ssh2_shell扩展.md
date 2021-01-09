---
title: "mac安装php之ssh2_shell扩展"
date: 2020-01-14
categories: ["php"]
tags: ["ssh2_shell"]
draft: false 
---
## 问题

```bash
Error : Class 'ssh2_connect' not found
```

## 通过源码安装

```bash
wget https://pecl.php.net/get/ssh2-1.1.2.tgz
tar -zxvf ssh2-1.1.2.tgz
cd ssh2-1.1.2
phpize
./configure --with-ssh2
make
make install
```

## 配置php.ini

```
extensions=ssh2.so
```

## 校验

```bash
~ » php -m | grep ssh2                                                                                                                                                                              ssh2
```

