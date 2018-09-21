---
title: '清理“可恢复的项目”文件夹: Exchange 2013 Help'
TOCTitle: 清理“可恢复的项目”文件夹
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50556607
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- 分类外泄
- 分类外泄清理
- 分类邮件外泄
- 分类邮件外泄清理
- 搜索和销毁
- 邮件外泄
- 邮件外泄清理
ms.translationtype: HT
---

# 清理“可恢复的项目”文件夹

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-09-30_

“可恢复的项目”文件夹（在早期版本的 Exchange 中称为*垃圾站*）的存在是为了防止出现意外或恶意删除，并帮助进行常在诉讼或调查之前或期间进行的发现工作。若要了解有关“可恢复的项目”文件夹的详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。

清理邮箱的“可恢复的项目”文件夹的方式取决于邮箱是否处于就地保留或诉讼保留或者启用了单个项目恢复：

  - 如果邮箱未处于就地保留或诉讼保留，或者未启用单个项目恢复，则只能从“可恢复的项目”文件夹中删除项目。在删除后，不能使用单个项目恢复来恢复项目。

  - 如果邮箱处于就地保留或诉讼保留，或者启用了单个项目恢复，则在删除保留或禁用单个项目恢复之前，一直保留邮箱数据将十分重要。在这种情况下，需要执行更多详细步骤来清理“可恢复的项目”文件夹。

若要了解有关就地保留和诉讼保留的更多信息，请参阅[就地保留和诉讼保留](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-and-litigation-holds)。若要了解有关单个项目恢复的详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)中的“单个项目恢复”。

有关“可恢复的项目”文件夹的详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该过程的时间：30 分钟。这可能会因为“可恢复的项目”文件夹的大小不同而有差异

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“删除邮箱内容”条目。

  - 因为错误地清理“可恢复的项目”文件夹可能会导致数据丢失，所以熟悉“可恢复的项目”文件夹以及删除其内容所产生的影响将十分重要。在执行此过程之前，建议您查看[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)中的信息。

  - 不能使用 Exchange 管理中心 (EAC) 执行这些过程。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 使用命令行管理程序从未处于保留或未启用单个项目恢复的邮箱的“可恢复的项目”文件夹中删除项目

此示例从 Gurinder Singh 的“可恢复的项目”文件夹中永久删除项目，还将这些项目复制到发现搜索邮箱（由 Exchange 安装程序创建的发现邮箱）中的 GurinderSingh-RecoverableItems 文件夹。

    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent

> [!NOTE]  
> 若要删除邮箱中的项目而不将这些项目复制到另一个邮箱，请在不带 <em>TargetMailbox</em> 和 <em>TargetFolder</em> 参数的情况下使用上面的命令。


