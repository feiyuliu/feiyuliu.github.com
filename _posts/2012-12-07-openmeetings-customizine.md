---
layout: post
title: openmeetings的一些定制化
description: openmeetings的定制，可以修改自己的logo，修改自己的项目名，还有一些性能调优等。
category: openmeetings
tags: [openmeetings]
---
{% include JB/setup %}
##openmeetings logo修改
如果你想要在首页前面改变openmeetings的logo的话，你可以按以下步骤来做：

1. 创建一个png格式的logo图片，要求高度为40px；
2. 在目录openmeetings/WebContent/openmeetings/public/themes/basic-theme/general/下将logo.png退换成你创建的png logo图片；
3. 你可以修改目录openmeetings/WebContent/openmeetings/目录下的 config.xml文件。在appdisplay 标签下修改你的logo和name
4. 你可以修改目录openmeetings/WebContent/openmeetings/目录下的  default-theme.xml文件修改你的图片的name/path

##修改项目名/openmeetings
如果你想要用你自己的名字http://yourip:5080/yourproject 代替http://yourip:5080/openmeetings ,可以按以下步骤做：

1. 首先停止openmeetings的运行
2. 进入openmeetings的目录.
3. 修改/openmeetings/WebContent/openmeetings 为/openmeetings/WebContent/yourproject (例如：mv /openmeetings/WebContent/openmeetings /openmeetings/WebContent/yourproject ).
4. 打开文件openmeetings/WebContent/openmeetings/config.xml
5. 找到并修改<webAppRootKey>openmeetings</webAppRootKey> 为<webAppRootKey>yourproject</webAppRootKey>
6. 找到并修改 <httpRootKey>/openmeetings/</httpRootKey> 为<httpRootKey>/yourproject/</httpRootKey>
修改你的主菜单

如果你想要修改你的主菜单，你可以编辑数据库文件中以下的表：

    navimain   naviglobal

可能由于数据库缓存的原因，修改可能要过一会儿才能起作用。
##JVM调优
在jvm的启动脚本中做一些基本的设置，可以提高RED5服务器的性能。有一个red5.highperf.sh文件，在部署和高负载的情况下，建议使用该脚步启动。

    #!/bin/bash 
    if [ -z "$RED5_HOME" ]; then export RED5_HOME=.; fi 
    # Previous option set 
    export JAVA_OPTS="-Xrs -Xms512M -Xmx1024M -Xss128K -XX:NewSize=256m -XX:SurvivorRatio=16 -XX:MinHeapFreeRatio=20 -XX:+ExplicitGCInvokesConcurrent -Djava.net.preferIPv4Stack=true -Xverify:none" 
    # start Red5 
    echo "Setting Hi Performance Options" 
    exec $RED5_HOME/red5.sh >> $RED5_HOME/log/jvm.stdout 2>&1 & 

你必须在在red5-highperf.sh添加"-XX：+ UseConcMarkSweepGC"参数，这样才能使其更好的工作。但是，如果你是一个高性能研究者，你也可能发挥的值找到完美匹配您的使用情况。
对于一个完整的概述可能的参数和它们的含义，请参阅： http://www.oracle.com/technetwork/java/javase/tech/vmoptions-jsp-140102.html PerformanceTuning
