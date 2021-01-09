---
title: "spring的xml配置"
date: 2018-11-01
categories: ["java"]
tags: ["java","spring"]
draft: false 
---
## 创建一个Bean
applictionContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <bean id="helloWorld" class="com.study.spring.pojo.HelloWorld">
        <property name="name" value="china-spring"/>
    </bean>
    
</beans>
```

## Bean熟悉值包含特殊字符的处理方式
applictionContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="car1" class="com.study.spring.pojo.Car">
        <constructor-arg name="brand" value="BMW"/>
        <!-- 如果字面包含特殊字符可以使用 <![CDATA[]]> 包裹-->
        <!-- 属性值也可以通过 value 子节点进行配置-->
        <constructor-arg name="city"><value><![CDATA[<Beijing'>]]></value></constructor-arg>
        <constructor-arg name="price" value="1000000"/>
        <constructor-arg name="maxSpeed" value="300"/>
    </bean>
    
</beans>
```

## Bean引用
applictionContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="car1" class="com.study.spring.pojo.Car">
        <constructor-arg name="brand" value="BMW"/>
        <constructor-arg name="city" value="Shanghai"/>
        <constructor-arg name="price" value="1000000"/>
        <constructor-arg name="maxSpeed" value="300"/>
    </bean>

    <bean id="person" class="com.study.spring.pojo.Person">
        <property name="name" value="Tom"/>
        <property name="age" value="20"/>
        <!-- 可以使用 property 的 ref 属性建立 bean 之间的引用关系-->
        <property name="car" ref="car1"/>
    </bean>
</beans>
```

## 内部Bean
applictionContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="person" class="com.study.spring.pojo.Person">
        <property name="name" value="Tom"/>
        <property name="age" value="20"/>
        <property name="car">
            <!-- 内部 bean ,不能被外部 bean 引用 -->
            <bean class="com.study.spring.pojo.Car">
                <constructor-arg name="brand" value="Ford"/>
                <constructor-arg name="city" value="Changan"/>
                <constructor-arg name="price" value="1500000"/>
                <constructor-arg name="maxSpeed" value="140"/>
            </bean>
        </property>
    </bean>
</beans>
```

## Bean为级联属性赋值
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="car1" class="com.study.spring.pojo.Car">
        <constructor-arg name="brand" value="BMW"/>
        <constructor-arg name="city" value="Shanghai"/>
        <constructor-arg name="price" value="1000000"/>
        <constructor-arg name="maxSpeed" value="300"/>
    </bean>

    <bean id="person" class="com.study.spring.pojo.Person">
        <property name="name" value="Tom"/>
        <property name="age" value="20"/>
        <property name="car" ref="car1"/>
        <!-- 为级联属性赋值 -->
        <property name="car.maxSpeed" value="500"/>
    </bean>
</beans>
```

## Bean配置集合属性
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 配置集合属性 -->
    <bean id="person1" class="com.study.spring.pojo.collection.Person">
        <property name="name" value="Jerry"/>
        <property name="age" value="30"/>
        <property name="cars">
            <list>
                <bean class="com.study.spring.pojo.collection.Car">
                    <constructor-arg name="brand" value="FT"/>
                    <constructor-arg name="city" value="XA"/>
                    <constructor-arg name="price" value="100000"/>
                    <constructor-arg name="maxSpeed" value="220"/>
                </bean>
                <bean class="com.study.spring.pojo.collection.Car">
                    <constructor-arg name="brand" value="FT1"/>
                    <constructor-arg name="city" value="XA1"/>
                    <constructor-arg name="price" value="110000"/>
                    <constructor-arg name="maxSpeed" value="230"/>
                </bean>
            </list>
        </property>
    </bean>
</beans>
```

## 配置Properties属性值
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 配置 Properties 属性值 -->
    <bean id="dataSource" class="com.study.spring.pojo.DataSource">
        <property name="properties">
            <props>
                <prop key="username">root</prop>
                <prop key="password">root</prop>
                <prop key="jdbcUrl">jdbc:mysql://127.0.0.1:3306/blog</prop>
                <prop key="driverClass">com.mysql.jdbc.Driver</prop>
            </props>
        </property>
    </bean>
</beans>
```

## 配置单例的集合
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/util
       http://www.springframework.org/schema/util/spring-util.xsd">

    <!-- 配置单例的集合 bean ，以供多个 bean 调用， 需要导入 util 命名空间-->
    <util:list id="cars">
        <ref bean="car1"/>
        <ref bean="car1"/>
        <ref bean="car1"/>
    </util:list>
</beans>
```

