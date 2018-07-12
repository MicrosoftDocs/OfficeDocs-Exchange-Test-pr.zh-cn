---
title: '创建就地电子数据展示搜索: Exchange 2013 Help'
TOCTitle: 创建就地电子数据展示搜索
ms:assetid: feedc0c9-4a44-4bb2-8520-cc29d66d4fc3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd353189(v=EXCHG.150)
ms:contentKeyID: 50492056
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建就地电子数据展示搜索

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-01-17_

> [!NOTE]  
> 在 Exchange Online（Office 365 和 Exchange Online 独立计划）中新建就地电子数据展示搜索的截止时间为 2017 年 7 月 1 日，我们已推迟了这一最后期限。不过，今年晚些时候或明年初，将无法在 Exchange Online 中新建就地电子数据展示搜索。若要创建电子数据展示搜索，请开始在 Office 365 安全与合规中心使用<a href="https://go.microsoft.com/fwlink/?linkid=847843">内容搜索</a>。在我们取消新建就地电子数据展示搜索后，仍可以修改现有就地电子数据展示搜索，并且在 Exchange Server 2013 和 Exchange 混合部署中新建就地电子数据展示搜索也仍将受支持。


使用 [就地电子数据展示](in-place-ediscovery-exchange-2013-help.md) 搜索所有邮箱内容，包括 [就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md) 上的用户的已删除项目和已修改项目的原始版本。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“就地 eDiscovery”条目。

  - 若要创建电子数据展示搜索，您必须在要创建搜索的组织中拥有 SMTP 地址。因此，在 Exchange Online 中，您必须拥有经过许可的 Exchange Online（计划 2）邮箱才能创建电子数据展示搜索。在 Exchange 混合组织中，您的本地 Exchange 邮箱必须在 Office 365 组织中拥有对应的邮件用户帐户，这样您才能搜索 Exchange Online 邮箱。否则，如果您使用仅存在（计划 2）于 Office 365 中的帐户（如租户管理员帐户）进行登录，则该帐户必须分配有 Exchange Online（计划 2）许可证。

  - Exchange 2013 安装程序将创建名为“发现搜索邮箱”的发现邮箱以复制搜索结果。默认情况下，发现搜索邮箱也在 Exchange Online 中创建。可以创建其他发现邮箱。有关详细信息，请参阅[创建发现邮箱](create-a-discovery-mailbox-exchange-2013-help.md)。

  - 在您创建就地电子数据展示搜索后，搜索结果中返回的邮件不会自动复制到发现邮箱。创建搜索后，您可以使用 Exchange 管理中心 (EAC) 估计、预览搜索结果或将其复制到发现邮箱。有关详细信息，请参阅：
    
      - Estimate or preview search results（本主题中的后面部分）
    
      - [将电子数据展示搜索结果复制到发现邮箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 EAC 创建就地电子数据展示搜索

如前所述，若要创建电子数据展示搜索，您必须登录在您的组织中拥有 SMTP 地址的用户帐户。

1.  转到“合规管理”\>“就地电子数据展示和保留”。

2.  单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“名称和描述”页面的“就地电子数据展示和保留”中，键入搜索的名称，添加可选描述，然后单击“下一步”。

4.  在“邮箱”页上，选择要搜索的邮箱。您可以跨所有邮箱搜索或选择要搜索的特定邮箱。在 Exchange Online 中，您还可以选择 Office 365 组作为搜索的内容源。
    
    > [!IMPORTANT]  
    > 您无法使用“搜索所有邮箱”选项将所有邮箱置于保留状态。要创建“就地保留”，您必须选择“指定要搜索的邮箱”。有关更多详细信息，请参阅<a href="create-or-remove-an-in-place-hold-exchange-2013-help.md">创建或删除就地保留</a>。


5.  在“搜索查询”页上，填写下列字段：
    
      - “包含所有用户邮箱内容”   选择此选项以保留选定邮箱中的所有内容。如果您选择此选项，则无法指定其他搜索条件。
    
      - “基于条件筛选”   选择此选项以指定搜索条件，包括关键词、开始和结束日期、发件人和收件人地址以及邮件类型。
        
        ![配置电子数据展示搜索查询](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "配置电子数据展示搜索查询")  
    
    > [!NOTE]  
    > 由运行搜索时创建的搜索查询中的“<strong>OR</strong>”运算符连接“<strong>发件人:</strong>”和“<strong>收件人/抄送/密件抄送:</strong>”字段。这意味着，由任何指定用户发送或接收的邮件（并且匹配其他搜索条件）都包含在此搜索结果中。
    > 日期由 <strong>AND</strong> 运算符连接。


6.  在“就地保留设置”页面上，您可以选中“将与所选邮箱中的搜索查询匹配的内容置于保留状态”复选框，然后选择以下选项之一将项目置于就地保留状态：
    
      - “无限期保留”   选择该选项以无限期保留返回的项目。保留的项目将会保持，直到您从搜索中删除邮箱或删除搜索。
    
      - “指定保留项目的天数（相对于收到日期）” 使用此选项以在指定周期内保留项目。例如，如果您的组织需要将所有邮件至少保留七年，可使用此选项。可使用“基于时间”的就地保留以及保持政策，确保在七年后删除项目。
        
        > [!IMPORTANT]  
        > 当出于法律目的“就地保留”邮箱或项目时，通常建议无限期保持项目，并在完成案件或调查后删除保留。


7.  单击“完成”保存搜索，并返回根据您指定的条件进行搜索后返回的项目的估计总大小和总数。估计显示在详细信息窗格。单击“刷新”![刷新图标](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "刷新图标")，更新详细信息窗格中显示的信息。

返回顶部

## 使用命令行管理程序创建就地电子数据展示搜索

本示例将为包含关键词 Contoso 和 ProjectA 的项目创建名为 Discovery-CaseId012 的就地电子数据展示搜索，同时还满足以下条件：

  - 开始日期：1/1/2009

  - 结束日期：12/31/2011

  - 源邮箱：DG 财务

  - 目标邮箱：发现搜索邮箱

  - 邮件类型：Email

  - 在搜索统计信息中包含不可搜索的项目

  - 日志级别：完整

> [!IMPORTANT]  
> 如果您在运行就地电子数据展示搜索时未指定额外搜索参数，结果将返回指定源邮箱中的所有项目。如果您未指定要搜索的邮箱，则会搜索 Exchange 或 Exchange Online 组织中的所有邮箱。


    New-MailboxSearch "Discovery-CaseId012" -StartDate "01/01/2009" -EndDate "12/31/2011" -SourceMailboxes "DG-Finance" -TargetMailbox "Discovery Search Mailbox" -SearchQuery '"Contoso" AND "Project A"' -MessageTypes Email -IncludeUnsearchableItems -LogLevel Full

> [!NOTE]  
> 使用 <em>StartDate</em> 和 <em>EndDate</em> 参数时，您必须使用日期格式“mm/dd/yyyy”，即使您的本地计算机设置配置为使用其他日期格式（如“dd/mm/yyyy”），也是如此。例如，若要搜索从 2013 年 4 月 1 日到 2013 年 7 月 1 日发送的邮件，则分别使用 <strong>04/01/2013</strong> 和 <strong>07/01/2013</strong> 作为开始日期和结束日期。


本示例创建名为 HRCase090116 的就地电子数据展示搜索，这会搜索由 Alex Darrow 于 2015 年发送给 Sara Davis 的电子邮件。

    New-MailboxSearch "HRCase090116" -StartDate "01/01/2015" -EndDate "12/31/2015" -SourceMailboxes  alexd,sarad -SearchQuery 'From:alexd@contoso.com AND To:sarad@contoso.com' -MessageTypes Email -TargetMailbox "Discovery Search Mailbox" -IncludeUnsearchableItems -LogLevel Full

使用命令行管理程序创建就地电子数据展示搜索后，您必须使用 **Start-MailboxSearch** cmdlet 启动搜索，以将邮件复制到 *TargetMailbox* 参数中指定的发现邮箱。有关详细信息，请参阅[将电子数据展示搜索结果复制到发现邮箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [New-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd298064\(v=exchg.150\))。

返回顶部

## 使用 EAC 估计或预览搜索结果

创建就地电子数据展示搜索后，您可以使用 EAC 估计和预览搜索结果。如果您使用 **New-MailboxSearch** cmdlet 创建新的搜索，则可以使用命令行管理程序启动搜索，以估计搜索结果。您无法使用命令行管理程序预览搜索结果中返回的邮件。

1.  导航到“合规管理”\>“就地 eDiscovery 与保留”。

2.  在列表视图中，选择就地电子数据展示搜索，然后执行以下操作之一：
    
      - 单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")\>“估计搜索结果”可返回估计的项目总大小和数量，此结果由搜索根据您指定的条件返回。选择此选项可重启搜索并估计搜索结果。
        
        估计的搜索结果显示在详细信息窗格中。单击“刷新”![刷新图标](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "刷新图标")，更新详细信息窗格中显示的信息。
    
      - 单击详细信息窗格中的“预览搜索结果”可以预览完成搜索估计后的结果。选择此选项以打开“电子数据展示搜索预览”窗口。从搜索的邮箱返回的所有邮件都会显示。
        
        > [!NOTE]  
        > 搜索的邮箱列于“电子数据展示搜索预览”窗口的右窗格中。对于每个邮箱，系统还会显示所返回的项目数量以及这些项目的总大小。搜索返回的所有项目列于右窗格中，可以按最近或最远日期进行排序。无法通过单击左窗格中的邮箱在右窗格中显示每个邮箱中的项目。若要查看从特定邮箱返回的项目，您可以复制搜索结果并在发现邮箱中查看项目。
    
    ![估计或预览搜索结果](images/Dd353189.57e0fc2d-71bf-42aa-aa4b-4a77148f2b43(EXCHG.150).gif "估计或预览搜索结果")  

返回顶部

## 使用命令行管理程序估计搜索结果

您可以使用 *EstimateOnly* 开关只返回估计的搜索结果，而不将结果复制到发现邮箱。必须使用 **Start-MailboxSearch** cmdlet 启动仅估计搜索。然后，您可以使用 **Get-MailboxSearch** cmdlet 检索估计的搜索结果。

例如，运行以下命令创建新的电子数据展示搜索，然后显示估计的搜索结果：
```
    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeKeywordStatistics
```
```
    Start-MailboxSearch "FY13 Q2 Financial Results"
```
```
    Get-MailboxSearch "FY13 Q2 Financial Results"
```

若要显示上一示例中估计的搜索结果的特定信息，您可以运行以下命令：

    Get-MailboxSearch "FY13 Q2 Financial Results" | FL Name,Status,LastRunBy,LastStartTime,LastEndTime,Sources,SearchQuery,ResultSizeEstimate,ResultNumberEstimate,Errors,KeywordHits

返回顶部

## 有关电子数据展示搜索的详细信息

  - 创建新的电子数据展示搜索后，您可以将搜索结果复制到发现邮箱，并将这些搜索结果导出到 PST 文件中。有关详细信息，请参阅：
    
      - [将电子数据展示搜索结果复制到发现邮箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)
    
      - [将电子数据展示搜索结果导出到 PST 文件](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - 运行电子数据展示搜索估计值（搜索条件中包括关键字）后，单击选定搜索窗格中“查看关键字统计信息”可以查看关键字统计信息。这些统计信息显示有关搜索查询中使用的每个关键字返回的项目数的详细信息。但是，如果搜索中包括 100 个以上的源邮箱，则在试图查看关键字统计信息时会返回一个错误。若要查看关键字统计信息，搜索中包含的源邮箱不可以超过 100 个。

  - 如果使用 Exchange Online 中的 **Get-MailboxSearch** 检索有关电子数据展示搜索的信息，您必须指定搜索名称，以返回搜索属性的完整列表，例如，`Get-MailboxSearch "Contoso Legal Case"`。如果您在不使用任何参数的情况下运行 **Get-MailboxSearch** cmdlet，则不会返回以下属性：
    
      - SourceMailboxes
    
      - Sources
    
      - SearchQuery
    
      - ResultsLink
    
      - PreviewResultsLink
    
      - Errors
    
    原因是需要通过很多资源为组织中的所有电子数据展示搜索返回这些属性。

返回顶部

