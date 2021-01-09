---
title: "如何将自己的域名CNAME到github.io"
date: 2019-10-12
categories: ["other"]
tags: ["other"]
draft: false 
---
## 问题
将自己的域名CNAME到github.io

## 解决
1. 在`shijianliangs.github.io`的根目录下添加`CNAME`文件，写入你自己的域名

   > 注意这里只可以添加一个域名

   ```bash
   ~ » cat CNAME
   blog.shijianliang.cn
   ```

2. 域名解析配置

   ![image-20191016153006223](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016153006223.png)

3. github仓库设置

   勾选ENforce HTTPS，域名自动跳转https。最后出现红框里的 <font color="green">绿色</font> 的提示，则代表成功。

   ![image-20191016153122059](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016153122059.png)

