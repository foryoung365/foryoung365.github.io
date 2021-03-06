---

layout: post
title: "使用LOGERR需要注意的问题"
description: "使用LOGERR需要注意的问题"
category: Development
tags: [C++]
---
{% include JB/setup %}

问题描述
--------

------------------------------------------------------------------------

有如下函数声明

pre.
I64 CFriendRecord::GetInt(FRIEND_DATA eType) const;

该函数的作用是根据eType（其实就是字段的索引号）返回对应数据库记录的字段值

数据库表部分结构如下：

pre.
id int(4),unsigned
userid int(4),unsigned
friend int(4),unsigned

现在想要用LOGERR在出错时把程序获取到的该条记录的以上三个字段打印出来：

pre.
LOGERR ("%u, %u, %un", pFriendData-&gt;GetInt(0), pFriendData~~<span style="text-align:right;">GetInt(1), pFriendData</span>~~&gt;GetInt(2));

数据库真实记录值如下：

pre.
90 1000834 1000835

而打印出来的结果是

pre.
90 0 1000834

而使用

pre.
LOGERR ("%u", pFriendData-&gt;GetInt(0));
LOGERR ("%u", pFriendData-&gt;GetInt(1));
LOGERR ("%u", pFriendData-&gt;GetInt(2));

打印出来的结果却是正确的

原因分析
--------

------------------------------------------------------------------------

可能很多人已经发现了，这是类型不匹配读取造成的问题

LOGMODERR中使用的_vsnprintf函数在解析可变参数时，将传入的参数默认按照4字节解析，而GetInt函数的返回值是I64，有8个字节,I64返回的结果低4字节存放的数据库的字段值，高4字节是全0，所以pFriendData-&gt;GetInt(1)打印出来的结果实际上是id字段的高4字节，而不是预想中的userid(1000834)

解决方案
--------

------------------------------------------------------------------------

使用LOGERR,LOGINFO等日志宏记录数据库信息时，需要注意格式化输出的格式必须和参数相匹配（比如本例中的函数返回值I64），而不是使用数据库对应字段的数据类型

pre.
LOGERR ("%llu, %llu, %llun", pFriendData-&gt;GetInt(0), pFriendData~~<span style="text-align:right;">GetInt(1), pFriendData</span>~~&gt;GetInt(2));
