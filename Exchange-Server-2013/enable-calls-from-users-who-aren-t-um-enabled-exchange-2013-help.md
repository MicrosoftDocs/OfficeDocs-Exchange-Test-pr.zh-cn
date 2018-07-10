---
title: '允许从没有启用 UM 的用户的电话: Exchange Online Help'
TOCTitle: 允许从没有启用 UM 的用户的电话
ms:assetid: 3c39c6df-6d7a-469f-b92b-85b3f14bad31
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb267006(v=EXCHG.150)
ms:contentKeyID: 50490346
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许从没有启用 UM 的用户的电话

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

您可以启用或禁用呼叫的用户不能启用的统一邮件 (UM)。默认情况下，统一消息允许通过未经身份验证的调用方通过自动助理要转移到已启用 UM 的用户的传入呼叫。启用此选项，来自组织外部的用户可以将传输对启用 UM 的用户的呼叫。

如果已启用 UM 的用户禁用了此设置，用户的邮箱仍可使用目录搜索定位。但是，如果外部呼叫者尝试传输到用户，系统说，"我很抱歉，我不能向该用户呼叫转接。调用方将转移到该运算符，如果操作员已配置自动助理。如果没有操作员已配置自动助理，呼叫被转移到一个拨号计划运算符，，如果配置一个。如果已启用语音的自动助理、 双音多频 (DTMF) 回退自动助理或拨号计划上不配置任何运算符扩展，系统响应说，"对不起。运算符或按键的服务既不是可用。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 执行此过程之前，请确认已启用 UM 的用户的邮箱。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序启用来自未启用 UM 的用户的呼叫

此示例允许 Tony Smith 接收来自未启用 UM 的呼叫者的语音呼叫。

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers SearchEnabled

