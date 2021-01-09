---
title: "caddy权限控制"
date: 2018-05-08
categories: ["other"]
tags: ["caddy"]
draft: false 
---
编辑Caddyfile
```bash
:9001 {
    root		/Users/shijl/book/public/
    log			/Users/shijl/Downloads/9001_access.log
    errors 	/Users/shijl/Downloads/9001_errors.log
    basicauth test test {
        realm name
        /
    }
}
```
效果
![image-20191016102937670](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016102937670.png)