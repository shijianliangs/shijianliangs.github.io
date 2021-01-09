---
title: "Mybatis动态SQL"
date: 2018-12-08
categories: ["java"]
tags: ["java","mybatis"]
draft: false 
---
EmployeeMapper.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >

<mapper namespace="com.study.mybatis.dynamic.dao.EmployeeMapper">
    <!-- if -->
    <select id="getEmpsByConditionIf" resultType="com.study.mybatis.dynamic.pojo.Employee">
        select * from tbl_employee
        <where>
            <if test="id!=null">
                id = #{id}
            </if>
            <if test="lastName != null and lastName != ''">
                and last_name = #{lastName}
            </if>
            <if test="email != null and email.trim() != ''">
                and last_name = #{lastName}
            </if>
            <if test="gender == 0 or gender == 1">
                and gender = #{gender}
            </if>
        </where>
    </select>
    <!-- trim : 自定义字符串截取
        prefix：字符串前面+
        prefixOverrides：字符串前面-
        suffix：字符串后面+
        suffixOverrides：字符串前面-
    -->
    <select id="getEmpsByConditionTrim" resultType="com.study.mybatis.dynamic.pojo.Employee">
        select * from tbl_employee
        <trim suffixOverrides="and">
            <if test="id!=null">
                id = #{id} and
            </if>
            <if test="lastName != null and lastName != ''">
                last_name = #{lastName} and
            </if>
            <if test="email != null and email.trim() != ''">
                last_name like #{lastName} and
            </if>
            <if test="gender == 0 or gender == 1">
                gender = #{gender}
            </if>
        </trim>
    </select>

    <!-- choose -->
    <select id="getEmpsByConditionChose" resultType="com.study.mybatis.dynamic.pojo.Employee">
        select * from tbl_employee
        <where>
            <choose>
                <when test="id != null">
                    id = #{id}
                </when>
                <when test="lastName != null">
                    last_name like #{lastName}
                </when>
                <when test="email != null">
                    email = #{email}
                </when>
                <otherwise>
                    gender = #{gender}
                </otherwise>
            </choose>
        </where>
    </select>

    <!-- set -->
    <update id="updateEmpSet">
        update tbl_employee
        <set>
            <if test="lastName != null">
                last_name = #{lastName},
            </if>
            <if test="email != null">
                email = #{email},
            </if>
            <if test="gender != null">
                gender = #{gender},
            </if>
        </set>
        <where>
            id = #{id}
        </where>
    </update>

    <update id="updateEmpTrim">
        update tbl_employee
        <trim prefix="set" suffixOverrides=",">
            <if test="lastName != null">
                last_name = #{lastName},
            </if>
            <if test="email != null">
                email = #{email},
            </if>
            <if test="gender != null">
                gender = #{gender},
            </if>
        </trim>
        <where>
            id = #{id}
        </where>
    </update>

    <!-- foreach -->
    <select id="getEmpsByConditionForeach" resultType="com.study.mybatis.dynamic.pojo.Employee">
        select * from tbl_employee
        <foreach collection="ids" item="item_id" separator="," open=" where id in (" close=")">
            #{item_id}
        </foreach>
    </select>
    <insert id="addEmps">
        <!-- include 引用sql片段 -->
        insert into tbl_employee (<include refid="insertColumns"></include>)
        values
        <foreach collection="emps" item="emp" separator=",">
            (#{emp.lastName},#{emp.email},#{emp.gender},#{emp.dept.id})
        </foreach>
    </insert>

    <!--
    mybatis 内置参数:
    _parameter: 代表整个参数，多个参数会封装成map
    _databaseId: 若果配置了databaseIdProvider，_databaseId代表当前数据库的别名
    -->
    <select id="getEmpsTestInnerParams" resultType="com.study.mybatis.dynamic.pojo.Employee">
        <if test="_databaseId=='mysql'">
            <bind name="_lastName" value="'%'+lastName+'%'"/>
            select * from tbl_employee
            <if test="_parameter != null">
                where last_name like #{_lastName}
            </if>
        </if>
        <if test="_databaseId=='oracle'">
            select * from employee
        </if>
    </select>

    <!-- 抽取可重复使用的sql片段 -->
    <sql id="insertColumns">
        <if test="_databaseId=='oracle'">
            last_name,email
        </if>
        <if test="_databaseId=='mysql'">
            last_name,email,gender,d_id
        </if>
    </sql>
</mapper>
```
## github链接
[https://github.com/shijianliangs/study-java/tree/master/mybatis-dynamicsql](https://github.com/shijianliangs/study-java/tree/master/mybatis-dynamicsql)

## 参考
[https://ke.qq.com/course/199779?taid=1162699186834531](https://ke.qq.com/course/199779?taid=1162699186834531)