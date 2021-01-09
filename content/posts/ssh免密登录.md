---
title: "ssh免密登录"
date: 2018-09-19
categories: ["linux"]
tags: ["ssh","linux"]
draft: false 
---
1. 生成公钥

   ```bash
   ssh-keygen
   ```

2. 仅需将机器A的ssh公钥文件安装到机器B上，在机器A的终端执行

   ```
   ssh-copy-id user@xxx.xxx.xxx.xxx
   ```

3. 之后从机器A登录机器B，就无需再输入密码了

   ```
   ssh user@xxx.xxx.xxx.xxx
   ```

