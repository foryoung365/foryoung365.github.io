---

layout: post
title: "SVN全局忽略匹配表达式"
description: "SVN全局忽略匹配表达式"
category: Development
tags: [C++]
---
{% include JB/setup %}

不错的一组SVN全局忽略匹配表达式，记录下来备用。以后重装SVN的时候再也不用到处找了。

**可复制黏贴模式**

pre.
**.o**.lo .la ## .**.rej .rej .~ ~ .# .DS_Store thumbs.db Thumbs.db**.bak **.class**.exe **.dll**.mine **.obj**.ncb **.lib**.log **.idb**.pdb **.ilk .msi .res**.pch **.suo**.exp ~. cvs CVS .CVS .cvs release Release debug Debug ignore Ignore bin Bin obj Obj **.csproj.user**.user _ReSharper.* *.resharper.user

**可读模式**

pre.
**.o**.lo .la ## .**.rej .rej .~ ~ .# .DS_Store thumbs.db Thumbs.db**.bak
**.class**.exe **.dll**.mine **.obj**.ncb **.lib**.log **.idb**.pdb **.ilk .msi .res**.pch **.suo**.exp ~. cvs
CVS .CVS .cvs release Release debug
Debug ignore Ignore bin Bin obj Obj
**.csproj.user**.user _ReSharper.* *.resharper.user

来自 [StackOverflow](http://stackoverflow.com/questions/85353/best-general-svn-ignore-pattern)
