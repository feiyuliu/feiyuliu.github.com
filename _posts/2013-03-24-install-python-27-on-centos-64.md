---
layout: post
title: CentOS6.4安装python2.7.3环境
description: ""
category: python
tags: [python]
---
{% include JB/setup %}
Centos6.4默认的python环境是2.6.6。我们可以自己安装Python 2.7.3。但是值得注意的是，我们必须不能破坏系统的环境。因为几个关键的实用应用程序依赖于Python2.6.6。如果替换了系统的python环境就会发生很多难以预见的错误，导致要重装系统。

在没有破坏系统的python环境的情况下安装Python 2.7.3。执行以下命令，请使
用root的身份登录或者使用sudo命令
###安装开发工具
为了编辑Python，你必须要先安装开发工具盒一些额外的库。这些额外的库并不严格的需要，但是如果不安装，新版本的python编译器可能没法工作。所以建议
先安装。

    # yum groupinstall "Development tools"
    # yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel

###下载和安装Python
下面有个一个非常重要的步骤是我们使用的是make altinstall。如果使用make install，你将会看到在系统中有两个不同版本的Python在/usr/bin/目录中。这将会导致很多问题，而且不好处理。

    # wget http://python.org/ftp/python/2.7.3/Python-2.7.3.tar.bz2
    # tar xf Python-2.7.3.tar.bz2
    # cd Python-2.7.3
    # ./configure --prefix=/usr/local
    # make && make altinstall
  
运行以上命令后，你可以在目录/usr/local/bin/python2.7 看到新编译的环境。系统的环境python 2.6.6是在/usr/bin/python目录 和 /usr/bin/python2.6目录
.
###下载和安装Distribute
Distribute提供一个安装python模块的框架。你系统的每一个python解释器都需要它自己的Distribute。你可以自己找到最新版本的Distribute，在这里https://pypi.python.org/pypi/distribute 

    # wget http://pypi.python.org/packages/source/d/distribute/distribute-0.6.35.tar.gz
    # tar xf distribute-0.6.35.tar.gz
    # cd distribute-0.6.35
    # python2.7 setup.py install

这将产生一个脚本/usr/local/bin/easy_install-2.7 ，你可以使用它来安装python 2.7 模块。它将安装的模块放到 /usr/local/lib/python2.7/site-

packages/目录中。

###VirtualEnv构建Python虚拟机工作环境
virtualenv是Python开发常用的工具之一，它可以帮助开发者建立一个独立的虚拟的环境，开发者可以将自己需要用的pythonpackage装入到这个虚拟环境中，这样就和系统全局的其他package隔离了，不会影响系统的package布局，要使用这些安装在虚拟环境中的模块，只需要activate进行该环境就OK了，不activate的话就不能使用那些在虚拟环境中的模块，就像从没安装过一样。

    # easy_install-2.7 virtualenv
    # virtualenv-2.7 --distribute someproject
    New python executable in someproject/bin/python2.7
    Also creating executable in someproject/bin/python
    Installing distribute...................done.
    Installing pip................done.
    # source someproject/bin/activate
    (someproject)# python --version
    Python 2.7.3
    (someproject)#
