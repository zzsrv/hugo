---
title: rm排除特定文件
description: 
date: 2023-10-25
slug: rm
categories:
    - Linux
---

##### 删除当前目录下所有 *.txt文件，除了test.txt
```
rm `ls *.txt|egrep -v test.txt`
rm `ls *.txt|awk '{if($0 != "test.txt") print $0}'`
```
##### 排除多个文件
```
rm `ls *.txt|egrep -v '(test.txt|fff.txt|ppp.txt)'`
rm -f `ls *.log|egrep -v '(access.log|error.log)'`
rm -f `ls *.log|egrep -v '(access.log)'`
```

注意：上面所用的符号不是单引号，是 `

##### find查找排除

```
rm `find . -name *.txt | egrep -v ‘（test.txt|fff.txt|ppp.txt)'`
```
