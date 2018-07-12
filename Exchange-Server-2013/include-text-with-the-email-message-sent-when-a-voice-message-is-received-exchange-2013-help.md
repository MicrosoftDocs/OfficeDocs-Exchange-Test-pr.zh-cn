---
title: '与收到语音邮件时，发送该电子邮件包含文本: Exchange Online Help'
TOCTitle: 与收到语音邮件时，发送该电子邮件包含文本
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 51408253
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 与收到语音邮件时，发送该电子邮件包含文本

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-12-16_

您可以启用统一邮件 (UM) 语音邮件的用户收到一封语音邮件时发送的电子邮件中包含附加文本。默认情况下，有语音邮件附带的文本仅指示用户已收到语音邮件。但是，您可以创建自定义消息 UM 邮箱策略上的**当用户收到语音邮件**框中添加文本。例如，文本可以包括信息系统的安全策略和说明的正确的方式来处理您的组织中的语音邮件。添加的文字后，它将包括与 UM 邮箱策略相关联的已启用 UM 的用户收到语音邮件时，会发送每封电子邮件中。

> [!NOTE]  
> 语音邮件附带的自定义文本限制为 512 个字符，可以包括简单 HTML 文本。


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

## 使用 EAC 更改语音邮件附带的文本

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面 \>\&quot;邮件文本\&quot;的\&quot;当用户接收语音邮件时\&quot;文本框中，输入要包含在用户接收语音邮件时发送的电子邮件中的文本。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改语音邮件附带的文本

在此示例中，发送到与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的用户的语音邮件中包含附加文本\&quot;不要将语音邮件转发给此组织外部的用户\&quot;。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."

