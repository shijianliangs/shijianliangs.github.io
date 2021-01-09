---
title: "Mybatis全局配置文件的常用配置"
date: 2019-02-07
categories: ["java"]
tags: ["java","mybatis"]
draft: false 
---
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <!-- 引用配置文件 -->
    <properties resource="mybatis/jdbc.properties"/>

    <!-- 设置 -->
    <settings>
        <!-- 是否开启自动驼峰命名规则（camel case）映射，即从经典数据库列名 A_COLUMN 到经典 Java 属性名 aColumn 的类似映射。（默认false）-->
        <setting name="mapUnderscoreToCamelCase" value="true"/>

        <!-- 全局地开启或关闭配置文件中的所有映射器已经配置的任何缓存（默认true） -->
        <setting name="cacheEnabled" value="true"/>

        <!-- 设置超时时间，它决定驱动等待数据库响应的秒数。(默认null) -->
        <setting name="defaultStatementTimeout" value="10"/>
		
		<!--
            懒加载：
			aggressiveLazyLoading 或 collection 在进行分步查询时，
            若使用到级联对象的属性，则进行查询
            若未使用到级联对象的属性，则不进行查询
         -->
        <setting name="lazyLoadingEnabled" value="true"/>
        <setting name="aggressiveLazyLoading" value="false"/>
    </settings>

    <!-- 别名,别名不区分大小写 -->
    <typeAliases>
        <!-- 别名: 默认 alias = 类名小写 ，也可自定义-->
        <typeAlias type="com.study.mybatis.pojo.Student" alias="Student"/>

        <!-- 批量起别名: 为当前包下的每一个类都起一个默认的别名 -->
        <!-- 批量起别名: 可以使用@Alias标签为某个类型制定新的别名 -->
        <package name="com.study.mybatis.pojo"/>
    </typeAliases>

    <!-- environments:配置多个环境，default 指定默认使用哪个环境 -->
    <environments default="default">

        <!-- environment: 配置一个具体的环境信息，必须有 transactionManager 和 dataSource 两个标签 -->
        <environment id="default">

            <!-- 事务管理器: JDBC|MANAGED -->
            <!-- 如果你正在使用 Spring + MyBatis，则没有必要配置事务管理器， 因为 Spring 模块会使用自带的管理器来覆盖前面的配置。 -->
            <transactionManager type="JDBC"/>

            <!-- 数据源 -->
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>

    <!-- 配置 Mappers -->
    <mappers>

        <!-- 使用相对于类路径的资源引用 -->
        <mapper resource="mybatis/mapper/StudentMapper.xml"/>

        <!-- 使用完全限定资源定位符（URL） -->
        <mapper url="file:///Users/shijl/IdeaProjects/study/study-spring/src/main/resources/mybatis/mapper/StudentMapper.xml"/>

        <!-- 使用映射器接口实现类的完全限定类名 -->
        <mapper class="com.study.mybatis.dao.StudentMapper"/>

        <!-- 将包内的映射器接口实现全部注册为映射器 -->
        <package name="com.study.mybatis.dao"/>
    </mappers>
</configuration>
```
## 参考
[https://ke.qq.com/course/199779?taid=1162699186834531](https://ke.qq.com/course/199779?taid=1162699186834531)