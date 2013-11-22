---
layout: post
title: "nginx alias和root区别"
description: "nginx的alias和root区别"
category: nginx
tags: [nginx配置]
---
{% include JB/setup %}

##

alias 主要不会组合location的地址，而root会组合。

**另外，使用alias时目录名后面一定要加“/”**

        location ~ ^/feiyu/ {
            root  /home/feiyu/;
        }
访问：http://test.com/feiyu/ 实际访问的是/home/feiyu/feiyu/

        location ~ ^/feiyu/ {
            alias  /home/   **使用alias时目录名后面一定要加“/”**
        }
访问：http://test.com/feiyu/ 实际访问的是/home/}


