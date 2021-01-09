---
title: "Mybatis的缓存机制"
date: 2017-09-05
categories: ["java"]
tags: ["java","mybatis"]
draft: false 
---
## 一级缓存（本地缓存）

### 工作机制
* sqlSession级别的缓存，一直开启，无法配置关闭。
* 与数据库同一次会话期间查询到的数据会放在本地缓存中，以后如果需要获取相同的数据，直接从缓存中读取。

### 一级缓存失效的几种情况
* 不同的sqlSession
* sqlSession相同，查询条件不同
* sqlSession相同，查询条件相同，两次之间执行了增删改操作
* sqlSession相同，查询条件相同，两次之间手动清除缓存

```java
openSession.clearCache();
```

* * *

## 二级缓存（全局缓存）

### 工作机制
* namespace级别的缓存
* sqlSession被关闭时，一级缓存保存到二级缓存中
* 不同的namespace查出的缓存数据会放在自己对于的二级缓存中
* 注意：
默认查询出的结果先放到一级缓存中。只有当sqlSession被关闭的时候，一级缓存才会转移到二级缓存中。

### 二级缓存的使用
* 开启全局二级缓存配置(默认开启)

```xml
 <setting name="cacheEnabled" value="true"/>
```
* 在每个mapper.xml中配置使用二级缓存

```xml
<cache></cache>
```
* POJO需要实现序列化接口

```java
public class Department implements Serializable {
    private static final long serialversionUID = 1L;
    //TODO
}
```
### mapper.xml中的cache属性

#### (1)eviction
这个更高级的配置创建了一个 FIFO 缓存，每隔 60 秒刷新，最多可以存储结果对象或列表的 512 个引用，而且返回的对象被认为是只读的，因此对它们进行修改可能会在不同线程中的调用者产生冲突。
可用的清除策略有：
* LRU（默认值） – 最近最少使用：移除最长时间不被使用的对象。
* FIFO – 先进先出：按对象进入缓存的顺序来移除它们。
* SOFT – 软引用：基于垃圾回收器状态和软引用规则移除对象。
* WEAK – 弱引用：更积极地基于垃圾收集器状态和弱引用规则移除对象。
#### (2)flushInterval
（刷新间隔）属性可以被设置为任意的正整数，设置的值应该是一个以毫秒为单位的合理时间量。 默认情况是不设置，也就是没有刷新间隔，缓存仅仅会在调用语句时刷新。
#### (3)size
（引用数目）属性可以被设置为任意正整数，要注意欲缓存对象的大小和运行环境中可用的内存资源。默认值是 1024。
#### (4)readOnly
（只读）属性可以被设置为 true 或 false。
* 只读的缓存会给所有调用者返回缓存对象的相同实例。 因此这些对象不能被修改。这就提供了可观的性能提升。
* 而可读写的缓存会（通过序列化）返回缓存对象的拷贝。 速度上会慢一些，但是更安全，因此默认值是 false。

## 参考
[http://www.mybatis.org/mybatis-3/zh/sqlmap-xml.html](http://www.mybatis.org/mybatis-3/zh/sqlmap-xml.html)
[https://ke.qq.com/course/199779?taid=1162699186834531](https://ke.qq.com/course/199779?taid=1162699186834531)