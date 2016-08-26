---

layout: post
title: "SVN提交代码时遇到403 forbiden MKACTIVITY问题的解决方法"
description: "SVN提交代码时遇到403 forbiden MKACTIVITY问题的解决方法"
category: Development
tags: [C++]
---
{% include JB/setup %}

问题描述
--------

------------------------------------------------------------------------

使用TortoiseSVN提交代码时，遇到403 forbiden MKACTIVITY问题，提交失败，而CHECKOUT代码时却没问题。

原因分析
--------

------------------------------------------------------------------------

一般无法提交代码，都是权限问题。所以第一反应去查看代码权限申请单，发现是可读可写没错。联系了生产专员重新确认了权限，确实是已经开通了可读写。

因此不是权限问题。之后上网搜了一下，发现有可能是SVN提交路径的URL的大小写不匹配问题。

解决方案
--------

------------------------------------------------------------------------

仔细核对了权限申请单上的URL和本地的URL:

pre.
https://172.23.xxx.xxx/svn/svn_xxxServer

发现没错。然后又找生产专员确认了SVN路径，才发现正确的路径是：

pre.
https://172.23.xxx.xxx/svn/Svn_XxxServer

使用正确的URL重新checkout后commit，问题解决。

提交代码遇到403 forbidden问题时，如果确认权限没问题，那么很可能是SVN路径的大小写匹配问题，因为SVN在checkout和update代码时是忽略大小写的，而commit和delete代码时确是大小写敏感的，所以要仔细核对SVN的路径。
