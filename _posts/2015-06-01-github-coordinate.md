---
layout: post
title: "github协同开发"
description: ""
category: 
tags: [github]
---
{% include JB/setup %}

1.在 GitHub 上 fork 到自己的仓库，如 feythin/feythin_test，然后 clone 到本地，并设置用户信息。

  $ git clone git@github.com:feythin/feythin_test.git
  $ cd feythin_test
  $ git config user.name "yourname"
  $ git config user.email "your email"

2.修改代码后提交，并推送到自己的仓库。

   $ #do some change on the content
   $ git commit -am "Fix issue #1: change helo to hello"
   $ git push

3.在 GitHub 网站上提交 pull request。如果原作者通过的话，会把你提交的代码merger到原作者的代码里去。

4.定期使用项目仓库内容更新自己仓库内容。

   $ git remote add upstream https://github.com/yeasy/feythin_test
   $ git fetch upstream
   $ git checkout master
   $ git rebase upstream/master
   $ git push -f origin master
