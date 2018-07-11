---
title: '设置 Outlook Voice Access 用户邮箱功能: Exchange Online Help'
TOCTitle: 设置 Outlook Voice Access 用户邮箱功能
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50556627
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置 Outlook Voice Access 用户邮箱功能

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

当用户访问使用Outlook语音访问统一邮件 (UM) 系统使用电话用户界面 (TUI) 设置。当您修改已启用 UM 的用户的 TUI 配置设置时，您可以修改属性和它们的值对启用 UM 的用户的邮箱。

可以更改启用 UM 的用户的以下 TUI 设置：

  - 允许订阅者访问

  - 允许通过 TUI 访问日历

  - 允许通过 TUI 访问电子邮件

  - 允许自动语音识别

有关与 UM 用户相关的其他管理任务，请参阅[设置 Outlook Voice Access 用户邮箱功能](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些步骤之前，请确认，现有的Exchange收件人启用统一邮件和语音邮件。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序修改单个启用 UM 的用户的 TUI 设置

此示例使用 TUI 为启用 UM 的 Tony Smith 用户启用日历和电子邮件访问。

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True

> [!NOTE]  
> TUI 的用户设置，还提供在 UM 邮箱策略上。修改 UM 邮箱策略上的 TUI 设置会影响所有用户与该 UM 邮箱策略相关联。有关如何修改 UM 邮箱策略上的 TUI 设置的详细信息，请参阅<a href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">设置 Outlook Voice Access 用户的邮箱功能</a>。

