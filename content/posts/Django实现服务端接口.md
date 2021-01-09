---
title: "Django实现服务端接口"
date: 2019-11-25
categories: ["python"]
tags: ["python","django","demo"]
draft: false 
---
## 为什么要学习Django？

* [软件测试人员该学习 Python 的七个理由](https://zhuanlan.zhihu.com/p/31805753)
* [Django](https://docs.djangoproject.com/)是当前Python世界里最负盛名且最成熟的Web框架

基于以上两点，决定学习下这个比较火的Python框架



## 安装配置

### 1. 安装Django

```bash
pip install Django
```

### 2. 新建Django项目

```bash
django-admin startproject demo
```

### 3. 创建应用和接口

新建 hello 应用

```bash
python manage.py startapp hello
```

应用创建成功后，在 demo 项目生成 hello 目录

```bash
hello
├── __init__.py
├── __pycache__
│   └── __init__.cpython-37.pyc
├── admin.py
├── apps.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```

在`views.py`创建接口，代码如下

```python
from django.http import JsonResponse


def hello(request):
    return JsonResponse({'code': 200, 'msg': 'hello', 'data': 'hello'})
```

将一个URL映射给此接口，在hello目录中新建一个`urls.py`文件，代码如下

```python
from django.urls import path
from . import views

urlpatterns = {
    path('hello', views.hello, name='hello')
}
```

在`demo/urls.py`中指定我们创建的 hello.urls 模块

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', include('hello.urls')),
]
```

### 4. 启动Django服务

```python
python manage.py runserver
-----------------------------
November 02, 2019 - 11:50:26
Django version 2.2.6, using settings 'demo.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-
```

### 5. 请求接口

```bash
~ » curl http://127.0.0.1:8000/hello/hello
{"code": 200, "msg": "hello", "data": "hello"}
```

这样一个最简单的接口就实现了



## 其他一些设置

### 1. 配置MySQL

* 安装pymysql数据库驱动

  ```bash
  pip install pymysql
  ```

* 配置Django中的DATABASE

  修改`settings.py`中的DATABASE

  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.mysql',    #数据库引擎
          'NAME': 'django_demo',  #数据库名
          'USER': 'root',   #账户名
          'PASSWORD': 'root', #密码
          'HOST': 'localhost', #主机
          'PORT': '3306', #端口
      }
  }
  ```

* 修改`_init_.py`

  ```python
  import pymysql
  
  pymysql.install_as_MySQLdb()
  
  TIME_ZONE = 'Asia/Shanghai'
  ```

* 执行数据迁移

  ```bash
  python manage.py makemigrations
  python manage.py migrate
  ```

  执行完成后，看到数据表新建成功

  ```bash
  mysql> show tables;
  +----------------------------+
  | Tables_in_django_demo      |
  +----------------------------+
  | auth_group                 |
  | auth_group_permissions     |
  | auth_permission            |
  | auth_user                  |
  | auth_user_groups           |
  | auth_user_user_permissions |
  | django_admin_log           |
  | django_content_type        |
  | django_migrations          |
  | django_session             |
  +----------------------------+
  10 rows in set (0.00 sec)
  ```

### 2. 获取Get参数

```python
def test_get(request):
    return HttpResponse('参数p1:' + request.GET['p1'] + ',参数p2:' + request.GET['p2'])
```

```bash
~ » curl http://127.0.0.1:8000/hello/test_get\?p1\=aaa\&p2\=bbb
参数p1:aaa,参数p2:bbb
```

### 3. 获取Post参数

```python
def test_post(request):
    return HttpResponse('参数p1:' + request.POST['p1'] + ',参数p2:' + request.POST['p2'])
```

```bash
~ » curl -d 'p1=mmm&p2=nnn' http://127.0.0.1:8000/hello/test_post      
参数p1:mmm,参数p2:nnn
```

### 4.获取application/json格式的Post参数

```python
def test_post_json(request):
    return JsonResponse(json.loads(request.body))
```

```bash
~ » curl -H "Content-Type:application/json" -X POST -d '{"p1":"mmm","p2":"nnn"}' http://127.0.0.1:8000/hello/test_post_json   
{"p1": "mmm", "p2": "nnn"}
```





## 遇到的问题

### 1. makemigrations报错1

django.core.exceptions.ImproperlyConfigured: mysqlclient 1.3.13 or newer is required; you have 0.9.3.

解决方式：`base.py`35、36 行注释版本校验

```python
version = Database.version_info
# if version < (1, 3, 13):
#    raise ImproperlyConfigured('mysqlclient 1.3.13 or newer is required; you have %s.' % Database.__version__)
```

### 2. makemigrations报错2

AttributeError: 'str' object has no attribute 'decode'

解决方式：`operations.py`146 行，把 decode 改成 encode 即可



## 参考

[https://docs.djangoproject.com/zh-hans/2.2/](https://docs.djangoproject.com/zh-hans/2.2/)

[https://segmentfault.com/a/1190000016049962](https://segmentfault.com/a/1190000016049962)

[https://blog.csdn.net/lijing742180/article/details/91966031](https://blog.csdn.net/lijing742180/article/details/91966031)

