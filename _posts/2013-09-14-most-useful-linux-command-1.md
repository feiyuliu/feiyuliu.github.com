---
layout: post
title: "一些高级的linux命令(系列一)"
description: ""
category: Linux command
tags: [Linux]
---
{% include JB/setup %}
引言

Shell作为Unix系操作系统当中最有魅力且不可或缺的组件，经过数十载的洗礼不仅没有被淘汰，而且愈加变得成熟稳健，究其原因，大概因为它是个非常稳固的粘合剂，能够把大量功能强大的组件任意配搭，总能很好很快地完成用户的任务。

本文的一些命令很可能看起来是“雕虫小技”，我们只好仰慕一下Shell大牛了，但是有些细节我会稍加发掘加以说明，遇到有趣的地方希望能博您一笑了。

###1.以sudo运行上条命令

	$ sudo !!
大家应该都知sudo，不解释。但通常出现的情况是，敲完命令执行后报错才发现忘了sudo。这时候，新手用户就会：按上箭头，按左箭头，盯着光标回到开始处，输入sudo，回车；高手用户就蛋定多了，按`Ctrl-p`，按`Ctrl-a`，输入sudo，回车。

这里介绍这个是天外飞仙级别的，对，就直接`sudo !!`。

当然这几种解决方式效果是完全一样的，只是款不一样，嗯，不解释。

两个感叹号其实是bash的一个特性，称为事件引用符（event designators）。`!!`其实相当于`!-1`，引用前一条命令，当然也可以`!-2`，`!-50`。默认情况下bash会在`~/.bash_history`文件内记录用户执行的最近500条命令，history命令可以显示这些命令。

关于事件引用符的更多用法可以深入阅读The Definitive Guide to Bash Command Line History。

###2.以HTTP方式共享当前文件夹的文件

	$ python -m SimpleHTTPServer
这命令启动了Python的SimpleHTTPServer模块，考虑到Python在绝大多数的Linux发行版当中都默认安装，所以这个命令很可能是最简单的跨平台传文件的方法。

命令执行后将在本机8000端口开放HTTP服务，在其他能访问本机的机器的浏览器打开`http://ip:8000`即打开一个目录列表，点击即可下载。

###3.在以普通用户打开的vim当中保存一个root用户文件

	:w !sudo tee %
这题目读起来纠结，其实是很常见的，常常忘记了sudo就直接用vim编辑/etc内的文件，（不过也不一定，vim发现保存的文件无法保存时候会提示）等编辑好了，保存时候才发现没权限。曲线方法是先保存个临时文件，退出后再sudo cp回去。不过实际上在vim里面可以直接完成这个过程的，命令就是如此。

查阅vim的文档（输入`:help :w`），会提到命令`:w!{cmd}`，让vim执行一个外部命令{cmd}，然后把当前缓冲区的内容从stdin传入。

tee是一个把stdin保存到文件的小工具。

而%，是vim当中一个只读寄存器的名字，总保存着当前编辑文件的文件路径。

所以执行这个命令，就相当于从vim外部修改了当前编辑的文件，好完工。

###4.切换回上一个目录

	$ cd -
应该不少人都知道这个，横杆-代表上一个目录的路径。

实际上`cd -`就是`cd $OLDPWD`的简写，bash的固定变量$OLDPWD总保存着之前一个目录的路径。

相对地，$PWD总保存着当前目录的路径。这些变量在编写shell脚本时候相当有用。

###5.替换上一条命令中的一个短语

	$ ^foo^bar^
又是另外一个事件引用符（event designator），可以把上一条命令当中的foo替换成bar。

在需要重复运行调试一道长长的命令，需要测试某个参数时候，用这个命令会比较实用；但多数人会首先选择按上箭头提出上道命令，再移动光标去修改某参数，这样更直观，但效率上就不够使用引用符高，而且在脚本中用这个方法可以简化很多。

这道命令的原始样式应该是这样的:

	!!:s/foo/bar/
本文一开始介绍过!!，后面的一段大家应该很熟悉，vim、sed的替换操作都是这样的语法。

关于事件引用符的更多用法可以深入阅读The Definitive Guide to Bash Command Line History

