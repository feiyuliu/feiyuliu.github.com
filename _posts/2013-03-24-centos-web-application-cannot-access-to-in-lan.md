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
	
	Table: filter
	Chain INPUT (policy ACCEPT)
	num  target     prot opt source               destination
	1    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           tcp dpt:22
	2    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           tcp dpt:8888
	3    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED
	4    ACCEPT     icmp --  0.0.0.0/0            0.0.0.0/0
	5    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0
	6    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22
	7    REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited

	Chain FORWARD (policy ACCEPT)
	num  target     prot opt source               destination
	1    REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited

	Chain OUTPUT (policy ACCEPT)
	num  target     prot opt source               destination

出现如上信息，代表防火墙正在运行ing～
由于我web使用的是8888端口，所以要在防火墙中开放8888端口开放8888端口

    #/sbin/iptables  -I INPUT -p tcp --dport 8888 -j ACCEPT