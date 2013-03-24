---
layout: post
title: CentOS部署web应用，本机可以访问，局域网不能访问的解决方法
description: ""
category: Web
tags: [iptables]
---
{% include JB/setup %}
CentOS部署web应用，本机可以访问，局域网不能访问的解决方法
查看防火墙状态：

    #/etc/init.d/iptables status
出现如上信息，代表防火墙正在运行ing～
由于我web使用的是8888端口，所以要在防火墙中开放8888端口开放8888端口

    #/sbin/iptables  -I INPUT -p tcp --dport 8888 -j ACCEPT