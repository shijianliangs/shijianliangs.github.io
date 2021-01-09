---
title: "记录一次mac权限修复"
date: 2020-03-27
categories: ["other"]
tags: ["mac"]
draft: false 
---
## 问题
手欠执行了`sudo chmod -R 664 /usr`
直接导致shell命令无法执行，重启后无法进入系统

## 恢复模式
首先想到的方式是重装系统，reboot，按住command+R进入恢复模式

竟然看到了“时间机器”.....

那就先看看"时间机器"能不能恢复吧。恩，时间机器被我关了，没有可恢复的内容，放弃。

那还是重装系统吧。

重装系统需要联网，竟然连不上网了，放弃。

尝试/usr权限修复

## /usr权限修复
还是先进入恢复模式，

先挂载硬盘

```bash
cd /Volumes/Macintosh\ HD
```

看了下别人电脑，权限大多755，先一把给个755权限

```bash
sudo chmod -R 755 usr
```

特殊的几个文件
```bash
chmod 555 usr/bin/nc
chmod 555 usr/bin/logger
chmod 555 usr/bin/login
chmod u+s usr/bin/login
```

重启,可以进入系统了，开心。

打开terminal，无法执行sudo

Google了下，sudo的权限不对,继续进入恢复模式
```bash
chmod u+s usr/bin/sudo
```

之后就变成这个样子了

```bash
-rwsr-xr-x  1 root  wheel  370720 May  4 15:02 /usr/bin/sudo
```

再次重启，成功，sudo也可以执行了。

目前使用无影响，以后有问题再慢慢修复吧。

## 总结
No Zuo No Die

忘记截图了，纯文字感受下

**文笔粗糙请谅解**