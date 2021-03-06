---

layout: post
title: "RakNet参考手册索引"
description: "RakNet参考手册索引"
category: Development
tags: [RakNet]
---
{% include JB/setup %}

RakNet开源免费了，接下来准备学习一下，计划把RakNet的文档做个翻译。就从手册开始吧。[原文链接](http://www.jenkinssoftware.com/raknet/manual/index.html)。

介绍
----

------------------------------------------------------------------------

手册最后更新时间 2012-11-19。查看readme.txt文件获取当前版本号。

RakNet是为游戏或者其他高性能网络应用设计的一套高性能的网络API。RakNet致力于提供现代游戏所需的绝大部分的功能特性，如Master Server（主服务器），autopatcher(自动更新),语音聊天和跨平台兼容性等。RakNet当前支持Windows, PlayStation 3, XBOX 360, PlayStation Vita, Linux, Mac, the iPhone[1], Android,和Windows Phone 8。

快速入门
--------

------------------------------------------------------------------------

[多人游戏的组成](http://www.jenkinssoftware.com/raknet/manual/multiplayergamecomponents.html)
[系统概览](http://www.jenkinssoftware.com/raknet/manual/systemoverview.html)
[实现细节](http://www.jenkinssoftware.com/raknet/manual/detailedimplementation.html)
[教程](http://www.jenkinssoftware.com/raknet/manual/tutorial.html)
[编译设置(Visual Studio)](http://www.jenkinssoftware.com/raknet/manual/compilersetup.html)
[编译设置(XCode)](http://www.jenkinssoftware.com/raknet/manual/compilersetup_xcode.html)
[可选的第三方依赖项](http://www.jenkinssoftware.com/raknet/manual/dependencies.html)
[操作方式](http://www.jenkinssoftware.com/forum/index.php?topic=584.0)

教学视频
--------

------------------------------------------------------------------------

[介绍：主要特性](http://www.youtube.com/watch?v=sez3o00uCqU)
[教程1：RPC3](http://www.jenkinssoftware.com/raknet/manual/RPC3Video.htm)
[教程2：ReplicaManager3](http://www.jenkinssoftware.com/raknet/manual/ReplicaManager3Video.htm)
[教程3：Autopatcher](http://www.jenkinssoftware.com/raknet/manual/AutopatcherVideo.htm)
[教程4：一个覆盖了对象复制，组队，玩家作为主机的房间和大厅，NAT遍历，和主机迁移的完整实例](http://www.youtube.com/watch?v=w4OUGeLKcss)

特性视频
--------

------------------------------------------------------------------------

[使用SQLiteClientLoggerPlugin记录网络化日志](http://www.jenkinssoftware.com/raknet/manual/SQLite3LoggerPluginVideo.html)

基础内容
--------

------------------------------------------------------------------------

[启动](http://www.jenkinssoftware.com/raknet/manual/startup.html)
- 启动RakPeerInterface, 和线程休眠定时器详解

[连接](http://www.jenkinssoftware.com/raknet/manual/connecting.html)
- 如何发现并连接到其他系统，以及如何解决这过程中遇到的问题

[创建消息包](http://www.jenkinssoftware.com/raknet/manual/creatingpackets.html)
- 如何使用结构体和比特流创建自定义的消息包，以及如何编码时间戳。

[发送消息包](http://www.jenkinssoftware.com/raknet/manual/sendingpackets.html)
- 如何发送就绪的消息包，以及该使用哪些参数。

[接收消息包](http://www.jenkinssoftware.com/raknet/manual/receivingpackets.html)
- 如何将网络原始数据转换为可解析的结构体或者比特流的消息包。

[系统地址](http://www.jenkinssoftware.com/raknet/manual/systemaddresses.html)
- 介绍在消息包和某些函数参数中使用系统地址结构的作用和意义。

[比特流](http://www.jenkinssoftware.com/raknet/manual/bitstreams.html)
- RakNet中的bitstream类的概览，以及API的使用。

[可靠性类型](http://www.jenkinssoftware.com/raknet/manual/reliabilitytypes.html)
- 介绍用来发送控制数据的参数。

[网络消息](http://www.jenkinssoftware.com/raknet/manual/networkmessages.html)
- 消息概览，以及发送消息给用户的API介绍。这些API在**MessageIdentifier.h**中也有列出。

[给消息包打上时间戳](http://www.jenkinssoftware.com/raknet/manual/timestamping.html)
- 介绍打时间戳的意义。

[网络ID对象](http://www.jenkinssoftware.com/raknet/manual/networkidobject.html)
- 一个给每个类实例分配一个所有系统共享的唯一ID的工具类。

[统计信息](http://www.jenkinssoftware.com/raknet/manual/statistics.html)
- RakNet提供的统计信息。

[安全连接](http://www.jenkinssoftware.com/raknet/manual/secureconnections.html)
- 如何激活和使用安全连接。

[主服务器](http://masterserver2.raknet.com/)
- RakNet提供的主机主服务器，用以发现互联网上的其他游戏。

[云主机](http://www.jenkinssoftware.com/raknet/manual/cloudhosting.html)
- 使用云主机服务配置RakNet

[Rackspace[2]接口](http://www.jenkinssoftware.com/raknet/manual/rackspaceinterface.html)
- 用于Rackspace的C++接口，使你能够通过代码在服务器上创建、删除、重启、镜像和进行其他操作。

[NAT 遍历体系结构](http://www.jenkinssoftware.com/raknet/manual/nattraversalarchitecture.html)
- 如何结合UPNP， NAT 类型检测， NAT穿透，和Router2使P2P连接快速有效的完成。

[预处理器指令](http://www.jenkinssoftware.com/raknet/manual/preprocessordirectives.html)
- 允许你使用不同的代码设置重建库。

[自定义内存管理](http://www.jenkinssoftware.com/raknet/manual/custommemorymanagement.html)
- 控制台，内存追踪等。

[IPV6支持](http://www.jenkinssoftware.com/raknet/manual/custommemorymanagement.html)
- 下一代IP地址格式。

[Marmalade集成](http://www.jenkinssoftware.com/raknet/manual/marmalade.html)
- 集成了用于IOS和安卓平台的Marmalade SDK。

插件
----

------------------------------------------------------------------------

[Plugin Interface 2](http://www.jenkinssoftware.com/raknet/manual/plugininterface.html)
- 所有插件的基类

[Autopatcher](http://www.jenkinssoftware.com/raknet/manual/autopatcher.html)
- RakNet中包含的自动更新模块概览。

[RPC3](http://www.jenkinssoftware.com/raknet/manual/RPC3Video.htm)
- 使用本地参数列表调用C和C++函数，使用Boost的扩展功能。

[RPC4](http://www.jenkinssoftware.com/raknet/manual/rpc4.html)
- 调用C函数，无需其他外部依赖。

[Connection Graph](http://www.jenkinssoftware.com/raknet/manual/connectiongraph.html)
- 一款显示整个网络监控图像的插件。

[Directory Delta Transfer](http://www.jenkinssoftware.com/raknet/manual/directorydeltatransfer.html)
- 在目录间发送变更的或者丢失的文件。要求有一个简单的autopatcher用来传输关卡，皮肤等。

[File List Transfer](http://www.jenkinssoftware.com/raknet/manual/filelisttransfer.html)
- 一款用来发送文件列表，并且编码到FileList结构中的插件

[Fully COnnected Mesh 2](http://www.jenkinssoftware.com/raknet/manual/fullyconnectedmesh2.html)
- 一款端到端游戏的插件，具有主机选择，验证到网络连接的功能。

[Lobby2Client - PC](http://www.jenkinssoftware.com/raknet/manual/lobby.html)
- 使用PostgreSQL作为后端数据库，用来存储玩家，好友，氏族消息等游戏数据。

[Lobby2Client - Steam](http://www.jenkinssoftware.com/raknet/manual/steamlobby.html)
- 基于Streamworks的后端，使用Lobby2的接口。

[Lobby2Client - PS3](http://www.jenkinssoftware.com/raknet/manual/ps3lobby.html)
- 基于PS3 NP的后端，使用Lobby2的接口。

[Lobby2Client - XBOX 360](http://www.jenkinssoftware.com/raknet/manual/xbox360lobby.html)
- 基于XBOX LIVE 后端，支持语音聊天，使用Lobby2 接口，支持RakVoiceXBOX360Plugin和FullyConnectedMesh2。

[Lobby2Client - Games for Windows Live](http://www.jenkinssoftware.com/raknet/manual/gfwllobby.html)
- 和XBOX 360 后端相同，但是运行在Windows上。

[Message Filter](http://www.jenkinssoftware.com/raknet/manual/messagefilter.html)
- 基于发送者过滤掉不需要的网络消息，增加安全性。

[NAT type detection](http://www.jenkinssoftware.com/raknet/manual/nattypedetection.html)
- 找出你当前的NAT模式，将无法单独链接的玩家能够区分开来。

[NAT punchthrough](http://www.jenkinssoftware.com/raknet/manual/natpunchthrough.html)
- 连接处在NAT网络的玩家。端到端连接，语音交流或者允许玩家主持自己的服务器所必须的插件。

[Packet Logger](http://www.jenkinssoftware.com/raknet/manual/packetlogger.html)
- 将网络负载记录到屏幕，文件或者其他地方。

[RakVoice](http://www.jenkinssoftware.com/raknet/manual/rakvoice.html)
- RakVoice的概览。和**RakVoice.h**相关的完整实现和功能细节。

[Ready Event](http://www.jenkinssoftware.com/raknet/manual/readyevent.html)
- 使一组系统在一个通用标识符上全部准备完成时保持同步，在端到端环境中同时开始游戏或者在回合制游戏中同步回合进度时很有用。

[Replica Manager 3](http://www.jenkinssoftware.com/raknet/manual/replicamanager3.html)
- 一款管理游戏对象和玩家的管理器插件，能够让序列化，区域和对象创建和销毁更简单。

[Router2](http://www.jenkinssoftware.com/raknet/manual/router.html)
- 发送网络消息给一个或者多个没有直接连接的远程系统。

[SQLite3LoggerPlugin](http://www.jenkinssoftware.com/raknet/manual/sqlite3loggerplugin.html)
- 使用SQLite创建网络化的记录文件，基于SQLite3Plugin。

[SQLite3Plugin](http://www.jenkinssoftware.com/raknet/manual/sqlite3plugin.html)
- 使用SQLite通过网络执行语句（轻量数据库的替代品）

[TeamManager](http://www.jenkinssoftware.com/raknet/manual/teammanager.html)
- 管理队伍和队伍成员列表，支持C/S架构和P2P架构

[TwoWayAuthentication](http://www.jenkinssoftware.com/raknet/manual/twowayauthentication.html)
- 实现[两步验证](http://en.wikipedia.org/wiki/Mutual_authentication),校验预先指示的密码而无需传输这个密码。

C#和SWIG
---------

------------------------------------------------------------------------

[Swig 教程](http://www.jenkinssoftware.com/raknet/manual/swigtutorial.html)
- 如何用C#和SWIG和possibly Mono来运行RakNet。

[Unity集成](http://www.jenkinssoftware.com/raknet/manual/csharpunity.html)
- 如何在Unity中使用RakNet，以及如何升级到4.X版本

工具集
------

------------------------------------------------------------------------

[Crash Reporter](http://www.jenkinssoftware.com/raknet/manual/crashreporter.html)
- 当应用崩溃时，发送小型转储，将其写入磁盘或者发送邮件。

[Console Server](http://www.jenkinssoftware.com/raknet/manual/consoleserver.html)
- 通过安全的RakNet或者telnet连接到基于文字的后门，能够执行预先指定的命令或者任意的命令字符串。

[Email Sender](http://www.jenkinssoftware.com/raknet/manual/emailsender.html)
- Crash Reporter用来发送邮件（基于TCP协议）。

[String Compressor/ String Table](http://www.jenkinssoftware.com/raknet/manual/stringcompressor.html)
- 用来编码字符串，使用更少的带宽和提高安全性。

[TCP Interface](http://www.jenkinssoftware.com/raknet/manual/tcpinterface.html)
- TCP连接封装。

3D示例
------

------------------------------------------------------------------------

[Ogre 3D 插补示例](http://www.jenkinssoftware.com/raknet/manual/ogre3dinterpdemo.html)
- 使用[Ogre 3D](http://www.ogre3d.org/)展示在客户端和服务器之间爆爆米花的示例，使用[ReplicaManager3](http://www.jenkinssoftware.com/raknet/manual/replicamanager3.html)。

[Irrlicht FPS示例](http://www.jenkinssoftware.com/raknet/manual/irrlichtfpsdemo.html)
- 使用[Irrlicht](http://irrlicht.sourceforge.net/)来显示3D FPS示例，使用带有NAT穿透的P2P，同时也使用了[ReplicaManager3](http://www.jenkinssoftware.com/raknet/manual/replicamanager3.html)。

技术设计文档
------------

------------------------------------------------------------------------

[UML图表](http://www.jenkinssoftware.com/raknet/manual/RakNetUML.jpg)
[潜在的蓝牙支持](http://www.jenkinssoftware.com/raknet/manual/bluetooth.html)

数据结构
--------

------------------------------------------------------------------------

DS_BinarySearchTree.h - [二叉搜索树](http://en.wikipedia.org/wiki/Binary_search_tree)和[AVL平衡](http://en.wikipedia.org/wiki/AVL_tree)的二叉搜索树。
DS_BPlusTree.h - 用于快速查找，插入，删除的[B+树](http://en.wikipedia.org/wiki/B%2B_tree)。
DS_BytePool.h - 返回预定义大小的数据块以避免内存碎片。
DS_ByteQueue.h - 为读写字符序列化的队列。
DS_Heap.h - [堆数据结构](http://en.wikipedia.org/wiki/Heap_%28data_structure%29)，包括最小堆和最大堆。
DS_HuffmanEncodingTree.h - [霍夫曼编码树](http://en.wikipedia.org/wiki/Huffman_coding), 用来查找给定频率表的最小的按位表达.
DS_HuffmanEncodingTreeFactory.h - 创建霍夫曼编码树的实例.
DS_HuffmanEncodingTreeNode.h -霍夫曼编码树的节点.
DS_LinkedList.h - 标准[链表](http://en.wikipedia.org/wiki/Linked_list).
DS_List.h - 动态[数组](http://en.wikipedia.org/wiki/Array) (有时被误称为vector). Also doubles as a [栈](http://en.wikipedia.org/wiki/Stack_%28data_structure%29).
DS_Map.h - ([关联数组](http://en.wikipedia.org/wiki/Associative_array)) 根据每个元素的排序key排序的有序的list.
DS_MemoryPool.h - 分配和释放复用固定大小结构的实例，以减少内存碎片。
DS_Multilist_h - (Added 4/8/2009) 将list, stack, queue和ordered list结合在一个类中，并且提供相同的接口.
DS_OrderedChannelHeap.h - 根据节点关联channel的相对权重返回节点的最大堆。用于基于优先级的任务调度。
DS_OrderedList.h - 根据任何key排序的List, 使用[快速排序](http://en.wikipedia.org/wiki/Quicksort)。
DS_Queue.h - 使用数组实现的标准[队列](http://en.wikipedia.org/wiki/Queue_%28data_structure%29)。
DS_QueueLinkedList.h - 使用链表实现的标准队列。
DS_RangeList.h - 保存一个数值列表，如果这些数值是序列的，用一个范围来表示他们，而不是单独的元素。在存储通常情况下是序列的大量数值时很有用。
DS_Table.h - 包含行和列的[表](http://en.wikipedia.org/wiki/Table_%28database%29)，以及表的操作。
DS_Tree.h - 非周期性的[图](http://en.wikipedia.org/wiki/Graph_%28data_structure%29)。
DS_WeightedGraph.h - 带权图，用于使用[迪杰斯特拉算法](http://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)的路由。
RakString - String实现，比std::string快4.5倍。

技术支持
--------

------------------------------------------------------------------------

[FAQ](http://www.jenkinssoftware.com/raknet/manual/faq.html)
[断线调试](http://www.jenkinssoftware.com/raknet/manual/debuggingdisconnects.html)
[编程小贴士](http://www.jenkinssoftware.com/raknet/manual/programmingtips.html)
[版本记录](http://www.jenkinssoftware.com/raknet/manual/revisionlog.html)
[论坛](http://www.jenkinssoftware.com/forum)
[给作者发邮件](rakkar@jenkinssoftware.com)

[1] 这里应该指的是IOS。

[2] 一家服务器提供商的名字。
