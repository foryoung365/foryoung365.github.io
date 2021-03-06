---

layout: post
title: "一种回合制战斗过程的记录方式"
description: "一种回合制战斗过程的记录方式"
category: Development
tags: [GameDevelopment]
---
{% include JB/setup %}

回合制战斗的页游，需要将战斗过程在服务端全部计算完成后再下发给客户端，并且还需要将战斗过程保存起来，让第三方直接查看。

将战斗的过程以动作为单位分解成多种消息，之后将多种战斗消息封装在一个消息打包器中下发给客户端。客户端从打包消息中按字节流的方式还原

出战斗消息，再解析消息进行表现。保存战斗过程只需要保存被打包完的字节流消息即可。

**MsgPacker(2000+300)**

pre.
enum MSGPACKER_ACTION
{
MSGPACKER_None = 0, //无效
MSGPACKER_BattleNew = 1, //开始新的战斗
MSGPACKER_BattleMore = 2, //一次未发完的后续
MSGPACKER_BattleEnd = 3, //战斗过程结束
//s2c dwData = BATTLE_WINNER
};

pre.
#pragma pack(push, 1)
typedef struct
{
MSGHEAD_DEFINE
USHORT usAction;
DWORD dwData;
DWORD dwAmount; //后面有几个消息
UCHAR ucMsg[0]; //各种战斗消息
}MSG_Info;
#pragma pack(pop)

**MsgBattle(2000+301)**

pre.
enum MSGBATTLE_ACTION
{
MSGBATTLE_None, = 0, //无效
MSGBATTLE_BattleStart = 1, //战斗开始
MSGBATTLE_BattleEnd = 2, //战斗结束
MSGBATTLE_RoundStart = 3, //回合开始
MSGBATTLE_RoundEnd = 4, //回合结束
MSGBATTLE_HandStart = 5, //交手开始
MSGBATTLE_HandEnd = 6, //交手结束
};

pre.
#pragma pack(push, 1)
typedef struct
{
MSGHEAD_DEFINE
USHORT usAction;
DWORD dwData;
}MSG_Info;
#pragma pack(pop)

**MsgNormalAttack(2000+302)**

pre.
enum DAMAGE_TYPE
{
DAMAGETYPE_None = 0, //无效
DAMAGETYPE_Normal = 1, //正常攻击
DAMAGETYPE_CounterAttack= 2, //反击
};

pre.
enum MSGNORMALATTACK_ACTION
{
MSGNORMALATTACK_None = 0, //无效
MSGNORMALATTACK_PhyAtk = 1, //物理攻击
MSGNORMALATTACK_MgcAtk = 2, //策略攻击
};

pre.
#pragma pack(push, 1)
typedef struct
{
MSGHEAD_DEFINE
USHORT usAction;
OBJID idAttacker;
OBJID idTarget;
USHORT usDamageType;
DWORD dwDamage; //受击方受到的伤害
}MSG_Info;
#pragma pack(pop)

**MsgMagicAttack(2000+303)**

pre.
enum MSGMAGICATTACK_ACTION
{
MSGMAGICATTACK_None = 0, //无效
MSGMAGICATTACK_PhyAttack = 1, //物理型技能攻击
MSGMAGICATTACK_MgcAttack = 2, //策略型技能攻击
};

pre.
#pragma pack(push, 1)
typedef struct
{
OBJID idRole;
USHORT usDamageType;
DWORD dwDamage; //受击方受到的伤害
}MagicRoleInfo_t;
#pragma pack(pop)

pre.
#pragma pack(push, 1)
typedef struct
{
MSGHEAD_DEFINE
USHORT usAction;
OBJID idAttacker;
OBJID idMagic;
UCHAR ucAmount; //受到技能影响的单位数量
MagicRoleInfo_t setInfo[0];
}MSG_Info;
#pragma pack(pop)

**MsgHitAction(2000+304)**

pre.
enum MSGHITACTION //受击类型
{
HITACTION_None = 0, //无效
HITACTION_Normal = 1, //正常
HITACTION_Dodge = 2, //闪避
HITACTION_Fend = 3, //抵挡
HITACTION_Bang, = 4, //暴击
};

pre.
#pragma pack(push, 1)
typedef struct
{
MSGHEAD_DEFINE
USHORT usAction;
OBJID idRole;
}MSG_Info;
#pragma pack(pop)

**MsgBattleStatus(2000+305)**

pre.
enum MSGBATTLESTATUS_ACTION
{
MSGBATTLESTATUS_None = 0, //无效状态
MSGBATTLESTATUS_Add = 1, //增加状态
MSGBATTLESTATUS_Del = 2, //删除状态
};

pre.
#pragma pack(push, 1)
typedef struct
{
MSGHEAD_DEFINE
USHORT usAction;
OBJID idRole;
OBJID idStatusType; //状态类型ID
int nParam1; //状态参数1
int nParam2; //状态参数2
}MSG_Info;
#pragma pack(pop)

**MsgBattleAttrib(2000+306)**

pre.
enum MSGBATTLEATTRIB
{
MSGBATTLEATTRIB_None = 0, //无效
MSGBATTLEATTRIB_AddLife = 1, //生命值
MSGBATTLEATTRIB_AddAnger = 2, //气势
};

pre.
#pragma pack(push, 1)
typedef struct
{
MSGHEAD_DEFINE
USHORT usAction;
OBJID idRole;
USHORT usReason;
int nData; //正值增加，负值减少
}MSG_Info;
#pragma pack(pop)

如果以文字的方式解析消息将得到如下的战斗日志（当然，客户端是以FLASH的形式表现的）：

pre.
-~~战斗开始-~~
-~~第一回合开始-~~
-~~第一次交手开始-~~
角色1001使用攻击，对角色2001造成了1259点物理伤害
角色2001被暴击了
角色1001的气势增加了25
角色2001的气势增加了25
-~~第一次交手结束-~~
-~~第二次交手开始-~~
...
-~~第二次交手结束-~~
...
-~~第一回合结束-~~
---
-~~战斗结束-~~
