---
title: '允许调用方没有来电要留下语音信息: Exchange Online Help'
TOCTitle: 允许调用方没有来电要留下语音信息
ms:assetid: 51367d98-e17c-4bcf-8b14-208bd1ac3af0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232040(v=EXCHG.150)
ms:contentKeyID: 50490544
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许调用方没有来电要留下语音信息

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以允许已启用 UM 的用户从匿名调用方接收语音邮件或阻止他们这样做。默认情况下，当用户启用统一邮件 (UM) 和语音邮件，它们可以接收调用匿名和不包含呼叫方 ID 信息。

在大多数情况下，调用由统一消息接收包含可用于确定传入的呼叫的呼叫方 ID。但是，传入呼叫不可能包括呼叫方 ID 信息，出于以下原因 ︰

  - 您组织的电话设备配置为不包含呼叫者 ID 信息。

  - 传入呼叫来自移动电话或外部电话。

  - 呼叫者已在其电话中禁用呼叫者 ID。

由于默认情况下启用了*AnonymousCallersCanLeaveMessages*参数，启用 UM 的用户可以收到语音邮件，即使呼叫方 ID 信息并不包括在内。如果*AnonymousCallersCanLeaveMessages*选项被禁用，并且已启用 UM 的用户接收调用不包含呼叫者 ID，调用将被标识为匿名，并启用 UM 的用户不会收到语音邮件。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 执行此过程之前，请确认已启用 UM 的用户的邮箱。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序允许接收来自匿名呼叫者的语音邮件

此示例允许启用了 UM 的用户 tonysmith@contoso.com 接收来自未包含呼叫者 ID 信息的传入呼叫的语音邮件。

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $true

