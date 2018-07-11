---
title: '检索语音邮件 PIN 信息: Exchange Online Help'
TOCTitle: 检索语音邮件 PIN 信息
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54652228
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 检索语音邮件 PIN 信息

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-03_

可以为启用了统一消息 (UM) 的用户检索 PIN 信息。在用户启用 UM 并且 PIN 生成或创建之后，PIN 就被加密并且存储在用户的邮箱中。

为启用了 UM 的用户检索 PIN 信息时，将使用用户邮箱中以加密格式存储的 PIN 数据计算为您返回的信息。通过此步骤可以查看用户邮箱中的信息，并指示用户是否已锁定邮箱。

有关与 PIN 安全相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些过程之前，请先确认用户的邮箱已启用 UM。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 为已启用 UM 的用户检索 PIN 信息

1.  在 EAC 中，导航到\&quot;收件人\&quot;。在列表视图中，选择要查看的用户邮箱。

2.  在\&quot;详细信息\&quot;窗格的\&quot;电话和语音功能\&quot;下，单击\&quot;查看详细信息\&quot;。

3.  在\&quot;UM 邮箱\&quot;页 \>\&quot;UM 邮箱设置\&quot;上，查看用户的\&quot;PIN 状态\&quot;。在该页面上，您还可以为用户重置语音信箱的 PIN。

## 使用命令行管理程序为已启用 UM 的用户检索 PIN 信息

此示例将显示用户 ID、PIN 是否已过期、UM 邮箱是否已锁定，以及 Tony 是否为首次用户。

    Get-UMMailboxPIN -identity tony@contoso.com

