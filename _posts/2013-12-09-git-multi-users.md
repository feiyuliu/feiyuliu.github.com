---
layout: post
title: "git多密钥管理"
description: ""
category: git
tags: [git]
---
{% include JB/setup %}
在使用git管理多个项目时，可能存在不同的项目用户名，登录邮箱，密钥等不相同；如果在项目时再通过命令或者配置文件修改的话，就可能使用新的密钥覆盖旧的密钥的情况。

在新增私钥的时候，通过指定不同的文件名来生存不同的私钥文件。

	ssh-keygen -t rsa -f ~/.ssh/id_rsa.qunar -C "key for qunar work"
	ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "key for github work"
在*~/.ssh/*新增配置文件config，并修改权限

	touch ~/.ssh/config
	chmod 600 ~/.ssh/config

修改*config*文件的内容

	Host github.com
    	    IdentityFile ~/.ssh/id_rsa.github
    	    user feiyuliu
	Host gitlab.corp.qunar.com
	    IdentityFile ~/.ssh/id_rsa.qunar
            user feiyu.liu
	ServerAliveInterval 30
	ControlMaster auto
	ControlPath /tmp/master-%r@%h:%p
这样在登录的时候，ssh通过不同的Host来读取不同的私钥文件。
