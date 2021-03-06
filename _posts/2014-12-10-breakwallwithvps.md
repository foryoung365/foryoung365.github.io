---

layout: post
title: "如何用VPS+Shadowsocks科学上网"
description: "如何用VPS+Shadowsocks科学上网"
category: Tutorial
tags: [BreakWall]
---
{% include JB/setup %}

VPN
---

------------------------------------------------------------------------

最近GFW越来越凶残了，gmail上不去，google打不开，github奇慢无比，ruby gem源被墙，更不用说facebook,twitter之类常年被OOXX的网站了。每次开个国外网站都怀疑自己是不是还在用拨号上网连接。
网上各式各样的VPN也试了不少：

1.  [轻云](https://theqingyun.co/):一个月26块，提供3天1G流量免费试用，自动脚本配置，方便是方便了，不过速度真心只能呵呵了。
2.  [曲径](https://getqujing.com/zh-CN/):一个月50块，看起来很牛逼的样子，不提供试用(48小时内可以退款)，看过[他们的霸王条款](https://getqujing.com/zh-CN/tos)我就不想用了，有用过的童鞋不妨评论下。
3.  [云梯](https://www.ytvpn.com):同样不提供试用，只有年付，不过3天内可以退款，我买了最低级的套餐120一年，试用了一晚上，体验实在不算好。首先部分线路不稳定，我用台湾线路结果一小时后维护了（难道是我人品太好了？）。晚上高峰期网络极差，加载GMAIL用了3分钟还没加载完。很多线路访问被墙的网站也是404，不知道是什么原因。看youtube就更不用说了，只能看看240P，720P就卡到完全没反应。我已经申请退款了，不知道能不能退的回来。

各种折腾之后我只能放弃VPN，看最近Shadowsocks很火爆，于是转战VPS自己搭建Shadowsocks服务端。

VPS
---

------------------------------------------------------------------------

搜了下网上比较火的国外VPS提供商，大概有以下三个：

1.  [linode](https://www.linode.com/):口碑最好的服务器提供商，最低配10美刀一个月，对于我用来科学上网来说太贵了，伤不起。
2.  [DigitalOcean](https://www.digitalocean.com/):据说性价比很高，不过最低也是10美元。
3.  [vultr](https://www.vultr.com/):最低配5美元每月，首次充值送5刀。

因为我的用途是科学上网，所以我的评选标准只有两条——速度和价格，至于机器性能配置全部无视，带宽问题也不大，最多的是2T，最少的也有200G，反正我都用不完。上述三个网站都有提供多地的服务器机房可供选择，并且有每个机房的测速，你可以根据自己的网络实际情况挑选速度最快的。

这里有必要一提的是，测速的时候一定要关闭有些浏览器自带的加速下载功能，才能看到真实的网速，我这里用vultr的日本机房最快，每个月200GB流量。部署的时候操作系统选择CentOS,远程连接建议使用PuTTY,方便好用很多，当然也可以考虑vultr自带的浏览器界面。

搭建ShadowSocks服务端的[教程](http://www.v5fm.com/centos-shadowsocks.html)，这份写的很清楚，我就不再赘述了。

使用ShadowSocks
---------------

------------------------------------------------------------------------

客户端可以在[ShadowSocks官网](http://shadowsocks.cn/)下载，推荐使用ShadowSocks-gui，简单方便。

服务器IP就是VPS主机的IP，端口是你在VPS主机上启动ShadowSocks服务端使用的端口号，密码也是当时设置的密码，加密方式也需要相同。

本机的代理端口可以随便填，比如7070。[-使用Chrome浏览器可以下载一个SwitchySharp插件。
然后根据这份[设置教程](http://switchysharp.com/setting.html)进行配置，之后访问被墙的网站就会自动使用代理了。-]

更方便智能的方案参考[改进计划](#bettersolution)。

游戏代理
--------

------------------------------------------------------------------------

使用代理设置软件[ProxyCap](http://www.proxycap.com/)，把需要的游戏加进去就可以了。

改进计划
--------

------------------------------------------------------------------------

我有一个想法：

-   使用ShadowSocks做全局代理
-   国内外分流（即国内网站走直连，国外网站全部走代理）
-   已有的国内外分流方案基本上都是用[ChnRoutes](https://github.com/jimmyxu/chnroutes)来做，原理是通过修改路由表来区分国内外访问。但是很麻烦有木有，每次开VPN都要折腾一次。而且最坑爹的是每次执行那个脚本都要很久，而且路由表大了访问速度肯定慢。
-   ~~我打算把ShadowSocks做一些修改，直接把路由选择集成到ShadowSocks里面，这样就可以做到零配置国内外分流了。~~**发现最新版的ShaodowSocks-gui已经支持根据Pac文件自动分流了，文件戳[这里](/attachments/pac.txt)。把pac.txt直接扔到shadowSocks-gui的根目录下面即可。你需要根据自己的配置进行修改。**
    首先找到代理端口设置：

pre. var proxy = 'SOCKS5 127.0.0.1:7070; SOCKS 127.0.0.1:7070; DIRECT';

将其中的7070端口替换为你自己设定的本机代理端口。

然后找到本机不使用代理的设置：

pre.
if (isPlainHostName(host)
|| host = '127.0.0.1'
     || host = 'localhost') {
return 'DIRECT';
}

修改为

pre.
if (isPlainHostName(host)
|| host = '127.0.0.1'
     || host = 'localhost'
|| host === '你的VPS主机的IP') {
return 'DIRECT';
}

这个修改是因为你的VPS主机地址是国外地址，如果也走代理，就会出现死循环，所以必须将这个地址排除在代理列表之外。

最后将ShadowSocks里面的start on boot勾上，以后就可以完美无缝的科学上网了。
