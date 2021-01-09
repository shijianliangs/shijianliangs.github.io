---
title: "AOP"
date: 2019-02-03
categories: ["java"]
tags: ["java","aop"]
draft: false 
---
## 1.使用注解方式配置AOP
applicationContext-aop.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- 配置自动扫描的包 -->
    <context:component-scan base-package="com.study.spring2.aop.impl"/>

    <!-- 使 Aspect 注解起作用：自动为匹配的类生成代理对象 -->
    <aop:aspectj-autoproxy/>

</beans>
```
Calculator.java
```java
package com.study.spring2.aop.impl;

public interface Calculator {
	int add(int i, int j);

	int sub(int i, int j);

	int mul(int i, int j);

	int div(int i, int j);
}
```
CalculatorImpl.java
```java
package com.study.spring2.aop.impl;

import org.springframework.stereotype.Component;

@Component(value = "calculator")
public class CalculatorImpl implements Calculator {
	@Override
	public int add(int i, int j) {
		return i + j;
	}

	@Override
	public int sub(int i, int j) {
		return i - j;
	}

	@Override
	public int mul(int i, int j) {
		return i * j;
	}

	@Override
	public int div(int i, int j) {
		return i / j;
	}
}
```
LoggingAspect.java
```java
package com.study.spring2.aop.impl;


import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

import java.util.Arrays;
import java.util.List;

/**
 * 把这个类声明为一个切面： 需要把该类放入 IOC 容器中,再声明为一个切面
 * 可以使用@Order 指定切面的优先级，值越小，优先级越高
 */
@Order(2)
@Aspect
@Component
public class LoggingAspect {
	/**
	 * 定义一个方法，用于声明切入点表达式，该方法中不需要填入其他的代码
	 * 使用 @Pointcut 来声明切入点表达式
	 * 后面其他通知直接使用方法名来引用切入点表达式
	 */
	@Pointcut("execution(public int com.study.spring2.aop.impl.Calculator.*(int,int))")
	public void declareJoinPointExpresson() {
	}

	/**
	 * 声明该方法是一个前置通知，在目标方法开始前执行
	 */
	@Before("declareJoinPointExpresson()")
	public void beforeMethod(JoinPoint joinPoint) {
		String       methodName = joinPoint.getSignature().getName();
		List<Object> args       = Arrays.asList(joinPoint.getArgs());
		System.out.println("The Method " + methodName + " begins with " + args);
	}

	/**
	 * 后置通知：在目标方法执行后(无论是否发生异常)执行的通知
	 * 在后置通知中还不能访问目标方法执行的结果
	 */
	@After("declareJoinPointExpresson()")
	public void afterMethod(JoinPoint joinPoint) {
		String methodName = joinPoint.getSignature().getName();
		System.out.println("The Method " + methodName + " ends");
	}

	/**
	 * 返回通知：在方法正常返回后执行的代码
	 * 返回通知是可以访问到方法的返回值的
	 */
	@AfterReturning(value = "declareJoinPointExpresson()", returning = "result")
	public void afterReturning(JoinPoint joinPoint, Object result) {
		String methodName = joinPoint.getSignature().getName();
		System.out.println("The Method " + methodName + " ends with " + result);
	}

	/**
	 * 异常通知：在目标方法出现异常时会执行的代码
	 * 可以访问异常对象 ，且指定在出现特定异常时执行代码
	 */
	@AfterThrowing(value = "declareJoinPointExpresson()", throwing = "ex")
	public void afterThrowing(JoinPoint joinPoint, Exception ex) {
		String methodName = joinPoint.getSignature().getName();
		System.out.println("The Method " + methodName + " occurs with excetion: " + ex);
	}

	/**
	 * 环绕通知：需要携带 ProceedingJoinPoint 类型参数。
	 * 环绕通知类似于动态代理的全过程：ProceedingJoinPoint 决定是否执行目标方法
	 * 且环绕通知必须有返回值，返回值即目标方法的返回值
	 */
	@Around(value = "declareJoinPointExpresson()")
	public Object aroundMethod(ProceedingJoinPoint proceedingJoinPoint) {
		Object result     = null;
		String methodName = proceedingJoinPoint.getSignature().getName();
		try {
			//前置通知
			System.out.println("The Method " + methodName + " begins with " + Arrays.asList(proceedingJoinPoint.getArgs()));
			//执行目标方法
			result = proceedingJoinPoint.proceed();
			//返回通知
			System.out.println("The Method " + methodName + " ends with " + result);
		} catch (Throwable e) {
			//异常通知
			System.out.println("The Method " + methodName + " occurs with excetion: " + e);
			throw new RuntimeException(e);
		}
		//后置通知
		System.out.println("The Method " + methodName + " ends");
		return result;
	}
}
```
VildationAspect.java
```java
package com.study.spring2.aop.impl;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

import java.util.Arrays;

