---
title: "mac的launchpad设置"
date: 2020-04-06
categories: ["other"]
tags: ["mac","launchpad"]
draft: false 
---
## 设置 Launchpad 列数

```bash
defaults write com.apple.dock springboard-columns -int X
```

## 设置 Launchpad 行数

```bash
defaults write com.apple.dock springboard-rows -int Y
```

## 设置之后需要重启

```bash
killall Dock
```