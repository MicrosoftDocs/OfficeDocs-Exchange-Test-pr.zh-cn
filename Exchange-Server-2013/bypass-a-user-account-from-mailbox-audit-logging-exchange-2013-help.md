---
title: '绕过用户帐户从邮箱审核日志记录: Exchange 2013 Help'
TOCTitle: 绕过用户帐户从邮箱审核日志记录
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 50491108
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 绕过用户帐户从邮箱审核日志记录

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2013-05-21_

当您启用邮箱审核日志邮箱时，记录指定的邮箱访问事件 （例如，访问一个文件夹或邮件，或永久删除邮件）。但是，某些访问权限授予帐户，如由第三方工具或用于合法监视、 帐户的帐户可以创建大量邮箱审核日志条目和可能感兴趣的组织。

您可以配置绕过邮箱审核日志，因此通过该用户帐户或任何邮箱的帐户执行的操作不记录的用户或计算机帐户。通过跳过受信任的用户帐户或计算机帐户需要频繁访问邮箱，您可以减少邮箱审核日志中的干扰。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用邮箱审核日志审核邮箱访问权限和操作，必须定期监视邮箱审核旁路关联。如果邮箱审核避开关联添加一个帐户，该帐户可以访问到它已分配权限，而无需为此类访问或 （如消息删除） 所执行的任何操作生成任何邮箱审核日志条目的组织中的任何邮箱。</td>
</tr>
</tbody>
</table>


关于邮箱审核日志记录的更多管理任务，请参阅[邮箱审核日志记录程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮箱审核日志记录\&quot;条目。

  - 当帐户被配置为绕过邮箱审核日志时，将不会记录对该帐户的任何邮箱的访问。不能配置帐户能够绕过访问特定邮箱的日志记录。

  - 不能使用 Exchange 管理中心 (EAC) 来启用或禁用邮箱审核日志不使用的帐户。您必须使用外壳程序。

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


## 使用命令行管理程序为帐户启用或禁用邮箱审核日志记录绕过

有关如何为一个帐户启用邮箱审核记录的示例，请参阅 [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-cn/library/ff696758\(v=exchg.150\)) 中的 [Examples](https://technet.microsoft.com/zh-cn/ff696758\(exchg.150\)#examples)。

有关如何为一个帐户禁用邮箱审核记录的示例，请参阅 [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-cn/library/ff696758\(v=exchg.150\)) 中的 [Examples](https://technet.microsoft.com/zh-cn/ff696758\(exchg.150\)#examples)。

## 您如何知道这有效？

从邮箱审核记录绕过用户帐户后，可以运行 [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-cn/library/ff696741\(v=exchg.150\)) cmdlet 检查绕过设置。

有关如何检查邮箱审核绕过关联的示例，请参阅 [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-cn/library/ff696741\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-cn/ff696741\(exchg.150\)#examples)。

