---
title: '与收到传真邮件时，发送该电子邮件包含文本: Exchange Online Help'
TOCTitle: 与收到传真邮件时，发送该电子邮件包含文本
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 51408215
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 与收到传真邮件时，发送该电子邮件包含文本

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

用户谁启用统一邮件 (UM) 语音邮件和传真已启用，并在 UM 邮箱策略已正确配置要使用的传真合作伙伴提供接收到传真邮件时发送的电子邮件中，可以包含附加的文本。默认情况下，包括启用 UM 的用户接收的传真邮件的文本仅指示用户已收到的传真消息。但是，您可以创建自定义消息 UM 邮箱策略上的**当用户收到传真邮件**框中添加文本。例如，文本可以包括信息系统的安全策略和说明来处理您的组织中的传真消息的正确方式。添加的文字后，它将包括与该 UM 邮箱策略相关联的已启用 UM 的用户收到传真邮件时发送每封电子邮件中。

> [!NOTE]  
> 传真邮件附带的自定义文本最多为 512 个字符，并且可以包含简单的 HTML 文本。


有关传真合作伙伴的详细信息，请参阅[Microsoft 查明其传真合作伙伴](https://go.microsoft.com/fwlink/?linkid=190238)。

有关与传真相关的更多管理任务，请参阅[传真的步骤](faxing-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 更改传真邮件附带的文本

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面\>\&quot;邮件文本\&quot;的\&quot;当用户接收传真邮件时\&quot;文本框中，输入要包含在当用户的邮箱收到传真邮件时发送的电子邮件中的文本。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改传真邮件附带的文本

本示例为启用了 UM 且与 UM 邮箱策略关联的用户提供了有关如何打开其邮箱中收到的传真邮件的附加说明。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."

