---
title: '减小 Exchange 中发现邮箱的大小: Exchange 2013 Help'
TOCTitle: 减小 Exchange 中发现邮箱的大小
ms:assetid: fa762d14-f942-4728-8813-887d11441a68
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn750895(v=EXCHG.150)
ms:contentKeyID: 62371347
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 减小 Exchange 中发现邮箱的大小

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

有超过 50 GB 限制的发现邮箱吗？您可以通过创建新的发现邮箱，将搜索结果从大的发现邮箱复制到新的邮箱来修复此问题。

## 为何需要执行此操作？

在 Exchange Server 2013 和 Exchange Online 中，用于存储就地电子数据展示搜索结果的发现邮箱最大大小为 50 GB。在达到当前大小限制之前，您可以将存储配额增加到超过 50 GB，这会导致发现邮箱大大超过 50 GB。超过 50 GB 的发现邮箱存在三个问题：

  - 不受支持。

  - 无法迁移到 Office 365。

  - 如果它们是 Exchange Server 2010 中的发现邮箱，则不能升级到 Exchange Server 2013。

## 过程概览

下面快速介绍一下减小超过 50 GB 限制的发现邮箱大小时需执行的操作。

1.  步骤 1：创建发现邮箱要将搜索结果分发到的其他发现邮箱。

2.  将搜索结果从现有发现邮箱步骤 2：将搜索结果复制到发现邮箱到一个或多个新的发现邮箱。

3.  从原始发现邮箱中步骤 3：删除电子数据展示搜索电子数据展示搜索以减小大小。

此处显示的策略会根据日期范围，将原始发现邮箱中的搜索结果分组到单独的电子数据展示搜索。这是将多个搜索结果复制到新发现邮箱的快速方法。下图阐释了此方法。

![减小发现邮箱的大小](images/Dn750895.4400df18-c7ed-4c62-b304-f9060ffbdba5(EXCHG.150).gif "减小发现邮箱的大小")

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：时间将依据要复制到不同发现邮箱的搜索结果的数量和大小发生变化。

  - 运行以下命令，以确定您的组织中发现邮箱的大小。
    
        Get-Mailbox -RecipientTypeDetails DiscoveryMailbox | Get-MailboxStatistics | FL DisplayName,TotalItemSize

  - 确定您是否需要保留超过 50 GB 限制的发现邮箱中的部分或全部搜索结果。按照本主题中的步骤，将其复制到其他发现邮箱中以保留搜索结果。如果您不需要保留特定电子数据展示搜索的结果，您可以删除搜索，如步骤 3 中所述。删除搜索将删除发现邮箱中的搜索结果。

  - 如果您不需要超过 50 GB 限制的发现邮箱中的任何搜索结果，可以将其删除。如果这是设置 Exchange 组织时创建的默认发现邮箱，您可以重新创建它。有关详细信息，请参阅[在 Exchange 中删除和重新创建默认发现邮箱](delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md)。

  - 对于当前法律案件，您可能需要将所选电子数据展示搜索的结果导出到 .pst 文件。执行此操作可完整保留特定搜索的结果。除包含搜索结果的 .pst 文件外，还将导出包含搜索结果中返回的每个邮件条目的搜索结果日志（.csv 文件格式）。该文件中的每个条目标识邮件所在的源邮箱。有关详细信息，请参阅[将电子数据展示搜索结果导出到 PST 文件](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)。
    
    将搜索结果导出到 .pst 文件之后，如果您想从新的发现邮箱进行导入，您将需要使用 Outlook。

## 步骤 1：创建发现邮箱

第一步是创建附加发现邮箱，以便可以从超过大小限制的发现邮箱复制搜索结果。根据发现邮箱的 50 GB 大小限制，确定需要多少附加发现邮箱并进行创建。然后您将需要向用户或组分配打开这些新发现邮箱的必需权限。

1.  运行以下命令以创建一个新的发现邮箱。
    
        New-Mailbox -Name <discovery mailbox name> -Discovery

2.  若要为用户或群组分配打开发现邮箱和查看搜索结果所需的权限，请运行以下命令。
    
        Add-MailboxPermission <discovery mailbox name> -User <name of user or group> -AccessRights FullAccess -InheritanceType all

## 步骤 2：将搜索结果复制到发现邮箱

下一步是使用 **New-MailboxSearch** cmdlet 将搜索结果从现有发现邮箱复制到在上一步中创建的新发现邮箱。此过程使用 *StartDate* 和 *EndDate* 参数将搜索结果分组到不超过 50 GB 的批次。这可能需要进行一些测试（通过评估搜索结果），适当调整搜索结果的大小。

