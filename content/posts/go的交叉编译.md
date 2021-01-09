---
title: "go的交叉编译"
date: 2020-01-23
categories: ["go"]
tags: ["go"]
draft: false 
---
## linux 64-bit
```bash
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build xxx.go
```
## windows 64-bit
```bash
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build xxx.go
```
## mac 64-bit
```bash
CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build xxx.go
```

## 参考
[https://blog.csdn.net/panshiqu/article/details/53788067](https://blog.csdn.net/panshiqu/article/details/53788067)