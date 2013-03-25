---
layout: post
title: centos6安装java7和eclipse
description: ""
category: linux
tags: [linux]
---
{% include JB/setup %}
###安装Java7
(1).首先到oracle官方网上下载linux下的包 [jdk-7u17-linux-i586.rpm](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

(2).安装

	#su -c 'rpm -i jdk-7-linux-x64.rpm'
(3).设置java环境变量 

	#vim /etc/profile
在profile文件最后加上

	export JAVA_HOME=/usr/java/jdk1.7.0_17
	export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar 
	export PATH=$PATH:$JAVA_HOME/bin
使设置生效

	#source /etc/profile 
(4).更新 alternatives，选择JDK版本 

	#update-alternatives --install /usr/bin/java java /usr/java/jdk1.7.0_17/bin/java 60
	#update-alternatives --config java 
选择这个

	*+ 1           /usr/java/jdk1.7.0_17/bin/java
###安装eclipse
(1).下载eclipse的linux版本eclipse-jee-juno-SR2-linux-gtk.tar.gz

(2). 解压缩

	#tar -zxvf eclipse-jee-juno-SR2-linux-gtk.tar.gz
(3).进入/opt/soft/eclipse/目录，双击eclipse就可以启动了。