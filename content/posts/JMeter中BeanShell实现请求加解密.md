---
title: "JMeter中BeanShell实现请求加解密"
date: 2018-12-09
categories: ["test"]
tags: ["test","jmeter","beanshell"]
draft: false 
---
## 1. 获取请求数据进行加密

```java
import org.apache.jmeter.config.*;   
import org.apache.jmeter.protocol.http.sampler.*;
import java.util.*;

//获取加密前的数据
Arguments arguments =  sampler.getArguments();
Argument argument = arguments.getArgument(0);
String decrypt_data = argument.getValue();

//加密
String encrypt_data = encrypt(decrypt_data);

//将加密好的数据重新设置到参数
argument.setValue(encrypt_data);
```



## 2. 获取响应数据进行解密

```java
import com.alibaba.fastjson.*;
import java.util.*;

//获取响应的值
String response=new String(prev.getResponseData(),"UTF-8");

//解密
String decrypt_response = decrypt(response);

//将解密好的数据重新设置到响应
prev.setResponseData(decrypt_response);
```

