---
title: 'Exchange 审核报告: Exchange 2013 Help'
TOCTitle: Exchange 审核报告
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 50489637
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 审核报告

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

使用审核日志记录可通过跟踪管理员所做的特定更改来解决配置问题，并帮助您满足法规、遵从性以及诉讼等要求。Microsoft Exchange 提供两种类型的审核日志记录：

  - *管理员审核日志记录*会记录管理员执行的所有基于 Exchange 命令行管理程序 cmdlet 的操作。这可以帮助您解决配置问题，或找出与安全或合规性相关的问题的原因。在 Exchange Online 中，由 Microsoft 管理员和委派的管理员执行的操作也会进行记录。

  - *邮箱审核日志*会在管理员、代理用户或拥有该邮箱的人员访问邮箱时进行记录。这有助于确定谁访问了邮箱以及访问者完成了哪些操作。

本主题对以下方面进行了说明：

  - 导出审核日志

  - 运行审核报告

  - 配置审核日志记录
    
      - 启用邮箱审核日志记录
    
      - 授予用户对审核报告的访问权限
    
      - 配置 Outlook Web App 以允许 XML 附件

## 导出审核日志

在 Exchange 管理中心 (EAC) 的“合规性管理”\>“审核”页上，您可搜索并导出管理员审核日志中和邮箱审核日志中的条目。

  - **导出管理员审核日志**   管理员审核日志将记录管理员执行的所有基于命令行管理程序 cmdlet 且不以谓词 **Get**、**Search** 或 **Test** 开头的操作。审核日志条目包括已运行的 cmdlet、与 cmdlet 一起使用的参数和值以及操作是否成功。您可搜索并导出管理员审核日志中的条目。当您导出搜索结果时，Microsoft Exchange 会先将这些结果保存到 XML 文件中，然后再将其附加到电子邮件。有关详细信息，请参阅：
    
      - [搜索角色组更改或管理员审核日志](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [查看并导出外部管理审核日志](https://technet.microsoft.com/zh-cn/library/dn505728\(v=exchg.150\))
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>默认情况下，管理员审核日志条目保留 90 天。当某个条目超过 90 天时，会删除该条目。不能在基于云的组织中更改此设置。但是，可以使用 <strong>Set-AdminAuditLog</strong> cmdlet 在内部部署 Exchange 组织中更改它。</td>
    </tr>
    </tbody>
    </table>


  - **导出邮箱审核日志**   在为某个邮箱启用邮箱审核日志记录之后，Microsoft Exchange 会将非邮箱所有者对邮箱数据所执行的操作记录存储到邮箱审核日志中，此日志位于所审核的邮箱的隐藏文件夹中。还可以将邮箱审核日志配置到日志所有者操作中。此日志中的条目指示谁访问过该邮箱以及访问时间、所执行的操作以及操作是否成功。当搜索邮箱审核日志中的条目并导出它们时，Microsoft Exchange 会先将搜索结果保存到一个 XML 文件中，然后再将其附加到电子邮件。有关详细信息，请参阅[导出邮箱审核日志](export-mailbox-audit-logs-exchange-2013-help.md)。

## 运行审核报告

当您在 EAC 中的“审核”页上运行以下任何报告时，报告的详细信息窗格中将显示结果。

  - **运行非所有者邮箱访问报告**   使用此报告以查找由邮箱所有者之外的其他人访问过的邮箱。有关详细信息，请参阅[运行非所有者邮箱访问报告](run-a-non-owner-mailbox-access-report-exchange-online-help.md)。

  - **运行管理员角色组报告**   使用此报告可搜索对管理员角色组进行的更改。有关详细信息，请参阅[搜索角色组更改或管理员审核日志](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

  - **运行就地发现和保留报告**   使用此报告以查找已从就地保留中保留或删除的邮箱。有关详细信息，请参阅：
    
      - [就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)

  - **运行预邮箱诉讼保留报告**   使用此报告以查找已从诉讼保留中保留或删除的邮箱。有关详细信息，请参阅：
    
      - [运行每个邮箱的诉讼保留报告](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [将邮箱放到诉讼保留中](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **运行管理员审核日志报告**   使用此报告可以查看管理员审核日志中的条目。您可以在 EAC 中运行管理员审核日志报告，而无需将其导出，导出可能需要 24 小时才能通过电子邮件收到。此报告会记录组织内管理员所进行的配置更改。将分多页显示多达 5000 个条目。若要缩小搜索范围，您可以指定日期范围。有关详细信息，请参阅：
    
      - [查看管理员审核日志](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)

  - **运行外部管理员审核日志报告**   此报告仅适用于 Exchange Online 和 Exchange Online Protection。由 Microsoft 管理员或委派的管理员执行的操作记录在管理员审核日志中。使用外部管理员审核日志报告可搜索并查看组织外部的管理员对 Exchange Online 组织的配置执行的操作。有关详细信息，请参阅[查看并导出外部管理审核日志](https://technet.microsoft.com/zh-cn/library/dn505728\(v=exchg.150\))。

## 配置审核日志记录

必须先为您的组织配置审核日志记录，才可运行审核报告并导出审核日志。

## 启用邮箱审核日志记录

对于需要运行非所有者邮箱访问报告的每个邮箱，必须启用邮箱审核日志记录。如果未对邮箱启用邮箱审核日志记录，则当您运行邮箱报告或导出邮箱审核日志时，将不会获得任何结果。

要对单个邮箱启用邮箱审核日志记录，请在命令行管理程序中运行以下命令。

    Set-Mailbox <Identity> -AuditEnabled $true

要对组织中所有用户邮箱启用邮箱审核，请运行以下命令：

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

有关配置记录的操作的详细信息，请参阅：

  - **Exchange 2013**   [启用或禁用邮箱的邮箱审核日志记录](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online**   [在 Office 365 中启用邮箱审核](https://go.microsoft.com/fwlink/p/?linkid=626109)

## 授予用户对审核报告的访问权限

默认情况下，管理员可在 EAC 中的“审核”页上访问并运行任何报告。但是，其他用户（例如，记录经理或法律事务员工）必须分配有必需的权限。

授予用户访问权限最方便的方法是将其添加到“记录管理”角色组。还可通过使用 Shell 将“审核日志”角色分配给用户，以授予其在 EAC 中访问“审核”页的权限。

## 将用户添加到“记录管理”角色组

1.  转到“权限”\>“管理员角色”。

2.  在角色组列表中，单击“记录管理”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“成员”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“选择成员”对话框中选择相应用户。通过键入部分或完整的显示名称，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，可以搜索相应的用户。还可以通过单击“名称”或“显示名”列标题，对列表进行排序。

5.  单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后单击“确定”以返回角色组页。

6.  单击“保存”以保存对角色组的更改。

在“详细信息”窗格中的“成员”下将列出该用户，并且该用户可访问 EAC 中的“审核”页，运行审核报告，还可导出审核日志。

## 将“审核日志”角色分配给用户

运行以下命令，以将“审核日志”角色分配给用户。

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

这样，用户便可选择 EAC 中的“合规性管理”\>“审核”以运行任何报告。用户还可以导出邮箱审核日志，并导出和查看管理员审核日志。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>要让某个用户运行审核报告，但不导出审核日志，则使用前面的命令以分配“仅查看审核日志”角色。</td>
</tr>
</tbody>
</table>


## 配置 Outlook Web App 以允许 XML 附件

当您导出邮箱审核日志或管理员审核日志时，Microsoft Exchange 会将审核日志（即一个 XML 文件）附加到一封电子邮件。然而，Outlook Web App 在默认情况下会阻止 XML 附件。如果要使用 Outlook Web App 访问这些审核日志，则必须将 Outlook Web App 配置为允许 XML 附件。

运行以下命令以在 Outlook Web App 中允许添加 XML 附件。

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

