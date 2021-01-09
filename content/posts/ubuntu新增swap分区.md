---
title: "ubuntu新增swap分区"
date: 2018-12-12
categories: ["linux"]
tags: ["linux","swap"]
draft: false 
---
系统版本信息
```bash
root@vultr:~# cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.1 LTS"
```

在执行apt命令的时候，报错了
```bash
root@vultr:~# sudo apt-get upgrade
E: Dynamic MMap ran out of room. Please increase the size of APT::Cache-Start. Current value: 42991616. (man 5 apt.conf)
Reading package lists... Error!
E: Dynamic MMap ran out of room. Please increase the size of APT::Cache-Start. Current value: 42991616. (man 5 apt.conf)
E: Error occurred while processing r-cran-futile.logger (NewFileVer1)
E: Problem with MergeList /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic_universe_binary-i386_Packages
E: The package lists or status file could not be parsed or opened.
```

Google了下，说是没有swap分区，查看一下果然如此。
```bash
root@vultr:~# free -h
              total        used        free      shared  buff/cache   available
Mem:           985M        115M        518M        2.1M        350M        730M
Swap:            0B          0B          0B
```

创建swap文件，swap文件的大小一般是内存的2倍，我的内存1G，那这里就新建一个2G的swap文件
```bash
sudo fallocate -l 2G /swapfile
```

给swap文件赋予root用户权限
```bash
sudo chmod 600 /swapfile
```

将文件标记为交换空间
```bash
root@vultr:~# sudo mkswap /swapfile
Setting up swapspace version 1, size = 2 GiB (2147479552 bytes)
no label, UUID=697c0490-f0a3-4f30-8e6e-672a562154ab
```

初始化分区
```bash
sudo swapon /swapfile
```

`free -h`再次查看下
```bash
root@vultr:~# free -h
              total        used        free      shared  buff/cache   available
Mem:           985M        115M        515M        2.1M        354M        730M
Swap:          2.0G          0B        2.0G
```

此时再执行`sudo apt-get upgrade`就不会报错了

但是，此时的swap分区只是暂时的，服务器重启就会失效。如何永久新增swap分区呢？

备份/etc/fstab文件
```bash
sudo cp /etc/fstab /etc/fstab.bak
```

永久保留交换文件
```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

合理调整swappiness参数

查看当前的swappiness值
```bash
root@vultr:~# cat /proc/sys/vm/swappiness
60
```

对于桌面系统来说，60不是一个糟糕的数值，对于服务器来说，最好是设置的非常靠近0。我们可以通过sysctl命令调整这个数值。
```bash
root@vultr:~# sudo sysctl vm.swappiness=10
vm.swappiness = 10
```

若想要重启生效

在`/etc/sysctl.conf`末尾添加`vm.swappiness=10`


## 参考
[https://blog.csdn.net/u010429286/article/details/79219230](https://blog.csdn.net/u010429286/article/details/79219230)

[https://blog.csdn.net/qq_35976351/article/details/79363760](https://blog.csdn.net/qq_35976351/article/details/79363760)

## 给大家推荐一个好用的VPS

[https://www.vultr.com](https://www.vultr.com/?ref=7324004)