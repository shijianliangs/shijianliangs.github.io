---
title: "JMeter分布式部署"
date: 2019-06-26
categories: ["test"]
tags: ["test","jmeter"]
draft: false 
---
## 1. 图解

![image-20191022003218453](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191022003218453.png)

```properties
controller:	192.168.1.1
agent:	192.168.1.2
```



## 2. 从机配置

1.指定启动端口

修改jmeter.properties

```properties
server_port=xxxx
server.rmi.localport=xxxx
```

2.启动jmeter-server

```bash
-bash-4.2#  ./jmeter-server
Using local port: 1099
Created remote object: UnicastServerRef2 [liveRef: [endpoint:[192.168.1.2:1099](local),objID:[231dc20a:16def119767:-7fff, -910579510655877551]]]
```



## 3. 主机配置

1.修改jmeter.properties

```properties
remote_hosts=192.168.12.2:1099
```

2.启动jmeter

在controller机器上远程执行

![image-20191022001515446](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191022001515446.png)

结果正常。

agent机器日志

```bash
-bash-4.2#  ./jmeter-server
Using local port: 1099
Created remote object: UnicastServerRef2 [liveRef: [endpoint:[192.168.1.2:1099](local),objID:[-60309461:16def1854f6:-7fff, -646160165786867583]]]
Starting the test on host 192.168.1.2:1099 @ Mon Oct 21 12:14:30 EDT 2019 (1571674470147)
Finished the test on host 192.168.1.2:1099 @ Mon Oct 21 12:14:30 EDT 2019 (1571674470709)
```

## 4. 遇到的问题

### loopback address

```bash
-bash-4.2# ./jmeter-server
Server failed to start: java.rmi.RemoteException: Cannot start. localhost.localdomain is a loopback address.
An error occurred: Cannot start. localhost.localdomain is a loopback address.
```

**解决方式1**

通过终端命令指定来启动

```bash
./jmeter-server -Djava.rmi.server.hostname=192.168.1.2
```

**解决方式2**	

修改jmeter-server文件

```bash
# One way to fix this is to define RMI_HOST_DEF below
RMI_HOST_DEF=-Djava.rmi.server.hostname=192.168.1.2
```

### Listen failed on port: 0

```bash
Server failed to start: java.rmi.server.ExportException: Listen failed on port: 0; nested exception is:
	java.io.FileNotFoundException: rmi_keystore.jks (No such file or directory)
An error occurred: Listen failed on port: 0; nested exception is:
	java.io.FileNotFoundException: rmi_keystore.jks (No such file or directory)
```

**解决方式**

修改jmeter.properties将server.rmi.ssl.disable设置成true

### No route to host

**解决方式**

telnet查看端口

```
shijl@shijl:~/controller/apache-jmeter-5.1.1/bin$ telnet 192.168.1.2 1099
Trying 192.168.1.2...
telnet: Unable to connect to remote host: No route to host
```

端口不通，检查是否agent机器的端口未开放。开放端口后可以通了

```
shijl@shijl:~/controller/apache-jmeter-5.1.1/bin$ telnet 192.168.1.2 1099
Trying 192.168.1.2...
Connected to 192.168.1.2.
Escape character is '^]'.
```



## 5 . 参考

[https://zhuanlan.zhihu.com/p/22414228](https://zhuanlan.zhihu.com/p/22414228)

[https://www.jianshu.com/p/15dec063bd2a](https://www.jianshu.com/p/15dec063bd2a)

[https://www.jianshu.com/p/9ce0e2b33625](https://www.jianshu.com/p/9ce0e2b33625)