## 通过p命名空间为Bean赋值
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <!-- 通过 p 命名空间为 bean 赋值，需要先导入 p 命名空间，相对于传统的配置方式更加简洁 -->
    <bean id="person2" class="com.study.spring.pojo.collection.Person" p:name="Queen" p:age="20" p:cars-ref="cars"/>
</beans>
```

## Bean自动装配
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="com.study.spring.pojo.autowire.Address" id="address" p:city="Beijing" p:street="Chaoyang"/>
    <bean class="com.study.spring.pojo.autowire.Car" id="car" p:brand="Audi" p:price="2000000"/>
    <bean class="com.study.spring.pojo.autowire.Person" id="person" p:name="Jay" p:address-ref="address"
          p:car-ref="car"/>
    <!--
    可以使用 autowire 属性指定自动装配方式。
    byName 根据 bean 的名字和当前 bean 的 setter 风格的属性名进行自动装配。若有匹配的，则装配；若没有匹配的，则不装配。
    byType 根据 bean 的类型和当前 bean 的属性类型进行自动装配。若 IOC 容器中有1个以上的类型匹配，则抛异常。
    -->
    <bean class="com.study.spring.pojo.autowire.Person" id="person1" p:name="Jay" autowire="byName"/>
    <bean class="com.study.spring.pojo.autowire.Person" id="person3" p:name="Jay" autowire="byType"/>

</beans>
```

## Bean的继承
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- bean 的配置继承：使用 bean 的 parent 属性指定继承哪个 bean 的配置-->
    <bean class="com.study.spring.pojo.autowire.Address" id="address" p:city="Beijing" p:street="WuDaoKou"/>
    <bean class="com.study.spring.pojo.autowire.Address" id="address2" parent="address"/>

    <!--
    抽象 bean：abstract 属性为 true 的 bean。这样的 bean 不能被 IOC 容器实例化，只能用来被继承。
    若一个 bean 的 class 属性没有被指定，则该 bean 必须是一个抽象 bean。
    -->
    <bean class="com.study.spring.pojo.autowire.Address" id="address3" p:city="Beijing" p:street="WuDaoKou" abstract="true"/>
    <bean id="address1" parent="address3" p:street="DaZhongSi"/>
</beans>
```

## Bean的依赖
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 要求在配置 person 时，必须有一个关联的 car！ 换句话说 person 这个 bean 依赖于 car 这个 bean -->
    <bean class="com.study.spring.pojo.autowire.Car" id="car2" p:brand="BMW" p:price="300000"/>
    <bean class="com.study.spring.pojo.autowire.Person" id="person" p:name="Tom" p:address-ref="address" p:car-ref="car2" depends-on="car2"/>
</beans>
```

## Bean的作用域
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--
        使用 bean 的 scope 属性来配置 bean 的作用域
        singleton：默认值. 容器初始化时创建 bean 实例，在整个容器生命周期内只创建这一个 bean （单例的）
        prototype：原型的. 容器初始化时不创建 bean 实例，而在每次请求时都创建一个新的 bean 实例，并返回。
    -->
    <bean class="com.study.spring.pojo.autowire.Car" id="car3" p:brand="Audi" p:price="500000" scope="prototype"/>
</beans>
```

## Bean引用外部文件
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd">
    
    <!-- 导入属性文件 -->
    <context:property-placeholder location="jdbc.properties"/>

    <!-- 使用外部文件的属性 -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
        <property name="driverClassName" value="${driverClassName}"/>
    </bean>
</beans>
```
jdbc.properties
```properties
username=root
password=root
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306
```

## 使用SpEL为属性赋值
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="address" class="com.study.spring.pojo.spel.Address">
        <!-- 使用 SpEL 为属性赋一个字面值 -->
        <property name="city" value="#{'Beijing'}"/>
        <property name="street" value="WuDaoKou"/>
    </bean>

    <bean id="car" class="com.study.spring.pojo.spel.Car">
        <property name="brand" value="Audi"/>
        <property name="price" value="500000"/>
        <!-- 使用 SpEL 引用类的静态属性 -->
        <property name="tyrePerimeter" value="#{T(java.lang.Math).PI * 80}"/>
    </bean>

    <bean id="person" class="com.study.spring.pojo.spel.Person">
        <!-- 使用 SePL 来引用其他的 bean -->
        <property name="car" value="#{car}"/>
        <!-- 使用 SePL 来引用其他的 bean 的属性 -->
        <property name="city" value="#{address.city}"/>
        <!-- 在 SePL 中使用运算符 -->
        <property name="info" value="#{car.price > 300000 ? '金领':'白领 '}"/>
        <property name="name" value="Tom"/>
    </bean>

</beans>
```