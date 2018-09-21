---
title: '将电子数据展示搜索结果复制到发现邮箱: Exchange 2013 Help'
TOCTitle: 将电子数据展示搜索结果复制到发现邮箱
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183396
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将电子数据展示搜索结果复制到发现邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-24_

创建就地电子数据展示搜索之后，您可以使用 EAC 将结果复制到发现邮箱。您还可以使用 Shell 启动使用 **New-MailboxSearch** cmdlet 创建的电子数据展示搜索，以便将结果复制到您在创建该搜索时所指定的发现邮箱。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟或更久一些，这取决于搜索结果中返回的邮箱项的数量

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“就地电子数据展示”条目。

  - 必须先使用 EAC 或 Shell 创建电子数据展示搜索，然后才能复制搜索结果。有关详细信息，请参阅[创建就地电子数据展示搜索](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/create-in-place-ediscovery-search)。

  - Exchange 2013 安装程序将创建名为“发现搜索邮箱”的发现邮箱以复制搜索结果。默认情况下，发现搜索邮箱也在 Exchange Online 中创建。可以创建其他发现邮箱。有关详细信息，请参阅[创建发现邮箱](create-a-discovery-mailbox-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 要执行什么操作？

## 使用 EAC 复制搜索结果

1.  在 EAC 中，转到“合规性管理”\>“就地电子数据展示和保留”。

2.  在列表视图中，选择电子数据展示搜索。

3.  单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，然后从下拉列表中单击“复制搜索结果”。

4.  在“复制搜索结果”中，从以下选项中进行选择：
    
      - **包含不可搜索的项目**   选中此复选框以包括无法搜索的邮箱项目（例如，带无法被 Exchange 搜索索引的文件类型附件的邮件）。有关详细信息，请参阅 [Exchange 电子数据展示中不可搜索的项目](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。
    
      - **启用重复数据删除**   选中此复选框以排除重复的邮件。仅有邮件的单个实例将被复制到发现邮箱。
    
      - **启用完全日志记录**   选中此复选框以在搜索结果中包含完整日志。
    
      - **复制完成后发送邮件给我**   选中此复选框以在搜索完成后收到电子邮件通知。
    
      - **将结果复制到此发现邮箱**   单击“浏览”以选择要复制搜索结果到其中的发现邮箱。
        
        ![复制搜索结果](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "复制搜索结果")  

5.  单击“复制”开始将搜索结果复制到指定发现邮箱的过程。

6.  单击“刷新”![刷新图标](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "刷新图标")更新有关显示在详细信息窗格中的复制状态的信息。

7.  复制完成后，单击“打开”打开发现邮箱查看搜索结果。

## 使用 Shell 复制搜索结果

使用 **New-MailboxSearch** cmdlet 创建就地电子数据展示搜索之后，您必须启动该搜索将邮件复制到您在 *TargetMailbox* 参数中指定的发现邮箱。有关使用 Shell 创建电子数据展示搜索的信息，请参阅：

  - [Use the Shell to create an In-Place eDiscovery search](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/create-in-place-ediscovery-search)

  - [New-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd298064\(v=exchg.150\))

例如，您可以运行以下命令来启动一个名为 *Fabrikam Investigation* 的电子数据展示搜索将搜索结果复制到指定的发现邮箱中。

```powershell
Start-MailboxSearch "Fabrikam Investigation"
```

如果您使用 *EstimateOnly* 开关获得估计的搜索结果，就必须先删除此开关，然后才可以复制搜索结果。您还必须指定向其复制搜索结果的发现邮箱。例如，如果您通过使用以下命令创建仅执行估计的搜索：

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

若要将此搜索的结果复制到发现邮箱，需要运行以下命令：
  ```
  Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"
  ```
  ```
  Start-MailboxSearch "FY13 Q2 Financial Results"
  ```

## 有关复制搜索结果的详细信息

  - 将搜索结果复制到发现邮箱后，您可以将那些搜索结果导出到 PST 文件。有关详细信息，请参阅[将电子数据展示搜索结果导出到 PST 文件](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)。

  - 有关不可搜索的项目的详细信息，请参阅 [Exchange 电子数据展示中不可搜索的项目](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。

  - 如果您复制特定日期范围内的所有邮箱内容（但未在搜索条件中指定任何关键字），则该日期范围内的所有不可搜索项目都将自动包含在搜索结果中。因此，当复制搜索结果时，请不要选中“包括不可搜索的项目”复选框。否则，所有不可搜索的项目的重复副本将被复制到发现邮箱。

  - 除了可将搜索结果复制到发现邮箱，您还可以估计或预览选定搜索的搜索结果。
    
      - **估计搜索结果**   此选项将返回预计的项目总大小和数量，搜索将基于您指定的条件返回。估计结果显示在 EAC 中的详细信息窗格中。
    
      - **预览搜索结果**   此选项可让您预览由搜索返回的搜索结果，而无需将其复制到发现邮箱进行查看。这使您可以快速确定搜索结果是否相关。在预览结果之后，您可以修改搜索查询以缩小搜索结果范围并重新运行搜索。预览页面中的项目是只读版本的实际搜索结果，因此您不能在预览页面上进行移动、编辑、删除或转发。
    
    有关详细信息，请参阅[Estimate or preview search results](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/create-in-place-ediscovery-search)。

