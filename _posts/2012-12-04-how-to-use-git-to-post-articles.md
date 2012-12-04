---
layout: post
title: 用git和jekyll来发表文章，并同步到github
category: github
tags: [git,jekyll]
---
{% include JB/setup %}
##jekyll发表文章
可以使用下面的命令来创建文章

    $rake page title="title name" //这个名字将会在url中呈现，所以尽量短些好
到_post目录下找到刚才建立的文件，然后编辑文件。设置title,description,category,tags等，再就是用markdown来写文章了。

  **注意：如果用notpad++来编辑时，要设置文件的格式为 "以UTF-8无BOM格式编码" 否则提交会出现乱码情况**

编辑完成后要先在本地预览一下，再提交到github。一般使用jekyll内置的服务器，运行一下代码：

    $jekyll --server --auto
页面没有问题后可以提交：

    $git add .
    $git commit -m "post a article about how to post a article"
    $git push origin master
如果在目录下删除了某个文件，得用git删除才能够在github上看到删除的结果，否则只是本地删除了，github上没有删除。删除文件后要提交，代码如下：

    $git rm -rf XXX.md
    $git commit -m "comment"
    $git push origin master
    
##过程中出现的问题

####1.打开浏览器出现GBK编码错误

打开Git Bash后运行 jekyll --server --auto在本地测试时出现一下错误

    Liquid error: invalid byte sequence in GBK
这个问题是在 Windows 下出现的，英文博文没问题，中文博文就会报错，原因是你所使用的控制台并不能工作 UTF-8。

临时：在执行 jekyll 命令前，将当前控制台的代码格式转为 UTF-8:

    $export LC_ALL=en_US.UTF-8
    $export LANG=en_US.UTF-8
    $jekyll --server --auto
永久：添加两对用户自定义的环境变量，LC_ALL=en_US.UTF-8 和 LANG=en_US.UTF-8

####2.运行jekyll --server时出现的编码问题

    "Ruby193/lib/ruby/gems/1.9.1/gems/jekyll-0.11.2/lib/jekyll/convertible.rb:29:in ‘read_yaml’: invalid byte sequence in GBK (ArgumentError)"

找到ruby目录下gems/jekyll-0.11.0/lib/jekyll/convertible.rb29行修改为下面的内容

    self.content = File.read(File.join(base, name), :encoding => "utf-8")