@Order(1)
@Aspect
@Component
public class VildationAspect {
	@Before("LoggingAspect.declareJoinPointExpresson()")
	public void validateArgs(JoinPoint joinPoint) {
		System.out.println("Validate:" + Arrays.asList(joinPoint.getArgs()));
	}
}
```
Main.java
```java
package com.study.spring2.aop.impl;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
	public static void main(String[] args) {
		//1. 创建 Spring 的 IOC 容器
		ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext-aop.xml");
		//2. 从 IOC 容器中获取 bean 的实例
		Calculator calculator = (Calculator) ctx.getBean("calculator");
		//3. 使用 bean
		int result = calculator.add(3, 6);
		System.out.println(result );

		result = calculator.div(12, 3);
		System.out.println(result );
	}
}
```

## 2.使用XML方式配置AOP
applicationContext-aop-xml.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd 
       http://www.springframework.org/schema/aop 
       http://www.springframework.org/schema/aop/spring-aop.xsd">
    
    <!-- 配置 bean -->
    <bean id="calculator" class="com.study.spring2.aop.xml.CalculatorImpl"/>

    <!-- 配置切面的 bean -->
    <bean id="loggingAspect" class="com.study.spring2.aop.xml.LoggingAspect"/>
    <bean id="vildationAspect" class="com.study.spring2.aop.xml.VildationAspect"/>

    <!-- 配置 AOP -->
    <aop:config>
        <!-- 配置切入点表达式 -->
        <aop:pointcut id="pointcut" expression="execution(* com.study.spring2.aop.xml.Calculator.*(..))"/>
        <!-- 配置切面及通知 -->
        <aop:aspect ref="loggingAspect" order="2">
            <aop:before method="beforeMethod" pointcut-ref="pointcut"/>
            <aop:after method="afterMethod" pointcut-ref="pointcut"/>
            <aop:after-returning method="afterReturning" pointcut-ref="pointcut" returning="result"/>
            <aop:after-throwing method="afterThrowing" pointcut-ref="pointcut" throwing="ex"/>
            <aop:around method="aroundMethod" pointcut-ref="pointcut"/>
        </aop:aspect>
        <aop:aspect ref="vildationAspect" order="1">
            <aop:before method="validateArgs" pointcut-ref="pointcut"/>
        </aop:aspect>
    </aop:config>
</beans>
```
Calculator.java
```java
package com.study.spring2.aop.xml;

public interface Calculator {
	int add(int i, int j);

	int sub(int i, int j);

	int mul(int i, int j);

	int div(int i, int j);
}

```
CalculatorImpl.java
```java
package com.study.spring2.aop.xml;

public class CalculatorImpl implements Calculator {
	@Override
	public int add(int i, int j) {
		return i + j;
	}

	@Override
	public int sub(int i, int j) {
		return i - j;
	}

	@Override
	public int mul(int i, int j) {
		return i * j;
	}

	@Override
	public int div(int i, int j) {
		return i / j;
	}
}

```
LoggingAspect.java
```java
package com.study.spring2.aop.xml;


import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;

import java.util.Arrays;
import java.util.List;

public class LoggingAspect {
	public void declareJoinPointExpresson() {
	}

	public void beforeMethod(JoinPoint joinPoint) {
		String       methodName = joinPoint.getSignature().getName();
		List<Object> args       = Arrays.asList(joinPoint.getArgs());
		System.out.println("The Method " + methodName + " begins with " + args);
	}

	public void afterMethod(JoinPoint joinPoint) {
		String methodName = joinPoint.getSignature().getName();
		System.out.println("The Method " + methodName + " ends");
	}

	public void afterReturning(JoinPoint joinPoint, Object result) {
		String methodName = joinPoint.getSignature().getName();
		System.out.println("The Method " + methodName + " ends with " + result);
	}

	public void afterThrowing(JoinPoint joinPoint, Exception ex) {
		String methodName = joinPoint.getSignature().getName();
		System.out.println("The Method " + methodName + " occurs with excetion: " + ex);
	}

	public Object aroundMethod(ProceedingJoinPoint proceedingJoinPoint) {
		Object result     = null;
		String methodName = proceedingJoinPoint.getSignature().getName();
		try {
			//前置通知
			System.out.println("The Method " + methodName + " begins with " + Arrays.asList(proceedingJoinPoint.getArgs()));
			//执行目标方法
			result = proceedingJoinPoint.proceed();
			//返回通知
			System.out.println("The Method " + methodName + " ends with " + result);
		} catch (Throwable e) {
			//异常通知
			System.out.println("The Method " + methodName + " occurs with excetion: " + e);
			throw new RuntimeException(e);
		}
		//后置通知
		System.out.println("The Method " + methodName + " ends");
		return result;
	}
}
```
VildationAspect.java
```java
package com.study.spring2.aop.xml;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

import java.util.Arrays;

public class VildationAspect {
	public void validateArgs(JoinPoint joinPoint) {
		System.out.println("Validate:" + Arrays.asList(joinPoint.getArgs()));
	}
}
```
Main.java
```java
package com.study.spring2.aop.xml;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
	public static void main(String[] args) {
		//1. 创建 Spring 的 IOC 容器
		ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext-aop-xml.xml");
		//2. 从 IOC 容器中获取 bean 的实例
		Calculator calculator = (Calculator) ctx.getBean("calculator");
		//3. 使用 bean
		int result = calculator.add(3, 6);
		System.out.println(result);

		result = calculator.div(12, 3);
		System.out.println(result);
	}
}
```