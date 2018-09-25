---
title: '搜索和删除邮件 - 管理员帮助: Exchange Online Help'
TOCTitle: 搜索和删除邮件 - 管理员帮助
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52061370
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 搜索和删除邮件 - 管理员帮助

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-12-20_

管理员可以使用 **Search-Mailbox** cmdlet 来搜索用户邮箱，然后从邮箱中删除邮件。

若要使用一个步骤搜索并删除邮件，请运行带有 *DeleteContent* 开关的 **Search-Mailbox** cmdlet。但是，在执行此操作时，无法预览搜索结果或生成搜索返回的邮件的日志，您可能意外删除不想删除的邮件。若要在删除搜索中找到的邮件之前预览这些邮件的日志，需要运行带有 *LogOnly* 开关的 **Search-Mailbox** cmdlet。

作为额外保护措施，可以使用 *TargetMailbox* 和 *TargetFolder* 参数，首先将邮件复制到另一个邮箱。这样可保留已删除邮件的副本，以防需要再次访问这些邮件。

## 在开始之前，我需要知道什么？

  - 估计完成时间：10 分钟。实际时间可能因邮箱大小和搜索查询而异。

  - 不能使用 Exchange 管理中心 (EAC) 执行这些过程。必须使用命令行管理程序。

  - 您需要分配有以下两个管理角色才能在用户邮箱中搜索和删除邮件：
    
      - **邮箱搜索**   利用此角色，您可以跨组织中的多个邮箱搜索邮件。默认情况下不会向管理员分配此角色。要向自己分配此角色以便搜索邮箱，请将您自己添加为\&quot;发现管理\&quot;角色组的成员。请参阅[在 Exchange 中分配电子数据展示权限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。
    
      - **邮箱导入导出**   此角色允许您从用户邮箱删除邮件。默认情况下，不向任何角色组分配此角色。若要从用户邮箱删除邮件，您可以将\&quot;邮箱导入导出\&quot;角色添加到\&quot;组织管理\&quot;角色组。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)中的\&quot;将角色添加到角色组\&quot;部分。

  - 如果要从中删除邮件的邮箱启用了单个项目恢复，则必须首先禁用该功能。有关详细信息，请参阅[启用或禁用邮箱的单个项目恢复](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md)。

  - 如果要从中删除邮件的邮箱已置于保留状态，建议您在删除保留和删除邮箱内容之前，与记录管理或法律部门进行核实。在获得审批之后，按照主题[清理\&quot;可恢复的项目\&quot;文件夹](clean-up-the-recoverable-items-folder-exchange-2013-help.md)中列出的步骤执行。

  - 使用 **Search-Mailbox** cmdlet，最多可搜索到 10,000 个邮箱。如果你是 Exchange Online 组织，并拥有超过 10,000 个邮箱，则可以使用合规性搜索功能（或相应的 **New-ComplianceSearch** cmdlet）搜索任意数量的邮箱。然后，你可以使用 **New-ComplianceSearchAction** cmdlet 删除由合规性搜索返回的邮件。有关详细信息，请参阅 [从你的 Office 365 组织搜索和删除电子邮件](https://go.microsoft.com/fwlink/p/?linkid=786856)。

  - 如果添加一个搜索查询（通过使用 *SearchQuery* 参数），**Search-Mailbox** cmdlet 最多返回搜索结果中的 10,000 个项目。因此，如果添加一个搜索查询，则可能需要多次运行 **Search-Mailbox** 命令才能将 10,000 多个项目删除。

  - 当您运行**Search-Mailbox** cmdlet 还将搜索用户的存档邮箱。同样，当您使用*DeleteContent*开关使用**Search-Mailbox** cmdlet 主存档邮箱中的项将被删除。为了防止出现这种情况，可以包括*DoNotIncludeArchive*开关。 此外，我们建议您不使用*DeleteContent*开关删除自动扩展启用了存档因为可能发生意外的数据丢失的Exchange Online邮箱中的邮件。

## 搜索邮件并记录搜索结果

本示例在 April Stewart 的邮箱中搜索 Subject 字段中包含\&quot;Your bank statement\&quot;短语的邮件，并将搜索结果记录在管理员邮箱的 SearchAndDeleteLog 文件夹中。不会将邮件复制到目标邮箱或从目标邮箱删除。

```powershell
    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full
```

此示例将搜索组织的所有邮箱，查找文件名中包含\&quot;特洛伊木马\&quot;一词的任何类型的附加文件的邮件，并向管理员的邮箱发送一封日志邮件。

```powershell
    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full
```

有关详细的语法和参数信息，请参阅 [Search-Mailbox](https://technet.microsoft.com/zh-cn/library/dd298173\(v=exchg.150\))。

返回顶部

## 搜索并删除邮件

本示例在 April Stewart 的邮箱中搜索 Subject 字段中包含\&quot;Your bank statement\&quot;短语的邮件，然后从源邮箱中删除这些邮件，而不将搜索结果复制到另一个文件夹。如前所述，您需要分配\&quot;邮箱导入导出\&quot;管理角色才能从用户邮箱删除邮件。

> [!IMPORTANT]  
> 在使用带有 <em>DeleteContent</em> 开关的 <strong>Search-Mailbox</strong> cmdlet 时，会从源邮箱中永久删除邮件。在永久删除邮件之前，建议您在删除搜索中找到的邮件之前使用 <em>LogOnly</em> 开关生成这些邮件的日志，或是在从源邮箱中删除这些邮件之前将其复制到另一个邮箱。


```powershell
Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent
```

本示例在 April Stewart 的邮箱中搜索 Subject 字段中包含\&quot;Your bank statement\&quot;短语的邮件，将搜索结果复制到 BackupMailbox 邮箱中的 AprilStewart-DeletedMessages 文件夹，然后从 April 的邮箱中删除这些邮件。

```powershell
    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent
```

此示例将搜索组织的所有邮箱，查找主题行为\&quot;下载此文件\&quot;邮件，然后将其永久删除。

```powershell
    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent
```

有关详细的语法和参数信息，请参阅 [Search-Mailbox](https://technet.microsoft.com/zh-cn/library/dd298173\(v=exchg.150\))。

返回顶部

## 使用 -LogLevel Full 参数

在上述部分示例中，*LogLevel* 参数和 `Full` 值用于记录由 **Search-Mailbox** cmdlet 返回的结果的详细信息。 包含此参数时，将创建电子邮件并将其发送到 *TargetMailbox* 参数指定的邮箱。日志文件（名为 Search Results.csv 的 CSV 格式文件）附加到此电子邮件，并置于由 *TargetFolder* 参数指定的文件夹中。运行 **Search-Mailbox** cmdlet 时，日志文件包含搜索结果中的每个邮件的行。

