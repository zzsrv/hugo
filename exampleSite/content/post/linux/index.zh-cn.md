---
title: Linux
description: 
date: 2023-11-02
slug: linux
categories:
    - Linux
---

#### 停止指定端口进程

```
netstat -nlp|grep 28082|awk '{print $7}'|awk -F '[/]' '{print "kill -9",$1}'|sh
```
或
```
lsof -i :28082|grep -v "PID"|awk '{print "kill -9",$2}'|sh
```

#### Linux后台启动并将错误输出到标准输出当中

```
nohup /config/frp/frps >/dev/null 2>$1 &
```
#### 查找文件及文件夹并修改属性

```
find / -name "*~" -print -exec rm -f {} \; Linux清空目录下后缀为～的临时文件
find . -type d -exec chmod 755 {} \;	+搜索  这个是把当前目录下及子目录的属性改成755
find . -type f -exec chmod 644 {} \;	+ 这个是把当前目录及子目录中的文件属性改成644
```

#### 挂载交换分区

新建：
```
dd if=/dev/zero of=/swapfile bs=1M count=4096
chmod 0600 /swapfile
/sbin/mkswap /swapfile
/sbin/swapon /swapfile
echo "/swapfile swap swap defaults 0 0" >>/etc/fstab
```
卸载：
```
/sbin/swapoff swapfile
```
删除/etc/fstab中交换分区的配置
```
rm -rf /swapfile
```

#### Linux刻录镜像到U盘

```
sudo dd if=WIN7-RTM_7600.16385_X86-64_CN-EN_DV5.iso of=/dev/sdc
```