有关详细的语法和参数信息，请参阅 [Search-Mailbox](https://technet.microsoft.com/zh-cn/library/dd298173\(v=exchg.150\))。

## 使用命令行管理程序清理处于保留或启用了单个项目恢复的邮箱的“可恢复的项目”文件夹

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“删除邮箱内容”条目。

如果邮箱达到其可恢复的项目配额，则建议您提高配额而不是删除文件夹中的项目。还可以监视与可恢复的项目警告配额相关的应用程序日志中的事件，并执行必要的操作（如提高配额或调查达到警告配额的邮箱的“可恢复的项目”文件夹增长）。

如果存储约束或类似问题阻碍您提高可恢复的项目配额，并且您需要从处于就地保留或诉讼保留或者启用了单个项目恢复的邮箱的“可恢复的项目”文件夹中删除邮件，则建议您首先将数据从用户的“可恢复的项目”文件夹复制到另一个邮箱。如果您由于某个卷上的存储约束而删除项目，则可以将项目复制到位于具有足够存储的卷上的邮箱。

此过程将项目从 Gurinder Singh 的“可恢复的项目”文件夹复制到发现搜索邮箱中的 GurinderSingh-RecoverableItems 文件夹。在从“可恢复的项目”文件夹复制和删除项目之前，必须首先执行几个步骤，以确保不会从“可恢复的项目”文件夹中删除项目。在将项目复制到发现或备份邮箱并清理该文件夹后，可以恢复为邮箱以前的设置。

1.  检索以下配额设置。请务必记下这些值，以便可以在清理“可恢复的项目”文件夹之后恢复这些设置：
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    > [!NOTE]  
    > 如果 <em>UseDatabaseQuotaDefaults</em> 参数设置为 <code>$true</code>，则不会应用以前的配额设置。会应用在邮箱数据库上配置的对应配额设置，即使填充了单个邮箱设置也是如此。
    
        Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults

2.  检索邮箱的邮箱访问设置。请务必记下这些设置以供将来使用。
    
        Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled

3.  检索“可恢复的项目”文件夹的当前大小。记下该大小，以便可以在步骤 6 中提高配额。
    
        Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize

4.  检索当前托管文件夹助理工作周期配置。请务必记下这些设置以供将来使用。
    
    ```powershell
Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle
```

5.  禁用对邮箱的客户端访问，以确保在此过程期间无法对邮箱数据进行更改。
    
        Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false

6.  若要确保不会从“可恢复的项目”文件夹中删除任何项目，请提高可恢复的项目配额、提高可恢复的项目警告配额，并将已删除项目保留期设置为大于用户的“可恢复的项目”文件夹当前大小的值。这对于为处于就地保留或诉讼保留的邮箱保留邮件尤其重要。建议将这些设置提高为其当前大小的两倍。
    
        Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false

7.  在邮箱服务器上禁用托管文件夹助理。
    
    ```powershell
Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
```
    
    > [!IMPORTANT]  
    > 如果邮箱位于数据库可用性组 (DAG) 中的某个邮箱数据库上，则必须在托管数据库副本的每个 DAG 成员上禁用托管文件夹助理。如果该数据库故障转移到另一个服务器，则这可防止该服务器上的托管文件夹助理删除邮箱数据。


8.  禁用单个项目恢复并从诉讼保留中删除邮箱。
    
    ```powershell
Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
```
    
    > [!IMPORTANT]  
    > 在运行此命令后，可能需要一小时来禁用单个项目恢复或诉讼保留。建议您仅当此期间过后才执行下一个步骤。


9.  将项目从“可恢复的项目”文件夹复制到发现搜索邮箱中的某个文件夹，并删除源邮箱中的内容。
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    如果您只需要删除匹配指定条件的邮件，请使用 *SearchQuery* 参数指定条件。此示例删除在“Subject”字段中具有字符串“Your bank statement”的邮件。
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    > [!NOTE]  
    > 不是一定要将项目复制到发现搜索邮箱。可以将邮件复制到任何邮箱。但是，为了防止访问可能敏感的邮箱数据，建议将邮件复制到仅限经过授权的记录管理员访问的邮箱。默认情况下，仅限发现管理角色组的成员访问默认发现搜索邮箱。有关详细信息，请参阅<a href="https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">就地电子数据展示</a>。


10. 如果邮箱以前处于诉讼保留或启用了单个项目恢复，请再次启用这些功能。
    
    ```powershell
Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
```
    
    > [!IMPORTANT]  
    > 在运行此命令后，可能需要一小时来启用单个项目恢复或诉讼保留。建议仅当此期间过后，才启用托管文件夹助理并允许客户端访问（步骤 11 和 12）。


11. 将以下配额恢复为在步骤 1 中记下的值：
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    在此示例中，从保留功能中删除了邮箱，已删除项目保留期重置为默认值 14 天，并且可恢复的项目配额配置为使用与邮箱数据库相同的值。如果在步骤 1 中记下的值有所不同，则必须使用上述参数指定每个值，并将 *UseDatabaseQuotaDefaults* 参数设置为 `$false`。如果 *RetainDeletedItemsForand UseDatabaseRetentionDefaults* 参数以前设置为不同的值，则还必须将这些参数恢复为在步骤 1 中记下的值。
    
        Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true

12. 通过将工作周期设置回在步骤 4 中记下的值，来启用托管文件夹助理。此示例将工作周期设置为一天。
    
    ```powershell
Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1
```

13. 启用客户端访问。
    
        Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true

有关语法和参数的详细信息，请参阅下列主题：

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/zh-cn/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/zh-cn/library/dd298173\(v=exchg.150\))

## 您如何知道这有效？

若要验证是否成功清理了邮箱的“可恢复的项目”文件夹，请使用 [Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa996762\(v=exchg.150\)) cmdlet 检查“可恢复的项目”文件夹的大小。

此示例将检索“可恢复的项目”文件夹及其子文件夹的大小，以及该文件夹及每个子文件夹中的项目数。

    Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto

