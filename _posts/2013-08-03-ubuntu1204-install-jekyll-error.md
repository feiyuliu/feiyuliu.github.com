---
layout: post
title: "ubuntu12.04 install jekyll error"
description: ""
category: 
tags: [ubuntu configuration]
---
{% include JB/setup %}
安装jekyll的时候出现一下的错误：

    ERROR:  While generating documentation for jekyll-0.12.1
    ... MESSAGE:   Unhandled special: Special: type=17, text="<!-- more -->"
    ... RDOC args: --ri --op /usr/lib/ruby/gems/1.8/doc/jekyll-0.12.1/ri --charset=UTF-8 lib README.textile LICENSE --title jekyll-0.12.1 Documentation --quiet
解决方法是先执行：

    sudo gem install rdoc
再执行：

    sudo gem install jekyll 
这样就OK了！
