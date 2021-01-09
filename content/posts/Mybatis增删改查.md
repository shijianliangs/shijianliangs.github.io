---
title: "Mybatis增删改查"
date: 2019-05-22
categories: ["java"]
tags: ["java","mybatis"]
draft: false 
---
## 测试数据准备
```sql
DROP TABLE IF EXISTS `student`;
CREATE TABLE `student` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8_bin NOT NULL DEFAULT '',
  `age` int(11) NOT NULL DEFAULT '0',
  `gender` varchar(255) COLLATE utf8_bin NOT NULL DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
```
## Mybatis的安装配置
### 1.安装（Maven直接引用）
```xml
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version>
</dependency>
```
`版本:`[https://github.com/mybatis/mybatis-3/releases](https://github.com/mybatis/mybatis-3/releases)

### 2.配置
resource/mybatis/jdbc.properties
```properties
username=root
password=root
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/study
```
resource/mybatis/mybatis-config.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <!-- 引用 JDBC 配置文件 -->
    <properties resource="mybatis/jdbc.properties"/>

    <!-- 配置数据库连接 -->
    <environments default="default">
        <environment id="default">
            <transactionManager type="JDBC"/>
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
        <!--  Mapper 的路径，从 resources 下一级目录开始写 -->
        <mapper resource="mybatis/mapper/StudentMapper.xml"/>
    </mappers>
</configuration>
```
### 3.实现
Student.java
```java
package com.study.mybatis.pojo;

public class Student {
	private String name;
	private int    age;
	private String gender;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getGender() {
		return gender;
	}

	public void setGender(String gender) {
		this.gender = gender;
	}

	@Override
	public String toString() {
		return "Student{" +
			   "name='" + name + '\'' +
			   ", age=" + age +
			   ", gender='" + gender + '\'' +
			   '}';
	}
}

```
StudentMapper.java
```java
package com.study.mybatis.dao;

import com.study.mybatis.pojo.Student;

import java.util.List;

public interface StudentMapper {
	List<Student> getStudents();

	void addStudent(Student student);

	void delStudent(Student student);

	void updateStudent(Student student);
}

```
resource/mybatis/mapper/StudentMapper.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >

<mapper namespace="com.study.mybatis.dao.StudentMapper">
    <resultMap id="resultMap" type="com.study.mybatis.pojo.Student">
        <result column="name" property="name"/>
        <result column="age" property="age"/>
        <result column="gender" property="gender"/>
    </resultMap>
    <select id="getStudents" resultMap="resultMap">
        select * from student;
    </select>
    <update id="updateStudent">
        update student set age = #{age} where name = #{name};
    </update>
    <delete id="delStudent">
        delete from student where name = #{name};
    </delete>
    <insert id="addStudent">
        insert into student (name,age,gender) values (#{name},#{age},#{gender});
    </insert>
</mapper>
```

### 4.测试
```java
package com.study.mybatis.test;

import com.study.mybatis.dao.StudentMapper;
import com.study.mybatis.pojo.Student;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.testng.annotations.Test;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class TestStudent {
	@Test
	public void testStudent() {
		String      resource    = "mybatis/mybatis-config.xml";
		InputStream inputStream = null;
		try {
			inputStream = Resources.getResourceAsStream(resource);
		} catch (IOException e) {
			e.printStackTrace();
		}
		SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream, "default");
		SqlSession        sqlSession        = sqlSessionFactory.openSession(true);
		StudentMapper     studentMapper     = sqlSession.getMapper(StudentMapper.class);

		//初始化
		Student student = new Student();
		student.setName("张三");
		studentMapper.delStudent(student);
		student.setName("李四");
		studentMapper.delStudent(student);
		student.setName("王五");
		studentMapper.delStudent(student);
		student.setName("张三");
		student.setAge(18);
		student.setGender("男");
		studentMapper.addStudent(student);
		student.setName("李四");
		student.setAge(19);
		student.setGender("女");
		studentMapper.addStudent(student);

		//查询
		List<Student> students = studentMapper.getStudents();
		System.out.println("开始查询:\n" + students);

		//新增
		student.setName("王五");
		student.setAge(25);
		student.setGender("男");
		studentMapper.addStudent(student);
		//新增后查询
		students = studentMapper.getStudents();
		System.out.println("新增王五后:\n" + students);

		//删除
		student.setName("李四");
		studentMapper.delStudent(student);
		//删除后查询
		students = studentMapper.getStudents();
		System.out.println("删除李四后:\n" + students);

		//更新王五的年龄为20
		student.setName("王五");
		student.setAge(20);
		studentMapper.updateStudent(student);
		students = studentMapper.getStudents();
		System.out.println("更新王五的年龄后:\n" + students);

	}
}
```

## 参考
[http://www.mybatis.org/mybatis-3/zh/index.html](https://github.com/mybatis/mybatis-3/releases)

[https://ke.qq.com/course/199779?taid=1162699186834531](https://ke.qq.com/course/199779?taid=1162699186834531)