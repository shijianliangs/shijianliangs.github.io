---
title: "centos开放端口"
date: 2017-09-07
categories: ["linux"]
tags: ["linux","centos"]
draft: false 
---
```bash
firewall-cmd --zone=public --add-port=2018/tcp --permanent
firewall-cmd --reload
```