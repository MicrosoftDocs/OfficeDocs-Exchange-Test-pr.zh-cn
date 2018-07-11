---
title: '放置的邮箱上保留挂起: Exchange Online Help'
TOCTitle: 放置的邮箱上保留挂起
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 50490247
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 放置的邮箱上保留挂起

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-14_

将邮箱放在保留挂起，请暂停处理保留策略或邮箱托管的文件夹邮箱策略。如用户暂时被休假或走的情况下旨在保留挂起。

在保留挂起期间用户可以登录到其邮箱，更改或删除的项。执行邮箱搜索时，删除超过已删除的项目的保留期的项目不是搜索结果中返回。若要确保用户通过更改或删除的项都保留在法律封存方案，必须将法律封存在邮箱中。有关详细信息，请参阅[创建或删除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

您还可以包括暂保留邮箱的保留意见。受支持版本的 Microsoft Outlook中显示批注。

有关与邮件记录管理 (IRM) 相关的其他管理任务，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮件记录管理\&quot;条目。

  - 不能使用 Exchange 管理中心 (EAC) 放置保留挂起状态的邮箱。您必须使用外壳程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序将邮箱放在保留挂起中

本示例将 Michael Allen 的邮箱放在保留挂起中。

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 使用命令行管理程序删除邮箱的保留挂起

本示例从 Michael Allen 的邮箱中删除保留挂起。

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功将邮箱放在保留挂起中，请使用 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) cmdlet 检索邮箱的 *RetentionHoldEnabled* 属性。

此命令检索 Michael Allen 的邮箱的 *RetentionHoldEnabled* 属性。

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

此命令检索 Exchange 组织中的所有邮箱，对放在保留挂起中的邮箱进行筛选，并将这些邮箱与应用于它们的保留策略一起列出。

> [!IMPORTANT]  
> 因为<em>RetentionHoldEnabled</em>不是Exchange 2013中的筛选属性，不能用来放置保留挂起，请在服务器端的筛选器邮箱<strong>Get-Mailbox</strong> cmdlet 使用<em>Filter</em>参数。此命令会检索所有邮箱和运行 Shell 会话的客户端上的筛选器的列表。在数千个邮箱的大环境中，此命令可能需要很长时间才能完成。


    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

