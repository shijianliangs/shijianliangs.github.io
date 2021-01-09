---
title: "pymysql常用操作"
date: 2019-08-27
categories: ["python"]
tags: ["python","mysql"]
draft: false 
---
## 安装
```python
pip  install pymysql
```

## Demo
```python
import pymysql


def test():
    # 新建连接
    connection = pymysql.connect(host = 'localhost', port = 3306, user = 'root', password = 'root',
                                 database = 'django_demo', charset = 'utf8')
    connection.autocommit()  # 开启自动commit
    cursor = connection.cursor(cursor = pymysql.cursors.DictCursor)  # cursor = pymysql.cursors.DictCursor用来指定按键值对返回查询结果

    # 查询
    cursor.execute('SELECT * FROM django_content_type LIMIT 1000')
    ones = cursor.fetchall()
    print(ones)

    # 插入
    cursor.execute('insert xxx (...) values (...)')
    # 若不开启自动commit，则每个除查询的之外的操作都需要单独commit
    connection.commit()

    # 关闭连接
    connection.close()

```