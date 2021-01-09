---
title: "JMeter5.2命令行选项"
date: 2019-01-13
categories: ["test"]
tags: ["test","jmeter"]
draft: false 
---
```bash
~/apache-jmeter-5.2/bin/jmeter -?
    _    ____   _    ____ _   _ _____       _ __  __ _____ _____ _____ ____
   / \  |  _ \ / \  / ___| | | | ____|     | |  \/  | ____|_   _| ____|  _ \
  / _ \ | |_) / _ \| |   | |_| |  _|    _  | | |\/| |  _|   | | |  _| | |_) |
 / ___ \|  __/ ___ \ |___|  _  | |___  | |_| | |  | | |___  | | | |___|  _ <
/_/   \_\_| /_/   \_\____|_| |_|_____|  \___/|_|  |_|_____| |_| |_____|_| \_\ 5.2

Copyright (c) 1999-2019 The Apache Software Foundation

	# 命令行选项
	--? 
	
	# 使用帮助
	-h, --help 
		
	# 查看版本号
	-v, --version 
	
	# 指定要使用的jmeter.properties属性文件
	-p, --propfile <argument> 
		
	# 其他JMeter属性文件
	-q, --addprop <argument>
		
	# 要运行的JMeter文件,'-t LAST'将使用最后一次用过的文件
	-t, --testfile <argument>

	# 指定记录执行日志的文件
	-l, --logfile <argument>

	# 日志配置文件 (log4j2.xml)
	-i, --jmeterlogconf <argument>
		
	# 日志输出文件 (jmeter.log)
	-j, --jmeterlogfile <argument>
		
	# 非GUI模式运行JMeter
	-n, --nongui

	# 运行JMeter server
	-s, --server
		
	# Set a proxy scheme to use for the proxy server
	-E, --proxyScheme <argument>
		
	# 代理服务器IP
	-H, --proxyHost <argument>
		
	# 代理服务器端口
	-P, --proxyPort <argument>
		
	# 设置不走代理的域名(e.g. *.apache.org|localhost)
	-N, --nonProxyHosts <argument>
		
	# 代理服务器用户名
	-u, --username <argument>
		
	# 代理服务器密码
	-a, --password <argument>
		
	# Define additional JMeter properties
	-J, --jmeterproperty <argument>=<value>
	
	# Define Global properties (sent to servers)		e.g. -Gport=123		 or Gglobal.properties
	-G, --globalproperty <argument>=<value>
		
	# Define additional system properties
	-D, --systemproperty <argument>=<value>
		
	# additional system property file(s)
	-S, --systemPropertyFile <argument>
		
	# force delete existing results files and web report folder if present before starting the test
	-f, --forceDeleteResultFile
		
	# [category=]level e.g. jorphan=INFO, jmeter.util=DEBUG or com.example.foo=WARN
	-L, --loglevel <argument>=<value>
	
	# 远程启动所有
	-r, --runremote
	
	# 远程启动指定
	-R, --remotestart <argument>

	# the jmeter home directory to use
	-d, --homedir <argument>
	
	# Exit the remote servers at end of test (non-GUI)
	-X, --remoteexit
	
	# generate report dashboard only, from a test results file
	-g, --reportonly <argument>
		
	# generate report dashboard after load test
	-e, --reportatendofloadtests
		
	# output folder for report dashboard
	-o, --reportoutputfolder <argument>
```

