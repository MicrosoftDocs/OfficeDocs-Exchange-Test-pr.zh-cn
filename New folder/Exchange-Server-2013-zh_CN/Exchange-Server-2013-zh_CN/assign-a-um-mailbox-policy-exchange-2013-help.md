---
title: '将 UM 邮箱策略分配: Exchange Online Help'
TOCTitle: 将 UM 邮箱策略分配
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 50491524
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将 UM 邮箱策略分配

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-30_

当您为用户启用统一邮件 (UM) 和语音邮件时，您必须选择将与该用户的邮箱关联的 UM 邮箱策略。您可以更改用户已启用了 UM 之后，与用户的邮箱关联的 UM 邮箱策略。

创建 UM 邮箱策略，以将一组通用的策略或安全设置应用于已启用 UM 的用户的邮箱的集合。您可以使用 UM 邮箱策略应用设置如下所示 ︰

  - PIN 策略

  - 拨号限制

  - 其他常规 UM 邮箱策略属性

> [!NOTE]
> 每次创建 UM 拨号计划时，将创建默认 UM 邮箱策略。您可以删除默认 UM 邮箱策略或创建基于您的组织需要的其他 UM 邮箱策略。


有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认该用户启用了统一消息。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 更改分配给启用 UM 的用户的 UM 邮箱策略

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择要更改 UM 邮箱策略的邮箱。

3.  在详细信息窗格的\&quot;电话和语音功能\&quot; \>\&quot;统一消息\&quot;下，单击\&quot;视图详细信息\&quot;。

4.  在\&quot;UM 邮箱\&quot;页上，单击\&quot;UM 邮箱设置\&quot;，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

5.  在\&quot;UM 邮箱\&quot;页上 \> 靠近\&quot;UM 邮箱策略\&quot;，单击\&quot;浏览\&quot;找到用户的 UM 邮箱策略。

6.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改分配给启用 UM 的用户的 UM 邮箱策略

此示例将名为 Tony Smith 的启用 UM 的用户与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略相关联。

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

