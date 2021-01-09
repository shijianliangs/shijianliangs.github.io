---
title: "Python常用字符串操作"
date: 2019-12-01
categories: ["python"]
tags: ["python"]
draft: false 
---
* 切割字符串
```python
a = 'a/b/c/d/e/f'
a_dict = a.split('/') 
print(a_dict)
# 执行结果:['a', 'b', 'c', 'd', 'e', 'f']
```