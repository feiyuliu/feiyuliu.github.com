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
###添加防火墙规则
出现如上信息，代表防火墙正在运行ing～
由于我web使用的是8888端口，所以要在防火墙中开放8888端口开放8888端口

    #/sbin/iptables  -I INPUT -p tcp --dport 8888 -j ACCEPT  
其中I表示默认在INPUT链开始插入。可以指定插入到第几条

	#iptables -I INPUT 2 --dport 80 -j ACCEPT
表示在第二条插入上面的规则。

###删除添加的规则
首先查看添加的规则在INPUT链的第几条。比如上面的开放的8888端口是第二条，可以使用下面命令来删除：

	#/sbin/iptables -D INPUT 2
###其中出现的问题：
我使用下面的命令从浏览器访问到：

	 #iptables -A INPUT -p tcp –dport 8000 -j ACCEPT
其中A表示默认在INPUT链的末尾加上上面的规则。当源地址或目的地址是以名字而不是ip地址的形式出现时，若这些名字可以被解析为多个地址，则这条规则会和所有可用的地址结合。
我使用—A选项时，从局域网里访问不了。但是我使用-I选项时可以。不晓得为啥子。看来iptables里有很多东西要学。贴一下我的iptables链信息。

	Table: filter
	Chain INPUT (policy ACCEPT)
	num  target     prot opt source               destination         
	1    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           tcp dpt:8000 
	2    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED 
	3    ACCEPT     icmp --  0.0.0.0/0            0.0.0.0/0           
	4    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           
	5    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22 
	6    REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited 
	7    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           tcp dpt:8000 

	Chain FORWARD (policy ACCEPT)
	num  target     prot opt source               destination         
	1    REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited 

	Chain OUTPUT (policy ACCEPT)
	num  target     prot opt source               destination