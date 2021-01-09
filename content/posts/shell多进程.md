---
title: "shell多进程"
date: 2019-07-05
categories: ["linux"]
tags: ["linux","shell"]
draft: false 
---
## echo.sh
```bash
#!/bin/bash
for (( i = 0; i < 10000; i++ )); do
    echo "process"${1}"的输出"${i};
done
```
## start.sh
```bash
#!/bin/bash
for (( i = 0; i < 5; i++ )); do
    ./echo.sh ${i} &
done
```

## 执行结果(摘取部分)
```
几个进程是并发执行的
...
process3的输出9896
process0的输出9641
process0的输出9642
process3的输出9897
process4的输出9876
process0的输出9643
process4的输出9877
process0的输出9644
process4的输出9878
process0的输出9645
process4的输出9879
process0的输出9646
process4的输出9880
process4的输出9881
process4的输出9882
process4的输出9883
process4的输出9884
...
```