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

如果在jekyll运行中出现一些这样的错误:

	| Could not find ref_id = "" for md_link(["\346\226\271\346\213\254\345\217\267"],"")
	| Available refs are []
	+---------------------------------------------------------------------------
	!/var/lib/gems/1.8/gems/maruku-0.6.1/lib/maruku/errors_management.rb:49:in `maruku_error'
	!/var/lib/gems/1.8/gems/maruku-0.6.1/lib/maruku/output/to_html.rb:716:in `to_html_link'
	!/var/lib/gems/1.8/gems/maruku-0.6.1/lib/maruku/output/to_html.rb:970:in `send'
	!/var/lib/gems/1.8/gems/maruku-0.6.1/lib/maruku/output/to_html.rb:970:in `array_to_html'
	!/var/lib/gems/1.8/gems/maruku-0.6.1/lib/maruku/output/to_html.rb:961:in `each'
应该安装如下的内容:

	$ gem install rdiscount
在你站点下的 _config.yml 文件中加入以下配置，以便以后每次执行时不必再指定命令行参数：

	markdown: rdiscount
再运行就OK了