###6.快速备份一个文件

	$ cp filename{,.bak}
这道命令把filename文件拷贝成filename.bak，大家应该在一些比较复杂的安装教程里面见过这样的用法。其原理就在于bash对大括号的展开操作，`filename{,.bak}`这一段会被展开成filename filename.bak再传给cp，于是就有了备份的命令了。

大括号在bash里面是一个排列的意义，可以试试这个：

	$ echo {a,b,c}{a,b,c}{a,b,c}
将输出三个集合的全排列:

	aaa aab aac aba abb abc aca acb acc
	baa bab bac bba bbb bbc bca bcb bcc
	caa cab cac cba cbb cbc cca ccb ccc
关于shell当中的集合操作，可深入阅读“Set Operations in the Unix Shell”

###7.免密码ssh登录主机

	$ ssh-copy-id remote-machine
这个命令把当前用户的公钥串写入到远程主机的	`~/.ssh/authorized_keys`内，这样下次使用ssh登录的时候，远程主机就直接根据这串密钥完成身份校验，不再询问密码了。前提是你当前用户有生成了公钥，默认是没有的，先执行ssh-keygen试试吧！

这个命令如果用手工完成，是这样的：

	your-machine$ scp ~/.ssh/identity.pub remote-machine:
	your-machine$ ssh remote-machine
	remote-machine$ cat identity.pub >> ~/.ssh/authorized_keys
如果你想删掉远程主机上的密钥，直接打开authorized_keys，搜索你的用户名，删除那行，即可。

###8.抓取Linux桌面的视频

	$ ffmpeg -f x11grab -s wxga -r 25 -i :0.0 -sameq /tmp/out.mpg
我们在一些视频网站上看到别人的3D桌面怎么怎么酷的视频，通常就是这么来的，ffmpeg可以直接解码X11的图形，并转换到相应输出格式。

ffmpeg的通常用法是，根据一堆参数，输出一个文件，输出文件通常放最后，下面解析下几个参数：

	-f x11grab 指定输入类型。因为x11的缓冲区不是普通的视频文件可以侦测格式，必须指定后ffmpeg才知道如何获得输入。

	-s wxga 设置抓取区域的大小。wxga是1366*768的标准说法，也可以换成-s 800×600的写法。

	-r 25 设置帧率，即每秒抓取的画面数。

	-i :0.0 设置输入源，本地X默认在0.0

	-sameq 保持跟输入流一样的图像质量，以用来后期处理。

至于其他ffmpeg的用法，可以参考下面两篇文章：

How to Extract Audio Tracks from YouTube Videos
Converting YouTube Flash Videos to a Better Format with ffmpeg
后记

说Shell是一种编程语言，可能有些尴尬，虽然很多人每天都在用Shell，但从来没见它荣登TIOBE编程语言排行榜之类的，可以说毫无名分，因为很多用户没意识到它是一种语言，只当做这是一个能够很好完成任务的工具，基本得理所当然，就好像GUI程序的菜单、按钮一样。

掌握Shell，通常能够让任务在数秒钟内完成，这就让Shell跟C、Perl、Python这些语言区别开来，没人否认后者更能胜任更多的任务，但是他们是在不同的层面上去做，Shell依赖大量的系统组件黏合调用，而后者依赖各种库，各所擅长不同的应用领域，比喻就是，Shell是混凝土，可以很方便地粘合一些建筑组件而成为稳固的高楼大厦；但同样是粘合剂，粘玻璃窗、粘书报、粘皮鞋，混凝土是绝对不合适的，Shell并不擅长一些细致操作，比如它连浮点运算都不支持，更别提什么图形运算什么的。但这并不妨碍Shell来帮我们完成很多粗重任务。

Shell的工作方式，大多数入门用户会觉得枯燥难学，而所谓的经典教材也离不开《Advanced Bash-Scripting》、《Bash Guide for Beginners》，但类似本文这样的一些“雕虫小技”因为难登大雅之堂绝不会收录进去。这情况如果象国外一些unix用户比较多的地方会有很好改善，即使是新手，偶尔看看别人的操作都能“偷师”一手，我编译本系列文章其实也就希望稍微改善一下这个状况。


