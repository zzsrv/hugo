---
title: Samba
description: 
date: 2023-10-24
slug: samba
categories:
    - Linux
---

#### 1、Samba简介
> Samba是著名的开源软件项目之一，它在Linux/UNIX系统中实现了微软的SMB/CIFS网络协议，从而使得跨平台的文件共享变得更加容易。在部署Windows、Linux/UNIX混合平台的企业环境时，选用Samba可以很好地解决不同系统之间的文件互访问题。

> SMB协议（Server Message Block 服务消息块协议），它能被用于Web连接和客户端与服务器之间的信息沟通。SMB最初是IBM的贝瑞·费根鲍姆（Barry Feigenbaum）研制的，其目的是将DOS操作系统中的本地文件接口“中断13”改造为网络文件系统。

> CIFS协议（Common Internet File System 通用互联网文件系统协议)，CIFS是SMB的另一种实现；CIFS 是一个新提出的协议，它使程序可以访问远程Internet计算机上的文件并要求此计算机提供服务。CIFS 使用客户/服务器模式。

在Samba项目出现之前，Windows并不能直接与Linux/UNIX系统进行文件系统共享；Linux中Samba服务使用NetBIOS（网络的基本输入输出系统），来提供浏览服务显示网络上的共享资源列表的功能。
#### 2、Samba服务组成
Samba服务器提供smbd、nmbd两个服务程序，分别完成不同的功能。
smbd：其主要功能就是用来管理Samba服务器上的共享目录、打印机等，主要是针对网络上的共享资源进行管理的服务。当要访问服务器时，要查找共享文件，这时我们就要依靠smbd这个进程来管理数据传输。
nmbd：其功能是进行NetBIOS名解析，并提供浏览服务显示网络上的共享资源列表。

| 进程          | 对应协议               |
| :------------ | :--------------------- |
| smbd          | 对应smb/cifs协议       |
| nmbd          | 对应netbios协议        |
| winbindd+ldap | 对应Windows AD活动目录 |

#### 3、Samba监听端口

| TCP  | UDP  |
| :--- | :--- |
| 139  | 137  |
| 445  | 138  |

> smbd服务程序负责监听TCP协议的139端口（SMB协议）、445端口（CIFS协议）；
> nmbd服务程序负责监听UDP协议的137、138端口（NetBIOS协议）。

简单的开机启动
```
/usr/sbin/smbd -D
/usr/sbin/nmbd -D
```
#### 4、小米电视访问OMV共享文件夹

扩展配置：
```
min receivefile size = 16384
getwd cache = yes
client max protocol = SMB3
client min protocol = NT1
server max protocol = SMB3
server min protocol = NT1
ntlm auth = yes
lanman auth = yes
raw NTLMv2 auth = yes
```
#### 5、小米云台摄像头连接NAS存储
修改OMV的“监控”共享文件夹权限为 7777，是4个7
