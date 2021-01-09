---
title: "scp"
date: 2018-05-01
categories: ["linux"]
tags: ["linux","scp"]
draft: false 
---
用于Linux之间复制文件和目录。（需要有对应的读写权限）
## 复制本地文件到远程服务器
```bash
scp /local_path/local_file.txt remote_user@remote_ip:/remote_path/
```

## 复制本地文件夹到远程服务器
```bash
scp -r /local_path/local_dir/ remote_user@remote_ip:/remote_path/
```

## 复制远程文件到本地
```bash
scp remote_user@remote_ip:/remote_path/remote_file.txt /local_path/
```

## 复制远程文件夹到本地
```bash
scp -r remote_user@remote_ip:/remote_path/remote_dir/ /local_path/
```