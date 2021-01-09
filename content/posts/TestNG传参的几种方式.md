---
title: "TestNG传参的几种方式"
date: 2019-03-14
categories: ["java"]
tags: ["java","testng"]
draft: false 
---
## 1.通过Xml文件传参
TestNg.java
```java
package com.test;

import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class TestNG {
	@Parameters({"a", "b"})
	@Test
	public static void testNG(String a, String b) {
		System.out.println(a);
		System.out.println(b);
	}
}
```
testNG.xml
```xml
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >
<suite name="test">
    <!-- 参数配置 -->
    <parameter name="a" value="aaa"/>
    <parameter name="b" value="bbb"/>

    <!-- 执行测试 -->
    <test name="test"><classes><class name="com.test.TestNG"/></classes></test>
</suite>
```
执行结果：
```
aaa
bbb
```
## 2.通过@DataProvider传参
```java
package com.test;

import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

public class TestNG {
	@DataProvider(name = "xxx")
	public static Object[][] xxx() {
		return new Object[][]{
				{"aaa", "bbb"},
				};
	}

	@Test(dataProvider = "xxx")
	public static void testNG(String a, String b) {
		System.out.println(a);
		System.out.println(b);
	}
}
```
执行结果：
```
aaa
bbb
```