1.  运行以下命令以创建一个新的电子数据展示搜索。
    
        New-MailboxSearch -Name "Search results from 2010" -SourceMailboxes "Discovery Search Mailbox" -StartDate "01/01/2010" -EndDate "12/31/2010" -TargetMailbox "Discovery Mailbox Backup 01" -EstimateOnly -StatusMailRecipients admin@contoso.com
    
    此示例使用以下参数：
    
      - *Name*   此参数指定新电子数据展示搜索的名称。因为搜索的范围由发送日期和接收日期确定，因此在搜索名称中包括日期范围非常有用。
    
      - *SourceMailboxes*   此参数指定默认发现邮箱。您还可以指定已超出大小限制的另一个发现邮箱的名称。
    
      - *StartDate* 和 *EndDate*   这些参数指定默认发现邮箱中搜索结果的日期范围以包括在搜索结果中。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>对于日期，使用短日期格式 mm/dd/yyyy，即使本地计算机的“区域选项”设置以不同格式配置（如 dd/mm/yyyy）也是如此。例如，使用 <strong>03/01/2014</strong> 可指定 2014 年 3 月 1 日。</td>
        </tr>
        </tbody>
        </table>
    
      - *TargetMailbox*   此参数指定应该将搜索结果复制到名为“Discovery Mailbox Backup 01”的发现邮箱中。
    
      - *EstimateOnly*   此开关指定仅提供搜索开始时将返回的项目的估计数量。如果不包括此开关，邮件将在搜索开始时复制到目标邮箱中。通过使用此开关，可以根据需要调整日期范围，以增加或减少搜索结果的数量。
    
      - *StatusMailRecipients*   此参数指定应发送给指定收件人的状态邮件。

2.  创建搜索后，请使用命令行管理程序或 Exchange 管理员中心 (EAC) 将其启动。
    
      - **使用命令行管理程序：** 运行以下命令，启动在上一步中创建的搜索。因为创建搜索时包括 *EstimateOnly* 开关，搜索结果不会复制到目标发现邮箱。
        
            Start-MailboxSearch "Search results from 2010"
    
      - **使用 EAC：** 转到“合规性管理”\>“就地电子数据展示与保留”。选择在上一步中创建的搜索，单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，然后单击“估计搜索结果”。

3.  如有必要，调整日期范围来增加或减少返回的搜索结果的数量。如果您更改日期范围，请再次运行搜索以获得结果的新估计值。考虑更改搜索名称以反映新的日期范围。

4.  当您测试完搜索之后，使用命令行管理程序或 EAC 将搜索结果复制到目标发现邮箱。
    
      - **使用命令行管理程序：** 运行以下命令以复制搜索结果。您必须删除 *EstimateOnly* 开关，然后才能复制搜索结果。
        
            Set-MailboxSearch "Search results from 2010" -EstimateOnly $false
        
            Start-MailboxSearch "Search results from 2010"
    
      - **使用 EAC：** 转到“合规性管理”\>“就地电子数据展示与保留”。选择搜索，单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，然后单击“复制搜索结果”。
    
    有关详细信息，请参阅[将电子数据展示搜索结果复制到发现邮箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)。

5.  重复步骤 1 到 4，为其他日期范围创建新的搜索。在新搜索的名称中包括日期范围来指示结果范围。要确保没有发现邮箱超过 50 GB 限制，请将其他发现邮箱作为目标邮箱。

## 步骤 3：删除电子数据展示搜索

将搜索结果从原始发现邮箱复制到其他发现邮箱后，您可以删除原始电子数据展示搜索。删除电子数据展示搜索将从存储这些搜索结果的发现邮箱中删除搜索结果。

在删除搜索之前，您可以运行以下命令，识别已为组织中所有搜索复制到发现邮箱的搜索结果的大小。

    Get-MailboxSearch | FL Name,TargetMailbox,ResultSizeCopied

您可以使用命令行管理程序或 EAC 删除电子数据展示搜索。

  - **使用命令行管理程序：** 运行以下命令。
    
        Remove-MailboxSearch -Identity <name of search>

  - **使用 EAC：** 转到“合规性管理”\>“就地电子数据展示与保留”。选择要删除的搜索，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 您如何知道这有效？

删除电子数据展示搜索以从其存储所在的发现邮箱中删除结果后，运行以下命令显示所选发现邮箱的大小。

    Get-Mailbox <name of discovery mailbox> | Get-MailboxStatistics | FL TotalItemSize

