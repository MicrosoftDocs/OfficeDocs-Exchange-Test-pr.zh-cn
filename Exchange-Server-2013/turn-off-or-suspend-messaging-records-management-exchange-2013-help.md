---
title: '请关闭或挂起邮件记录管理: Exchange 2013 Help'
TOCTitle: 请关闭或挂起邮件记录管理
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52061514
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 请关闭或挂起邮件记录管理

 

_**适用于：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上一次修改主题：**2013-02-14_

以满足个人、 IT 或业务要求，您可能需要关闭或暂时挂起邮件记录管理 (MRM) 为单个用户或邮箱服务器。您可能需要关闭或挂起 MRM 的原因包括 ︰

  - 如果邮箱用户是在办公室或在其他方面不能访问电子邮件，您可以临时禁用 MRM 为邮箱方法放在保留挂起，请。保留挂起，请打开邮箱时，它将不再由托管文件夹助理处理。当邮箱用户返回或能够再次访问邮箱时，可以从邮箱中删除该保留挂起。

  - 如果您需要测试或解决性能问题，可以清除托管文件夹助理的日程安排，以暂时关闭该服务器上的 MRM。

  - 如果您需要删除邮箱的保留标记（这些邮箱具有应用了该标记的保留策略），可以从策略中删除该标记。

  - 如果您希望保留策略或托管文件夹邮箱策略不再应用于邮箱，可以删除邮箱的策略。

  - 如果您的组织决定不使用 MRM 功能，您可以关闭 MRM 永久的整个组织。如果您以后决定部署 MRM，必须这样做的能力。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您想执行什么操作？

## 将邮箱放在保留挂起中

您可以将邮箱保留挂起状态，要关闭 MRM 暂时 （例如当用户在渡假时）。这挂起的保留策略的邮箱的处理，直到保留挂起，请禁用。这是不同于将邮箱放在原位保存或诉讼封存。

有关如何将邮箱放在保留挂起中的详细信息，请参阅[放置的邮箱上保留挂起](place-a-mailbox-on-retention-hold-exchange-2013-help.md)。

若要了解有关就地保留和诉讼保留的更多信息，请参阅[就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

## 删除邮箱的保留标记

若要从邮箱删除保留标记，取消链接从保留策略的标记。当您取消链接默认文件夹的保留策略标记 （报表） 时，默认邮箱标记应用于该文件夹中的所有项。当您取消个人标记的链接时，就不再对用户可用。标记应用于现有的邮件将继续处理除非从 Exchange 组织中移除该标记。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮件记录管理\&quot;条目。

该命令行管理程序示例将取消保留标记 Delete - 3 Days 与保留策略 Corp-Users 之间的链接。

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

有关语法和参数的详细信息，请参阅 [Get-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd298086\(v=exchg.150\)) 和 [Set-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd335196\(v=exchg.150\))。

## 删除邮箱的保留策略

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;应用保留策略\&quot;条目。

您可以从邮箱用户属性中删除策略，从而阻止保留策略应用于该邮箱。

此命令行管理程序示例将删除邮箱 jpeoples 的保留策略。

    Set-Mailbox jpeoples -RetentionPolicy $null.

此命令行管理程序示例将删除 Exchange 组织中所有邮箱的保留策略。

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

此命令行管理程序示例将把保留策略 Corp-Finance 从所有应用了该策略的邮箱用户中删除。

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

有关语法和参数的详细信息，请参阅[Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))和[Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

## 为整个组织永久性地关闭 MRM

若要关闭组织的 MRM，删除所有保留标记和除 ArbitrationMailbox 策略，就由 Exchange 安装程序创建的保留策略。完成此步骤后，不会强制执行保留策略。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>保留策略还包括移动到归档文件标记，将邮件移动到用户的存档邮箱中。如果您删除已移动到存档标记的保留策略，则必须应用该策略的用户将不再有邮件移动到存档中的托管文件夹助理。<br />
若要避免这种情况，从组织中删除仅删除并允许恢复永久删除标记并使让移动到存档标记应用的策略。另外，拥有的用户和已启用存档无法手动项目移至存档邮箱使用Outlook或Outlook Web App。<br />
删除之前保留标记或保留策略，我们建议您检查要删除的标记设置。不要删除标记移动到归档保留操作。</td>
</tr>
</tbody>
</table>


您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮件记录管理\&quot;条目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在下列命令中加入 <em>WhatIf</em> 开关，以模拟某一命令执行的操作。</td>
</tr>
</tbody>
</table>


此示例从 Exchange 组织中移除了所有的删除标记，Exchange 安装程序创建的 ArbitrationMailbox 策略中使用的\&quot;永不删除\&quot;标记除外。

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

此示例移除了除\&quot;永不删除\&quot;标记以外的所有保留标记。

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

此命令从 Exchange 组织中移除了 Corp-Users 保留策略。

    Remove-RetentionPolicy Corp-Users

有关语法和参数的详细信息，请参阅下列主题：

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd297962\(v=exchg.150\))

