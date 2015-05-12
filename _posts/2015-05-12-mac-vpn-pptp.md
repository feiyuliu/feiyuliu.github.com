---
layout: post
title: "mac vpn pptp模式无法连接问题"
description: ""
category: vpn
tags: [mac]
---
{% include JB/setup %}
由于现在的公司发的电脑很搓，买了一个mac pro，用自己的电脑了。做运维的，经常跟各种命令打交道，这样也方便了一些。

现在有个问题，我要在家连接公司的内网，由于公司是用的pptp模式的，我就自己按照mac上教程一步一步的设置了，但到了最后还是连不上。错误信息如下：

    版本：OS X Yosemite 10.10.2 (14C109)
    日志：
    Fri May 8 20:41:25 2015 : publish_entry SCDSet() failed: Success!
    Fri May 8 20:41:25 2015 : publish_entry SCDSet() failed: Success!
    Fri May 8 20:41:25 2015 : pptp_get_router_address
    Fri May 8 20:41:25 2015 : pptp_get_router_address 192.168.1.1 from dict 1
    Fri May 8 20:41:25 2015 : PPTP connecting to server 'XXXX' (XXXX)...
    Fri May 8 20:41:25 2015 : PPTP connection established.
    Fri May 8 20:41:25 2015 : PPTP set port-mapping for en0, interface: 4, protocol: 0, privatePort: 0
    Fri May 8 20:41:25 2015 : using link 0
    Fri May 8 20:41:25 2015 : Using interface ppp0
    Fri May 8 20:41:25 2015 : Connect: ppp0 <--> socket[34:17]
    Fri May 8 20:41:25 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:25 2015 : PPTP port-mapping for en0, interfaceIndex: 0, Protocol: None, Private Port: 0, Public Address: a0b02b8, Public Port: 0, TTL: 0 (Double NAT)
    Fri May 8 20:41:25 2015 : PPTP port-mapping for en0 inconsistent. is Connected: 1, Previous interface: 4, Current interface 0
    Fri May 8 20:41:25 2015 : PPTP port-mapping for en0 initialized. is Connected: 1, Previous publicAddress: (0), Current publicAddress a0b02b8
    Fri May 8 20:41:25 2015 : PPTP port-mapping for en0 fully initialized. Flagging up
    Fri May 8 20:41:28 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:31 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:34 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:37 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:40 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:43 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:46 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:49 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:52 2015 : sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0x7a05c7ee> <pcomp> <accomp>]
    Fri May 8 20:41:55 2015 : LCP: timeout sending Config-Requests
    Fri May 8 20:41:55 2015 : Connection terminated.
    Fri May 8 20:41:55 2015 : PPTP disconnecting...
    Fri May 8 20:41:55 2015 : PPTP clearing port-mapping for en0
    Fri May 8 20:41:55 2015 : PPTP disconnected

google一下，网上有说设置dhcp模式的，有说修改mtu的，我都试过，无果。过了好几天，我发现在公司用公司的网线登陆，连接vpn居然没有问题；如果用公司的wifi连接的话，就又连不上连。于是，我怀疑是网段的原因了。目前公司分配的网段是10网段的，而我家里或者公司wifi连接后分配的dhcp网段是192.168网段的。如是，我回家后，修改了tplink路由器的LAN口设置的网段，把之前的192.168.1.0/24网段改到10网段了，然后连接，一切OK了。NND，总于搞OK了，自己觉得运维的过程中网络的问题经常会出现，所以得好好学学。
