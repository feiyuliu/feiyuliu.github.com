---
layout: post
title: Python学习-Day Two
description: python学习，遍历文件，查找与关键字匹配的一行
category: Python
tags: [python]
---
{% include JB/setup %}
##G2的Python诗
首先附上一首G2的Python诗

    Programming is fun
    When the work is done
    if you wanna make your work also fun:
        use Python!
##利用Grep处理子目录的问题
递归查找某个目录及其子目录下的文件包含某个关键词的一行。

    #coding=utf-8
    #filename:cdcGrep.py
    import os
    def cdcGrep(basepath,keyword):
        filelist=os.listdir(basepath)
        #print filelist
        for cdc in filelist:
                print os.path.isdir(basepath+os.sep+cdc)
                if os.path.isdir(basepath+os.sep+cdc):
                    filename=basepath+os.sep+cdc
                    #print filename
                    print u'%s 是子目录 ' % filename
                    cdcGrep(filename,keyword)
                    print u'执行迭代函数'
                elif '.md' in cdc:
                    print u'找到目标文件，准备读取'
                    cdcfile=open(basepath+os.sep+cdc)
                    for line in cdcfile.readlines():
                        #print line.decode('utf-8', 'ignore')
                        if keyword in line.decode('utf-8', 'ignore'):
                            print line.decode('utf-8', 'ignore')
                else:
                        print "nothing"
    if __name__=='__main__':
            cdc=cdcGrep('D:\\github',u'托管')
用到了文件编码问题，因为要读取的文件时UTF-8的文件格式，所以要对读出来的内容进行编码转换 line.decode('utf-8', 'ignore') ，文件分隔符通用的用os.sep. 其中的编码问题是最恼火的，下次主要学习一下，编码的codecs模块。

分析：首先传入要查找的根目录和查找的关键词，然后执行os.listdir()来得到当前的目录和文件的集合，遍历此集合，先判断此集合是不是目录，如果是目录，就执行迭代查找，如果是文件，就读取文件，然后使用in来判断是否在其中。