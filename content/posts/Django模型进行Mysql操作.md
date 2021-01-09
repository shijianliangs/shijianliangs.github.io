---
title: "Django模型进行Mysql操作"
date: 2020-04-18
categories: ["python"]
tags: ["python","django","mysql"]
draft: false 
---
```python
# 模型类
class Student(models.Model):
	id = models.AutoField(primary_key = True)
	name =  models.CharField(max_length = 32)
	age = models.IntegerField(blank = True)

# 增
stu = Student(name = 'Bob', age = 10)
stu.save()

# 删
Student.objects.filter(name = 'Bob').delete()

# 改
Student.objects.filter(name = 'Bob').update('age' = 12)

# 查
Student.objects.filter(name = 'Bob')

```