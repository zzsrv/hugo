---
title: Maven
description: 
date: 2023-10-27
slug: maven
categories:
    - Java
---

##### Maven打包编译跳过测试命令
```
clean package -B -e -U -Dmaven.test.skip=true -P test
```
-U:该参数能强制让Maven检查所有SNAPSHOT依赖更新，确保集成基于最新的状态，如果没有该参数，Maven默认以天为单位检查更新，而持续集成的频率应该比这高很多。

-e:如果构建出现异常，该参数能让Maven打印完整的stack trace，以方便分析错误原因。

-B:该参数表示让Maven使用批处理模式构建项目，能够避免一些需要人工参与交互而造成的挂起状态。
##### 推送本地
```
mvn install:install-file "-Dfile=<yourJarFileName>.jar" "-DgroupId=<yourGroupID>" "-DartifactId=<yourArtifactId>" "-Dversion=<yourVersion>" "-Dpackaging=jar"
```
##### 推送本地RELEASES版
```
mvn install:install-file "-Dfile=<yourJarFileName>.jar" "-DgroupId=<yourGroupID>" "-DartifactId=<yourArtifactId>" "-Dversion=<yourVersion>-RELEASES" "-Dpackaging=jar"
```
##### 推送本地SNAPSHOT版
```
mvn install:install-file "-Dfile=<yourJarFileName>.jar" "-DgroupId=<yourGroupID>" "-DartifactId=<yourArtifactId>" "-Dversion=<yourVersion>-SNAPSHOT" "-Dpackaging=jar"
```
###### 示例：
```
mvn install:install-file "-Dfile=activemq-client-5.14.1.jar" "-DgroupId=com.asiainfo" "-DartifactId=activemq-client" "-Dversion=1.0" "-Dpackaging=jar"
```
##### 推送到远程
因为nexus是需要登陆操作，在settings.xml的
```
<server>   
<id>nexus</id>   
<username>admin</username>
<password>admin123</password>   
</server>
```
推送的参数为`"-DrepositoryId=nexus"`，其中nexus为server的id属性
##### 推送远程RELEASES版
```
mvn deploy:deploy-file "-Dfile=<yourJarFileName>.jar" "-DgroupId=<yourGroupID>" "-DartifactId=<yourArtifactId>" "-Dversion=<yourVersion>" "-Dpackaging=jar" "-Durl=http://localhost:8081/repository/maven-releases/" "-DrepositoryId=nexus"
```
#### 推送远程SNAPSHOT版
```
mvn deploy:deploy-file "-Dfile=<yourJarFileName>.jar" "-DgroupId=<yourGroupID>" "-DartifactId=<yourArtifactId>" "-Dversion=<yourVersion>" "-Dpackaging=jar" "-Durl=http://localhost:8081/repository/maven-snapshots/" "-DrepositoryId=nexus"
```
###### 示例：
```
mvn deploy:deploy-file "-Dfile=activemq-client-5.14.1.jar" "-DgroupId=com.asiainfo" "-DartifactId=activemq-client" "-Dversion=1.0" "-Dpackaging=jar" "-Durl=http://localhost:8081/repository/maven-releases/"  "-DrepositoryId=nexus"
```
##### 推送到Maven中央仓库
###### 地址：
https://issues.sonatype.org/secure/Dashboard.jspa
https://oss.sonatype.org
###### 中央仓库搜索网站：
https://central.sonatype.com/
###### 发布命令
```
mvn clean deploy -P release -Dgpg.passphrase=password
```
