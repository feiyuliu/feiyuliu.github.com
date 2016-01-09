---
layout: post
title: "linux基本安全设置"
description: ""
category: 
tags: [linux]
---
{% include JB/setup %}

## linux系统安全

----
###1.推荐使用密钥认证

修改`/etc/ssh/sshd_config`文件下面的配置

```
Protocol 2    #仅允许使用ssh2
PubkeyAuthentication yes  # 启用pubkey认证
AuthorizedKeysFile  .ssh/authorized_keys  #pubkey文件路径
PasswordAuthentication no   #不使用口令认证
PermitRootLogin no     #不使用root用户登录
```

###2.合理使用su和sudo

  * su密码只给少量的人保管，尽量使用sudo命令来
  * 给用户分配执行系统管理员的少量命令
  
  修改`/etc/sudoers`使用`visudo`
  
  ```
  user1 ALL = /bin/cat /etc/shadow #允许user1用户查看shadow文件
  user2 ALL = NOPASSWD: /etc/init.d/nagios restart #允许user1无密码运行启动nagios命令
  user3 ALL = (ALL) NOPASSWD: ALL # 运行user3无密码运行所有命令
  %wowoops  ALL=(ALL)   NOPASSWD: ALL #允许wowoops组无密码运行sudo所有命令
  
  ```
###3.设置系统警告信息

  * 修改`/etc/motd`文件，添加重要警告信息
  
###4.禁止使用`ctrl+Alt+Delete`键盘关闭系统

* centos6版本中注释掉`/etc/init/control-alt-delete.conf`文件里的`exec /sbin/shutdown -r now "Control-Alt-Delete pressed"`
* centos5版本中注释掉`/etc/inittab` 文件中 `ca::ctrlaltdel:/sbin/shutdown -t3 -r now`

###5.启用tcp_wrappers防火墙
* 设置`/etc/hosts.allow`文件来允许通过ssh来访问

```
#service:hosts eg:ALL:ALL
sshd:10.0.0.8  #允许10.0.0.8机器通过ssh来登录
```
* 设置`/etc/hosts.deny`文件来禁止其他的机器登录:`sshd:ALL`



