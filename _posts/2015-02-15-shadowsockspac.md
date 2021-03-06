---

layout: post
title: "ShadowSocks-gui的PAC文件生成器"
description: "ShadowSocks-gui的PAC文件生成器"
category: Development
tags: [PacGenerotor]
---
{% include JB/setup %}

起因
----

------------------------------------------------------------------------

现在一直在用ShadowSocks科学上网（[教程](http://foryoung365.github.io/tutorial/2014/12/10/breakwallwithvps/)）。不过每到一处新地方，都要重新配置一次，然后生成PAC文件，根据你的代理服务器修改PAC文件。虽然步骤不多，但是也很麻烦。
之前也试过将ShadowSocks的exe，配置文件，pac都打包起来上传到网盘，换电脑也可以下载，但是频繁的升级exe和更新pac文件也是个麻烦事，而且每次pac更新完都要再修改一次，又要上传网盘，这种重复实在不能忍。

今天一怒之下终于用Python写了一个PAC自动生成器，可以自动下载最新版本的**ShadowSocks-gui**，并且根据你的**ShadowSocks-gui**的配置文件自动生成对应的PAC文件。这样我只要把gui-config.json和GenPac.exe一起打包上传到网盘。以后在新的电脑上用只需要双击**GenPac.exe**就收工了。

另外我在GitHub建了个[代码库(ShadowSocksPac)](https://github.com/foryoung365/ShadowSocksPac)，提供了源代码，基于leaskh的flora_Pac项目修改而成，目前只支持**ShadowSocks-gui**，要求2.3以上版本（2.3版本的配置文件格式与之前不同）。[GenPac.exe文件可从这里下载](/attachments/GenPac.zip)，感兴趣的可以自己去下载源代码，欢迎补充完善或者在本站评论区提供建议。这个还是自用为主，不喜勿喷。

使用说明
--------

------------------------------------------------------------------------

1.  首先，你需要一个**ShadowSocks-gui**的配置文件，通常文件名为**gui-config.json**。如果还没有的话，也没关系，可以去[**ShadowSocks-gui**](http://sourceforge.net/projects/shadowsocksgui/files/dist/)的发布页面下载一个**ShadowSocks-gui**文件,或者直接执行:

pre.
GenPac.py

会帮你自动下载一个最新版本的**ShadowSocks-gui**,启动后双击任务栏右下角图标，添加上你的代理服务器地址和端口等信息，然后在系统代理模式中勾上PAC模式。打开**ShadowSocks-gui**的安装目录以后就会看到已经生成了一个**gui-config.json**文件和一个**pac.txt**文件。

1.  然后将Python脚本（需要安装Python）或者GenPac.exe复制到**ShadowSocks-gui**的安装目录下，如果是脚本需要运行如下命令：

pre.
GenPac.py -f[FileName] -d[0 or 1]

*-f*是指定配置文件的文件名，如果不在同一个目录，需要提供完整路径或相对路径，默认值是**gui-config.json**，所以一般情况下你可以省略这个参数。生成的PAC文件名是**pac.txt**，会自动替换掉原来的文件，同时会将你的配置替换进PAC文件中。
*-d*表示是否需要从<http://sourceforge.net/projects/shadowsocksgui>自动下载最新版的**ShadowSocks-gui**，默认是会下载。
右击任务栏ShadowSocks的图标，选择Enable，之后你就可以开始科学上网啦。同时访问国内网站，不会经过代理，而访问国外或者被墙的网站，会自动通过ShadowSocks代理。是不是很方便？

在别的电脑使用
--------------

------------------------------------------------------------------------

以后在新的电脑上用怎么操作最省事？你只需要将**gui-config.json**和**GenPac.exe**两个文件一起打包上传到网盘中。然后在新电脑上：

1.  从网盘下载打包文件并解压到硬盘，如F:ShadowSocks
2.  双击**GenPac.exe**，待文件生成完毕后，打开**ShadowSocks-gui**即可。

果断变得轻松加愉快了吧，O(∩_∩)O哈哈~
