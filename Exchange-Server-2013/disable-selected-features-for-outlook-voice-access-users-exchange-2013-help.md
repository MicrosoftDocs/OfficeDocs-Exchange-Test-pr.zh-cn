---
title: '禁用选定的 Outlook Voice Access 用户功能: Exchange Online Help'
TOCTitle: 禁用选定的 Outlook Voice Access 用户功能
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50556552
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用选定的 Outlook Voice Access 用户功能

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

Outlook语音访问包含两个接口 ︰ 电话用户界面 (TUI) 和语音用户界面 (VUI)。默认情况下，当用户拨入Outlook语音访问他们可以访问他们的日历、 电子邮件和个人联系人，并在目录中搜索。外壳程序可用于防止用户访问一个或多个这些功能在使用Outlook语音访问来访问其邮箱时。修改统一邮件 (UM) 邮箱策略上的Outlook语音访问功能时，所做的更改将影响与该 UM 邮箱策略相关联的所有用户。

可以针对 UM 邮箱策略禁用用户对以下 Outlook Voice Access 功能的访问：

  - 日历

  - 目录

  - Email

  - 个人联系人

有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

外壳程序还可用于禁用单个启用 UM 的用户的邮箱上的Outlook语音访问功能。执行此操作时，将仅针对该用户禁用功能。尽管您不能禁用单个用户的 UM 邮箱策略找到的所有Outlook语音访问功能，您可以都禁用访问他们的日历和电子邮件。

有关与 UM 邮箱相关的其他管理任务，请参阅[用户的语音邮件](voice-mail-for-users-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只能使用命令行管理程序在 UM 邮箱策略上为启用 UM 的用户修改 Outlook Voice Access 功能，或在单个启用了 UM 的用户的邮箱上修改这些功能。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已启用 UM 的用户。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用命令行管理程序在 UM 邮箱策略上为启用 UM 的用户禁用所选的 Outlook Voice Access 功能

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

此示例将阻止与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的用户在其拨号连接到 Outlook Voice Access 时访问其日历。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

此示例将阻止与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的用户在其拨号连接到 Outlook Voice Access 时访问目录。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

此示例将阻止与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的用户在其拨号连接到 Outlook Voice Access 时访问其电子邮件。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

此示例将阻止与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的用户在其拨号连接到 Outlook Voice Access 时访问个人联系人。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## 使用命令行管理程序在单个启用 UM 的用户的邮箱上禁用所选的 Outlook Voice Access 功能

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

此示例在名为 tony@contoso.com 的 UM 邮箱上禁止在用户拨号连接到 Outlook Voice Access 时访问日历。

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

此示例在名为 tony@contoso.com 的 UM 邮箱上禁止在用户拨号连接到 Outlook Voice Access 时访问电子邮件。

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false

