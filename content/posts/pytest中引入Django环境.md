---
title: "pytest中引入Django环境"
date: 2020-04-10
categories: ["python"]
tags: ["python","pytest"]
draft: false 
---
常常在执行pytest单元测试的时候，找不到module，是因为没有引入Django的环境变量。需要单独引入，方法如下：

```python
import os
import django


def test():
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'your_project.settings')
    django.setup()
    from xxx.xxx import xxx

```