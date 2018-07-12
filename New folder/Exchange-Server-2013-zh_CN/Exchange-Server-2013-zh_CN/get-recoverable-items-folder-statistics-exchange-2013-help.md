---
title: '获取&quot;可恢复的邮件&quot;文件夹统计信息: Exchange 2013 Help'
TOCTitle: 获取“可恢复的邮件”文件夹统计信息
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52061557
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 获取\&quot;可恢复的邮件\&quot;文件夹统计信息

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-01-22_

\&quot;可恢复的邮件\&quot;文件夹包含 Microsoft Outlook 和 Microsoft OfficeOutlook Web App 用户或邮箱助理删除的邮件。已删除邮件保留在此文件夹中的持续时间取决于您为邮箱数据库或邮箱配置的已删除邮件保留时间设置。邮箱数据库默认配置为保留已删除邮件 14 天，\&quot;可恢复的邮件\&quot;警告配额和\&quot;可恢复的邮件\&quot;配额分别默认设置为 20 GB 和 30 GB。不过，如果您已为邮箱启用\&quot;就地保留\&quot;或\&quot;诉讼保留\&quot;，\&quot;可恢复的邮件\&quot;文件夹可以累积超过指定保留期的已删除邮件，还可以维护不同版本的已修改邮箱邮件。

当\&quot;可恢复的邮件\&quot;文件夹达到\&quot;可恢复的邮件\&quot;警告配额时，应用程序事件日志中会记录一个警告事件。如果邮箱未处于诉讼保留状态，则邮件删除原则为先进先出 (FIFO)。但如果邮箱处于诉讼保留状态，则邮箱永远不会清空；但当邮箱达到\&quot;可恢复的邮件\&quot;配额时，邮箱功能会受到影响。

因此，请务必监视事件日志中是否有当邮箱达到\&quot;可恢复的邮件\&quot;配额时生成的警报。您还可以通过此过程报告\&quot;可恢复的邮件\&quot;文件夹统计信息（尤其是处于诉讼保留状态的邮箱）。

有关详细信息，请参阅下列主题：

  - [\&quot;可恢复的项目\&quot;文件夹](recoverable-items-folder-exchange-2013-help.md)

  - [就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱文件夹\&quot;条目。

  - 无法使用 Exchange 管理中心 (EAC) 获取邮箱的\&quot;可恢复的邮件\&quot;文件夹统计信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 要执行什么操作？

## 获取邮箱的\&quot;可恢复的邮件\&quot;文件夹统计信息

本示例获取 Soumya Singhi 的\&quot;可恢复的邮件\&quot;文件夹统计信息，并以列表格式显示输出结果。

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List

本示例获取 Soumya Singhi 的\&quot;可恢复的邮件\&quot;文件夹统计信息，并以表格格式显示文件夹名称、文件夹路径、文件夹中的邮件数以及文件夹大小。

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize

有关语法和参数的详细信息，请参阅 [Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa996762\(v=exchg.150\))。

## 获取处于诉讼保留状态的所有邮箱的\&quot;可恢复的邮件\&quot;文件夹统计信息

本示例获取所有处于诉讼保留状态的邮箱的列表，以及每个邮箱的\&quot;可恢复的邮件\&quot;文件夹及其子文件夹的邮箱文件夹统计信息。**Identity**（邮箱文件夹标识）以及 **FolderAndSubfolderSize** 属性以表格格式显示。

    Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa996762\(v=exchg.150\))。

## 获取邮箱的可恢复邮件配额

本示例显示用户邮箱的\&quot;可恢复的项目\&quot;文件夹的配额和警告配额。该示例还检索有关将邮箱置于诉讼保留还是就地保留状态的信息。

    Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

本示例显示组织中所有用户邮箱的\&quot;可恢复的项目\&quot;文件夹的配额和警告配额。本示例还检索保留信息。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

