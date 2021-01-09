---
title: "shell脚本实现查询进程状态"
date: 2018-03-05
categories: ["linux"]
tags: ["linux","shell"]
draft: false 
---
```bash
#!/bin/bash

# 设置需要监控的进程名称
my_array=("Navicat" "QQ" "MWeb" "aaaaa" );

# 遍历监控的进程
for ((i=0; i < ${#my_array[*]}; i++))
do
    # 统计进程个数（需排除grep自身的查询进程）
    count=`ps -ef | grep "${my_array[i]}" | grep -v "grep" | wc -l`;
    if [ $count != 0 ];then
        # 绿色字体输出存活进程
        echo -e "\033[32m [Alive]    ${my_array[i]} \033[0m";
    else
        # 红色字体输出死亡进程
        echo -e "\033[31m [Dead]     ${my_array[i]} \033[0m";
    fi
done
```