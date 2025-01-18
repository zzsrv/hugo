---
title: SSH传输文件
description: 
date: 2023-10-25
slug: ssh
categories:
    - Linux
---

##### 将本地文件拷贝到服务器上（：相当于当前用户的根目录）
```
scp -rp /path/filename username@remoteIP:path 
```

##### 将远程文件从服务器下载到本地（：相当于当前用户的根目录）
```
scp -rp username@remoteIP:path/filename /path 
```

##### 压缩传输
```
tar cvzf - /path/ | ssh username@remoteip "cd /some/path/; cat -> path.tar.gz" 
```
##### 压缩传输一个目录并解压
```
tar cvzf - /path/ | ssh username@remoteip "cd /some/path/; tar xvzf -" 
```
