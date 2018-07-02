---
title: '启用或禁用邮箱的邮箱审核日志记录: Exchange 2013 Help'
TOCTitle: 启用或禁用邮箱的邮箱审核日志记录
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 50491492
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 启用或禁用邮箱的邮箱审核日志记录

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-09-30_

使用邮箱审核日志记录，可以跟踪邮箱登录以及用户登录时所执行的操作。 当启用邮箱的邮箱审核日志记录时，将默认记录管理员和代理人执行的某些操作。 将不记录邮箱所有者执行的任何操作。有关邮箱审核日志记录的详细信息，请参阅[邮箱审核日志记录](mailbox-audit-logging-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>邮箱所有者操作的审核可以生成大量邮箱审核日志条目，因此默认情况下是禁用的。 建议您仅启用符合业务和安全要求所需的特定所有者操作的审核。</td>
</tr>
</tbody>
</table>


关于邮箱审核日志记录的更多任务，请参阅[邮箱审核日志记录程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“邮箱审核日志记录”条目。

  - 不能使用 Exchange 管理中心 (EAC) 来启用或禁用邮箱审核日志记录。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用邮箱审核日志记录

可使用命令行管理程序启用或禁用邮箱审核日志记录。 这可启用或禁用为管理员、代理人和邮箱所有者指定的所有操作的日志记录。

本示例启用 Ben Smith 的邮箱的邮箱审核日志记录。

    Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true

本示例禁用 Ben Smith 的邮箱的邮箱审核日志记录。

    Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false

有关详细的语法和参数信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 使用命令行管理程序配置管理员、代理人以及所有者访问的邮箱审核日志记录设置

如果为邮箱启用了邮箱审核日志记录，则只会记录在邮箱的审核日志记录配置中指定的管理员、代理人和所有者操作。

本示例指定将为 Ben Smith 的邮箱记录委派用户对其所执行的 `SendAs` 或 `SendOnBehalf` 操作。

    Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true

本示例指定将为 Ben Smith 的邮箱记录管理员对其所执行的 `MessageBind` 和 `FolderBind` 操作。

    Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true

本示例指定将为 Ben Smith 的邮箱记录邮箱所有者对其所执行的 `HardDelete` 操作。

    Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功启用了邮箱的邮箱审核日志记录并为管理员、代理或所有者访问指定了正确的日志记录设置，可使用 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) cmdlet 来检索该邮箱的邮箱审核日志记录设置。

该示例会检索 Ben Smith 的邮箱设置并传送指定的审核设置（包括审核日志时间限制）到 **Format-List** cmdlet。

    Get-Mailbox "Ben Smith" | Format-List *audit*

