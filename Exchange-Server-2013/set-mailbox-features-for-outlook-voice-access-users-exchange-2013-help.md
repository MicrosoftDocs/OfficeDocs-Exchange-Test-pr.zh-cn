---
title: '设置 Outlook Voice Access 用户的邮箱功能: Exchange Online Help'
TOCTitle: 设置 Outlook Voice Access 用户的邮箱功能
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50556526
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置 Outlook Voice Access 用户的邮箱功能

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

Outlook Voice Access 包含两个界面：电话用户界面 (TUI) 和语音用户界面 (VUI)。用户在 Exchange 2013 中使用统一消息 (UM) 系统访问某个邮箱时，可以为启用了 UM 的用户配置 TUI 设置。在 UM 邮箱策略上为启用 UM 的用户修改 TUI 设置时，所做更改将影响与 UM 邮箱策略关联的所有用户。可以在 UM 邮箱策略上修改下列 TUI 设置：

  - 对语音邮件的无 PIN 访问

  - 对其他邮件的语音响应

  - 对其日历的 TUI 访问

  - 对目录的 TUI 访问

  - 对其电子邮件的 TUI 访问

  - 对其个人联系人的 TUI 访问

> [!NOTE]
> 只能使用命令行管理程序为启用了 UM 的用户修改 Outlook Voice Access TUI 设置。


有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序修改 UM 邮箱策略上的 TUI 设置

此示例将对名为 `MyUMMailboxPolicy` 的 UM 邮箱策略设置 TUI 相关设置。

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true

