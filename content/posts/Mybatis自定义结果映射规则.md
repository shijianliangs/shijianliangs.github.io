---
title: "Mybatis自定义结果映射规则"
date: 2019-10-16
categories: ["java"]
tags: ["java","mybatis"]
draft: false 
---
## 问题
在实际业务处理规则中，数据库的列名和对象的属性名不一致如何处理呢？

## 解决方式
### 1.通过开启Mybatis配置文件开启自动驼峰命名规则
适用于满足A_COLUNM/aColumn的对应规则的

```xml
<setting name="mapUnderscoreToCamelCase" value="true"/>
```

### 2.自定义结果映射规则
针对不能满足A_COLUNM/aColumn的对应规则的

#### (1)普通自定义结果映射
```xml
<resultMap id="resultMap" type="com.study.mybatis.pojo.Student">
    <result column="student_name" property="studentName"/>
    <result column="age" property="age"/>
    <result column="gender" property="gender"/>
</resultMap>
```

#### (2)自定义级联结果映射
适用于查询结果包含多个对象级联的情况

##### 方式1：通过 '.'
```xml
<resultMap id="resultMap1" type="com.study.mybatis.pojo.Person">
    <result column="name" property="name"/>
    <result column="age" property="age"/>
    <result column="car_brand" property="car.brand"/>
    <result column="car_price" property="car.price"/>
</resultMap>
```
##### 方式2：通过 'association标签'
```xml
<resultMap id="resultMap2" type="com.study.mybatis.pojo.Person">
    <result column="name" property="name"/>
    <result column="age" property="age"/>
    <association property="car" javaType="com.study.mybatis.pojo.Car">
        <result column="car_brand" property="brand"/>
        <result column="car_price" property="price"/>
    </association>
</resultMap>
```
## 参考
[https://ke.qq.com/course/199779?taid=1162699186834531](https://ke.qq.com/course/199779?taid=1162699186834531)