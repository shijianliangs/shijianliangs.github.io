---
title: "vuepress配置Valine评论插件"
date: 2018-08-19
categories: ["other"]
tags: ["vuepress","valine"]
draft: false 
---
## 1. 注册账号

前往[https://leancloud.cn/](https://leancloud.cn/)注册账号

## 2. 获取appId和appKey

路径 应用>设置>应用Keys

![image-20191021214132846](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191021214132846.png)

## 3.配置config.js

在themeConfig节点下配置自己Valine信息

```js
module.exports = {
    ......
    "themeConfig": {
        ......
        valineConfig: {
            appId: 'xxxxxxxxxxxxxxxxxxxxxxx',// your appId
            appKey: 'xxxxxxxxxxxxxxxxxxxxxxx', // your appKey
        }
    },
    ......
}
```

