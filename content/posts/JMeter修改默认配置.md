---
title: "JMeter修改默认配置"
date: 2019-06-29
categories: ["test"]
tags: ["test","jmeter"]
draft: false 
---
## 1. 修改默认语言

修改`jmeter.properties`文件，将 #language=EN 修改成 language=zh_CN，重启

## 2.修改默认内存

修改启动文件`jmeter`

```
: "${HEAP:="-Xms2g -Xmx4g -XX:MaxMetaspaceSize=2560m"}"
```



