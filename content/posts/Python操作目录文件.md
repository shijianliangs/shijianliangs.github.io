---
title: "Python操作目录文件"
date: 2019-01-28
categories: ["python"]
tags: ["python"]
draft: false 
---
* 遍历目录下所有以`.log`结尾的文件，并输出文件的全路径
```python
import glob

file_dict = glob.glob('/Users/shijl/Downloads/*.log')
print(file_dict)
"""
输出结果:
['/Users/shijl/Downloads/2018_access.log', '/Users/shijl/Downloads/2018_error.log']
"""

for file in file_dict:
	print(file)
"""
输出结果:
/Users/shijl/Downloads/2018_error.log
/Users/shijl/Downloads/2018_access.log
"""
```

* 获取文件属性
```python
import os
# 获取文件创建时间戳
print(os.path.getctime('/Users/shijl/Downloads/2018_access.log'))
"""
输出结果:
1576662925.199362
"""

# 获取文件修改时间戳
print(os.path.getmtime('/Users/shijl/Downloads/2018_access.log'))
"""
输出结果:
1576662925.199362
"""
```