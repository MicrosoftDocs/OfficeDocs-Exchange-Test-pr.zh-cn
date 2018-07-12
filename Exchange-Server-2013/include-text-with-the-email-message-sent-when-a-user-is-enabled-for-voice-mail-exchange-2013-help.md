---
title: '为用户启用语音邮件时发送的电子邮件消息中包括文本: Exchange Online Help'
TOCTitle: 为用户启用语音邮件时发送的电子邮件消息中包括文本
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51408213
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为用户启用语音邮件时发送的电子邮件消息中包括文本

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-12-16_

当用户的邮箱启用统一消息 (UM) 语音邮件时，发送一封电子邮件，欢迎您到统一消息的用户。此消息包含 PIN 信息用户将使用第一次访问语音邮件系统。

您可以自定义发送欢迎电子邮件中的 UM 邮箱策略上的**用户启用统一邮件时**框中添加文本的文本。您可以包括诸如 UM 技术支持电话号码或其他 Outlook Voice Access 号码等信息。添加的文字后，它将包括与 UM 邮箱策略相关联的用户启用统一邮件时发送的电子邮件消息中。

> [!NOTE]  
> 添加到欢迎邮件中的自定义文本限制为 512 个字符，并且它可以包含简单的 HTML 文本。


有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 自定义邮箱启用统一消息时发送的文本

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面\>\&quot;邮件文本\&quot;的\&quot;当为用户启用统一消息时\&quot;文本框中，输入在为用户启用统一消息语音邮件后要包含在发送的电子邮件中的文本。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序自定义邮箱启用统一消息时发送的文本

此示例使与 UM 邮箱策略关联的启用了 UM 的用户能够接收有关 UM 和 用户可用来通过电话访问其邮箱的 Outlook Voice Access 号码的附加说明。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."

