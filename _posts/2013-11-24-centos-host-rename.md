---
layout: post
title: "centos 主机改名"
description: "centos主机改名字"
category: centos management
tags: [centos]
---
{% include JB/setup %}

##第一步：
修改/etc/sysconfig/network文件中HOSTNAME
    
    NETWORKING="yes"
    NETWORKING_IPV6=no
    IPV6INIT=no
    HOSTNAME="feiyu.ops.cn6"
##第二步
修改/etc/hosts文件
在127.0.0.1 对应行的最后添加，或者另起一行对应实际的IP

    127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
    ::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
    192.168.236.152         feiyu.ops.cn6
##第三步
如果要立即生效，执行

    hostname feiyu.ops.cn6
##第四步
删除原来对应的域名解析，改为现在的域名解析。
