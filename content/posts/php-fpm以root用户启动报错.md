---
title: "php-fpm以root用户启动报错"
date: 2019-03-24
categories: ["php"]
tags: ["php"]
draft: false 
---
## 报错如下

```bash
-bash-4.2# ./opt/remi/php73/root/usr/sbin/php-fpm
[21-Oct-2019 16:49:26] ERROR: [pool www] please specify user and group other than root
[21-Oct-2019 16:49:26] ERROR: FPM initialization failed
```

## 解决

启动添加`-R`参数

```bash
-bash-4.2# sudo ./opt/remi/php73/root/usr/sbin/php-fpm -R
```

