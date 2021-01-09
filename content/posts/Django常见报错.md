---
title: "Django常见报错"
date: 2018-07-29
categories: ["python"]
tags: ["python","django"]
draft: false 
---
* In order to allow non-dict objects to be serialized
```python
return JsonResponse('aaa')
```
修改为
```python
return JsonResponse('aaa', safe = False)
```

* You called this URL via POST, but the URL doesn't end in a slash and you have APPEND_SLASH set
请求的url最后带上`/`


