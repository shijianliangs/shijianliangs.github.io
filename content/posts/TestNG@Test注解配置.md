---
title: "TestNG@Test注解配置"
date: 2017-09-17
categories: ["java"]
tags: ["java","testng"]
draft: false 
---
## alwaysRun
If set to true, this test method will always be run even if it depends on a method that failed.
```java
	/**
 	* 默认: false
 	* 设置为 true ，则次方法依赖的方法失败，该方法也会运行。
 	*/
	@Test(alwaysRun = true)
```

## dataProvider
The name of the data provider for this test method.
```java
/**
 * 设置该方法的执行参数
 */
@DataProvider(name = "xxx")
public static Object[][] xxx() {
	return new Object[][]{
			{"aaa", "bbb"},
			};
}
@Test(dataProvider = "xxx")
```

## dataProviderClass
The class where to look for the data provider. If not specified, the data provider will be looked on the class of the current test method or one of its base classes. If this attribute is specified, the data provider method needs to be static on the specified class.
```java
/**
 * dataProviderClass 指定去哪个类中查找 xxx ,与 dataProvider 配合使用
 * 默认查询该方法所在的类
 */
@DataProvider(name = "xxx")
public static Object[][] xxx() {
	return new Object[][]{
			{"aaa", "bbb"},
			};
}
@Test(dataProvider = "xxx", dataProviderClass = Bill.class)
```

## groups
The list of groups this class/method belongs to.
```java
/**
 * groups 测试方法所属的组
 * 一个方法可以属于多个组
 */
@Test(groups = {"g1","g2"})
```

## dependsOnGroups
The list of groups this method depends on.
```java
@Test(groups = {"g1", "g2"})
public void method0() {}

/**
 * dependsOnGroups 测试方法依赖的组
 * 执行方法时，会先执行依赖组包含的方法
 */
@Test(dependsOnGroups = {"g1"})
public void method1() {}
```

## dependsOnMethods
The list of methods this method depends on.
```java
@Test()
public void method0() {}

/**
 * dependsOnMethods 测试方法依赖的方法
 * 执行方法时，会先执行依赖的方法
 */
@Test(dependsOnMethods = {"method0"})
public void method1() {}
```

## description
The description for this method.
```java
/**
 * 描述
 */
@Test(description = "这是测试XXX功能")
```

## enabled
Whether methods on this class/method are enabled.
```java
/**
 * 是否执行该方法
 * 默认 true，设置为 false，执行时，跳过该方法
 */
@Test(enabled = false)
```

## expectedExceptions
The list of exceptions that a test method is expected to throw. If no exception or a different than one on this list is thrown, this test will be marked a failure.
```java
/**
 * expectedExceptions 预期的异常
 * 如果设置 IOException 为预期异常，则测试方法抛出 IOException 异常时，该测试结果也是通过
 */
@Test(expectedExceptions = IOException.class)
```

## invocationCount
The number of times this method should be invoked.
```java
/**
 * invocationCount 调用此方法的次数，默认为 1
 */
@Test(invocationCount = 10)
```

## invocationTimeOut
The maximum number of milliseconds this test should take for the cumulated time of all the invocationcounts. This attribute will be ignored if invocationCount is not specified.
```java
/**
 * invocationTimeOut 调用此方法的超时时间，执行方法的时间超过设置的值，则失败
 * invocationTimeOut 需要和 invocationCount 结合使用才有效
 */
@Test(invocationCount = 10, invocationTimeOut = 1L)
public void test1() throws InterruptedException {
	Thread.sleep(11L);
	System.out.println(1);
}
```

## priority
The priority for this test method. Lower priorities will be scheduled first.
```java
/**
 * priority 调用此方法的优先级
 * 值越小，优先级越高
 */
@Test(priority = 0)
```

## successPercentage
The percentage of success expected from this method
```java
/**
 * successPercentage 预期的成功百分比，若执行100次，成功90次，则算作测试通过
 */
@Test(invocationCount = 100,successPercentage = 90)
```

## singleThreaded
If set to true, all the methods on this test class are guaranteed to run in the same thread, even if the tests are currently being run with parallel="methods". This attribute can only be used at the class level and it will be ignored if used at the method level. Note: this attribute used to be called sequential (now deprecated).

```java
/**
 * 单线程设置，只有设置 ’类‘ 才有效
 */
@Test(singleThreaded = true)
```

## timeOut
The maximum number of milliseconds this test should take.

```java
/**
 * timeOut 超时时间，超时则失败
 */
@Test(timeOut = 1)
```

## threadPoolSize
The size of the thread pool for this method. The method will be invoked from multiple threads as specified by invocationCount. 
Note: this attribute is ignored if invocationCount is not specified
```java
/**
 * threadPoolSize 线程池大小，并发跑
 * 与 invocationCount 结合使用，不设置 invocationCount，属性无效
 */
@Test(invocationCount = 100, threadPoolSize = 10, timeOut = 100L)
```

# 官方文档
[https://testng.org/doc/documentation-main.html](https://testng.org/doc/documentation-main.html)