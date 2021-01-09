---
title: "Django设置允许跨域请求"
date: 2019-12-16
categories: ["python"]
tags: ["python","django","cros"]
draft: false 
---
## 1. 安装django-cors-headers

```bash
pip install django-cors-headers
```

## 2. 修改`settings.py`文件

```python
# Step 1
INSTALLED_APPS = [
    ...
    'corsheaders'  # cors
]

# Step 2
MIDDLEWARE = [
    ...
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',
    ...
	  # 'django.middleware.csrf.CsrfViewMiddleware',
]

# Step3
ALLOWED_HOSTS = [
    '*',
]
CORS_ALLOW_CREDENTIALS = True
CORS_ORIGIN_ALLOW_ALL = True
CORS_ALLOW_HEADERS = ('*')
```

