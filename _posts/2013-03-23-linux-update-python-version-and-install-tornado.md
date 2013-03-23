---
layout: post
title: linux下编译安装新版本python和tornado
description: ""
category: python
tags: [python]
---
{% include JB/setup %}
##python版本升级
1、下载

    wget http://www.python.org/ftp/python/2.7.3/Python-2.7.3.tar.bz2
2、解压

    tar jxvf Python-2.7.3.tar.bz2
3、编译安装

    $cd Python-2.7.3
    $./configure
    $make && make install
Python 默认安装目录在/usr/local/lib/python2.7
查看一下刚才安装的版本 /usr/local/bin/python -V，看到了 2.7.3 了
4、更改系统默认版本

    $mv /usr/bin/python /usr/bin/python.bak
    $ln -s /usr/local/bin/python2.7 /usr/bin/python
敲入 python -V 查看是否成功。
##安装Tornado
1、下载tornado

    $wget https://github.com/downloads/facebook/tornado/tornado-2.4.1.tar.gz
2、解压编译安装

    $ tar -zxvf tornado-2.4.1.tar.gz
    $ cd tornado-2.4.1
    $ python setup.py build
    $ python setup.py install
3、创建测试文件

    import tornado.ioloop
    import tornado.web

    class MainHandler(tornado.web.RequestHandler):
        def get(self):
            self.write("Hello, world")
    
    application = tornado.web.Application([
        (r"/", MainHandler),
    ])

    if __name__ == "__main__":
        application.listen(8888)
        tornado.ioloop.IOLoop.instance().start()

4、运行文件

    $python hello.py
出现下面的错误

    import zlib
    ImportError: No module named zlib
解决方法：再次编译python。
进入python源程序目录执行 ：

    $./configure --with-zlib
    $make && make install
再次运行python hello.py，然后打开浏览器，输入http://ip:8888就看到页面输出Hello, world了。表明已经OK了。