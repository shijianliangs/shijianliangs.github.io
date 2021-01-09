---
title: "mac安装php的redis插件"
date: 2019-09-07
categories: ["php"]
tags: ["php","mac"]
draft: false 
---
## mac安装php的redis插件
执行连接redis的操作遇到报错:
```
Fatal error</b>:  Uncaught Error: Class 'RedisCluster' not found in...
```

### 安装    
1. 下载php-redis
    ```
    curl -O https://nodeload.github.com/nicolasff/phpredis/zip/master
    ```
2. 解压
    ```
    unzip phpredis-master.zip && cd phpredis-master
    ```
3. 动态安装
    ```
    phpize
    ```
4. 编译
    ```
    ./configure
    ```
5. 安装
    ```
    make && make install
    ```
6. 修改`php.ini`,插入:
    ```
    extension=redis.so
    ```
7. 重启php-fpm
8. 查看是否安装成功
    ```
    shijl:7.4 shijl$ php -m | grep redis
    redis
    ```

### 参考：
[https://panxu.net/article/8400.html](https://panxu.net/article/8400.html)