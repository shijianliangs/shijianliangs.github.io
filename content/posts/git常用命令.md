---
title: "git常用命令"
date: 2019-04-21
categories: ["other"]
tags: ["git"]
draft: false 
---
## 初始化远程仓库
  ```bash
  git init;
  git remote add origin https://github.com/xxxx/xxx.git
  ```

## 强制覆盖本地分支
  ```bash
  git fetch --all
  git reset --hard origin/master 
  git pull
  ```

## 删除已在远程仓库的.ignore文件
  ```bash
  git rm -r --cached app/build #删除目录 
  git commit -m”rm app/build” 
  git push 
  # 然后再将需要新增的ignore文件加入.ignore中提交
  ```