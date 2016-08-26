---

layout: post
title: "游戏内类微博好友系统实现的一种方案"
description: "游戏内类微博好友系统实现的一种方案"
category: Development
tags: [GameDevelopment]
---
{% include JB/setup %}

问题描述
--------

------------------------------------------------------------------------

游戏内需要实现一种类似微博的好友系统。这种好友系统和一般的好友系统的区别在于玩家添加好友是单向的，不需要对方同意。但是玩家添加对方为好友后，对方能在听众列表中看到玩家的信息，因此仍然需要维护两份数据。

添加黑名单时，玩家自己的黑名单中会出现对方的名字，但是对方看不到自己被谁加入了黑名单，当对方上线时无法知道该给谁广播消息通告上线。

解决方案
--------

------------------------------------------------------------------------

采用如下数据表记录好友信息（这里只列出部分关键字段）：

pre.
CREATE TABLE `cq_friend` (
`id` int(4) unsigned NOT NULL auto_increment,
`user_id` int(4) unsigned NOT NULL default '0',
`frd_id` int(4) unsigned NOT NULL default '0',
`frd_type` int(4) unsigned default '0',
PRIMARY KEY (`id`),
KEY `user_id` (`user_id`),
KEY `idx_friend` (`frd_id`)
) TYPE=MyISAM

其中frd_type用来记录好友的类型：

pre.
enum FRIENDTYPE
{
FRIENDTYPE_FRIEND = 0x1, //好友
FRIENDTYPE_FANS = 0x2, //听众
FRIENDTYPE_BLACKLIST = 0x4, //黑名单
FRIENDTYPE_LASTCONTACTER = 0x8, //最近联系人
FRIENDTYPE_BEBLACKED = 0x10, //被加入黑名单
FRIRNDTYPE_ALL = 0xFF, //以上所有
}；

这里用位来标记好友类型，是方便查找时同时匹配多种类型：

比如同时查找好友和听众：

pre.
FRIENDTYPE_FRIEND | FRIENDTYPE_FANS

添加好友时，需要添加两条数据库记录：

玩家A添加玩家B为好友：

pre.
1.user_id=ID(A), frd_id=ID(B), frd_type=FRIENDTYPE_FRIEND （B是A的好友）
2.user_id=ID(B), frd_id=ID(A), frd_type=FRIENDTYPE_FANS （A是B的听众）

当玩家上线时，需要给自己所有的听众和把自己加入黑名单的人广播上线通告，因此服务器上还需要维护一份玩家被哪些人加入了黑名单的集合，但是这个集合只在服务器上作为管理使用，不下发给客户端。

因此，添加黑名单时也需要维护两条记录：

玩家A添加玩家B到黑名单：

pre.
1.user_id=ID(A) frd_id=ID(B) frd_type=FRIENDTYPE_BLACKLIST（B是A的黑名单）
2.user_id=ID(B) frd_id=ID(A) frd_type=FRIENDTYPE_BEBLACKED（B被A加入黑名单）

这种方案的优点是数据库表结构比较简单，一张表就能够把所有好友类型都保存下来

但是缺点也比较明显，就是需要维护两条数据记录，如果出现异常有可能导致数据不一致，因此如果好友系统业务是多线程环境不适用
