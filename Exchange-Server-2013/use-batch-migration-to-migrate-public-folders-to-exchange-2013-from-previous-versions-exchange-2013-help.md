---
title: '使用批处理迁移将公用文件夹从以前版本迁移到 Exchange 2013: Exchange 2013 Help'
TOCTitle: 使用批处理迁移将公用文件夹从以前版本迁移到 Exchange 2013
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64129760
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批处理迁移将公用文件夹从以前版本迁移到 Exchange 2013

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2018-03-26_

**摘要：** 本文介绍了如何将公用文件夹从 Exchange 2007 或 Exchange 2010 移动到 Exchange 2013。

本主题介绍了如何将公用文件夹从 Exchange Server 2010 SP3 RU8 或 Exchange 2007 SP3 RU15 迁移到同一林内的 Microsoft Exchange Server 2013 CU7 或更高版本中。

我们将 Exchange 2010 SP3 RU8 和 Exchange 2007 SP3 RU15 服务器称为*旧版 Exchange 服务器*。

> [!NOTE]  
> 本文中所述的批处理迁移方法是将旧版公用文件夹迁移到 Exchange 2013 支持的唯一方法。公用文件夹迁移的旧串行迁移方法即将弃用且不再受 Microsoft 支持。


您需要使用 **\*MigrationBatch** cmdlet 执行迁移，并使用 **\*PublicFolderMigrationRequest** cmdlet 进行故障排除。此外，您还会用到以下 PowerShell 脚本：

  - `Export-PublicFolderStatistics.ps1`：此脚本可创建文件夹名称到文件夹大小的映射文件。

  - ` Export-PublicFolderStatistics.psd1`：Export-PublicFolderStatistics.ps1 脚本使用此支持文件，应将此文件下载到同一位置。

  - `PublicFolderToMailboxMapGenerator.ps1`：此脚本可创建公用文件夹到邮箱的映射文件。

  - `PublicFolderToMailboxMapGenerator.strings.psd1`：PublicFolderToMailboxMapGenerator.ps1 脚本使用此支持文件，应将此文件下载到同一位置。

  - `Create-PublicFolderMailboxesForMigration.ps1` 该脚本创建用于迁移的目标公用文件夹邮箱。此外，此脚本依据[公用文件夹的限制](limits-for-public-folders-exchange-2013-help.md)中建议的每个公用文件夹邮箱上用户登录次数的准则，计算用于处理估计的用户负载所需要的邮箱数。

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` 此支持文件供 Create-PublicFolderMailboxesForMigration.ps1 脚本使用，应下载到相同的位置。

步骤 1:下载迁移脚本详细介绍了从何处可以下载这些脚本。请确保所有脚本都下载到相同的位置。

有关与公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

## 支持将公用文件夹从哪些版本的 Exchange 迁移到 Exchange 2013 中？

Exchange 支持从以下旧版 Exchange Server 移动公用文件夹：

  - Exchange 2010 SP3 RU8 或更高版本

  - Exchange 2007 SP3 RU15 或更高版本

如果您需要将公用文件夹移到 Exchange 2013 中，但您的本地服务器未运行 Exchange 2010 或 Exchange 2007 的最低支持版本，请查看[使用串行迁移将公用文件夹从以前版本迁移到 Exchange 2013](https://technet.microsoft.com/zh-cn/library/jj150486\(v=exchg.150\))。虽然您可以视需要选择使用串行迁移，但我们强烈建议您升级本地服务器，并使用批处理迁移。批处理迁移可以显著提高速度和可靠性。

您不能直接从 Exchange 2003 迁移公用文件夹。如果您组织运行的是 Exchange 2003，则需要将所有公用文件夹数据库和副本都移到 Exchange 2010 SP3 RU8 或更高版本中，或者将它们都移到 Exchange 2007 SP3 RU15 或更高版本中。Exchange 2003 上不能保留公用文件夹副本。此外，传递到 Exchange 2013 公用文件夹的邮件也不能通过 Exchange 2003 服务器进行路由。

## 在开始之前，您需要知道什么？

  - 在开始之前，我们建议您完整阅读本主题，因为有些步骤需要停机时间。

  - Exchange 2010 服务器需要运行 Exchange 2010 SP3 RU8 或更高版本。

  - Exchange 2007 服务器需要运行 Exchange 2007 SP3 RU15 或更高版本。

  - 可以一次迁移到 Exchange 2013 的公用文件夹的最大数目是 500,000。

  - 在 Exchange 2013 中，您必须是\&quot;组织管理\&quot;角色组的成员。若要详细了解如何启用\&quot;组织管理\&quot;角色组，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange 2010 中，必须是组织管理或服务器管理 RBAC 角色组的成员。有关详细信息，请参阅[向角色组添加成员](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 在 Exchange 2007 中，必须分配有 Exchange 组织管理员角色或 Exchange Server 管理员角色。此外，还必须分配有公用文件夹管理员角色和目标服务器的本地管理员组。有关详细信息，请参阅[如何向管理员角色添加用户或组](https://go.microsoft.com/fwlink/p/?linkid=81779)。

  - 在 Exchange 2007 服务器中，升级到[适用于 Windows Server 2008 x64 Edition 的 Windows PowerShell 2.0 和 WinRM 2.0](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)。

  - 开始迁移之前，您应考虑[公用文件夹的限制](limits-for-public-folders-exchange-2013-help.md)。

  - 在迁移之前，将所有用户邮箱都移到 Exchange 2013 中，因为 Exchange 2007 或 Exchange 2010 邮箱用户无权访问 Exchange 2013 上的公用文件夹。有关详细信息，请参阅[Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

  - 在多域环境中，已启用邮件的公用文件夹将停止如果在子域中运行 Exchange 迁移到 Exchange 2013 之后工作。这是因为在 Exchange 2013，已启用邮件的公用文件夹对象都需要在根域下进行。若要解决此问题，您需要禁用邮件已启用邮件的公用文件夹，然后启用邮件再次强调，它们将使您可以将它们移动到正确的域的位置。

  - 迁移完成后，如果你想要让外部发件人向迁移的已启用邮件功能的公用文件夹发送邮件，则至少需要向\&quot;**匿名**\&quot;用户授予\&quot;**创建项目**\&quot;权限。如果不执行此操作，外部发件人将收到一封传递失败通知，邮件将不会传递到迁移的已启用邮件功能的公用文件夹。要了解如何设置匿名用户的权限，请参阅[对公用文件夹启用或禁用邮件](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 第 1 步：下载迁移脚本

1.  从 [Public Folders Migration Scripts](https://go.microsoft.com/fwlink/?linkid=299838)（公用文件夹迁移脚本）下载所有的脚本和支持文件。

2.  将脚本保存到将运行 PowerShell 的本地电脑。例如，C:\\PFScripts。请确保所有的脚本都保存在相同的位置。

## 步骤 2：准备迁移

在开始迁移之前，执行以下先决条件步骤。

**适用于旧版 Exchange 服务器的先决条件步骤**

1.  为了在迁移结束时进行验证，我们建议您先在旧版 Exchange 服务器上运行以下命令，获取当前公用文件夹部署的快照：
    
      - 运行以下命令，获取原始源文件夹结构的快照：
        
        ```powershell
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
        ```
    
      - 运行以下命令，获取公用文件夹统计信息（如项目计数、大小和所有者）的快照：
        
        ```powershell
        Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
        ```
    
      - 运行以下命令，获取权限的快照：
        
        ```powershell
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
        ```

    保存上述命令所生成的信息，以供在完成迁移后进行比较。

2.  如果公用文件夹的名称中包含反斜杠\&quot;\\\&quot;，则在迁移发生时公用文件夹会在父公用文件夹中进行创建。在迁移之前，我们建议您对名称中包含反斜杠的公用文件夹进行重命名。
    
    1.  在 Exchange 2010 中，若要找到名称中包含反斜杠的公用文件夹，请运行以下命令：
        
        ```powershell
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
        ```

    2.  在 Exchange 2007 中，若要找到名称中包含反斜杠的公用文件夹，请运行以下命令：
        
        ```powershell
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
        ```

    3.  您可以使用以下命令对返回的任何公用文件夹进行重命名：
        
        ```powershell
        Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>
        ```

3.  请确保之前没有成功迁移的记录。
    
    1.  下面的示例展示了如何检查公用文件夹的迁移状态。
        
        ```powershell
        Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
        ```
        
        如果之前有成功迁移的记录，则 *PublicFoldersLockedforMigration* 或 *PublicFolderMigrationComplete* 属性的值为 `$true`。使用第 3b 步中的命令将此值设置为 `$false`。如果此值设置为 `$true`，则您的迁移请求会失败。
    
    2.  如果 *PublicFoldersLockedforMigration* 或 *PublicFolderMigrationComplete* 属性的状态为 `$true`，请使用下面的命令将此值设置为 `$false`。
        
        ```powershell
        Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
        ```
    
    > [!WARNING]  
    > 重置这些属性后，您必须等待 Exchange 检测到新设置。此过程最多可能需要两个小时才能完成。


有关语法和参数的详细信息，请参阅下列主题：

  - [Get-PublicFolder](https://technet.microsoft.com/zh-cn/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-cn/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/zh-cn/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/zh-cn/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Exchange 2013 服务器上的先决条件步骤**

1.  请确保没有现有的公用文件夹迁移请求。如果有，请清除它们，否则您自己的迁移请求将会失败。并非所有情况都需要此步骤；只有在您认为管道中可能存在现有迁移请求时，才需要此步骤。
    
    现有的迁移请求可以是下列两种类型之一：批处理迁移或串行迁移。用于检测每种类型请求和删除每种类型请求的命令如下所示。
    
    > [!IMPORTANT]  
    > 在删除迁移请求之前，请务必了解现有公用文件夹的存在原因。运行以下命令可以确定上一个请求的提出时间并诊断可能发生的任何问题。您可能需要与组织中的其他管理员沟通，以确定更改原因。
    
    下面的示例会发现任何现有的串行迁移请求。
    
    ```powershell
    Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    ```

    下面的示例展示了如何删除任何现有的公用文件夹串行迁移请求。
    
    ```powershell
    Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    ```
    
    下面的示例会发现任何现有的批处理迁移请求。
    
    ```powershell
    $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    ```

    下面的示例展示了如何删除任何现有的公用文件夹批处理迁移请求。
    
    ```powershell
    $batch | Remove-MigrationBatch -Confirm:$false
    ```

2.  请确保 Exchange 2013 服务器上没有公用文件夹或公用文件夹邮箱。
    
    1.  运行以下命令，检查是否有任何公用文件夹邮箱。
        
        ```powershell
            Get-Mailbox -PublicFolder 
        ```

    2.  如果此命令没有返回任何公用文件夹邮箱，请继续执行Step 3: Generate the CSV files。如果此命令返回了任何公用文件夹邮箱，请运行以下命令，检查是否有任何公用文件夹：
        
        ```powershell
        Get-PublicFolder
        ```
    
    3.  如果存在任何公用文件夹，请运行以下 PowerShell 命令将其删除。请确保您已保存公用文件夹中的所有信息。
        
        > [!NOTE]  
        > 删除后，公用文件夹中的所有信息都会永久删除。
        
        ```powershell
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```
        
        ```powershell
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```
        

有关语法和参数的详细信息，请参阅下列主题：

  - [Get-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-cn/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-cn/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/zh-cn/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/zh-cn/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/zh-cn/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/zh-cn/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/zh-cn/library/aa995948\(v=exchg.150\))

## 第 3 步：生成 .csv 文件

1.  在旧版 Exchange 服务器上，运行 `Export-PublicFolderStatistics.ps1` 脚本，创建文件夹名称到文件夹大小的映射文件。必须由本地管理员运行此脚本。此文件中包含以下两列：\&quot;文件夹名称\&quot;和\&quot;文件夹大小\&quot;。\&quot;文件夹大小\&quot;列的值以字节为单位显示。例如\&quot;\\PublicFolder01,10000\&quot;。
    
    ```powershell
    .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    ```

      - *FQDN of source server* 等于托管公用文件夹层次结构的邮箱服务器的完全限定的域名。
    
      - *Folder to size map path*等于 .csv 文件在用于保存其的网络共享文件夹上的文件名和路径。稍后，在本主题中，您将需要从 Exchange 2013 服务器访问此文件。如果您仅指定文件名，则会在本地计算机上的当前 PowerShell 目录中生成此文件。

2.  运行 `PublicFolderToMailboxMapGenerator.ps1` 脚本，创建公用文件夹到邮箱的映射文件。此文件用于计算 Exchange 2013 邮箱服务器上公用文件夹邮箱的正确数量。
    
    > [!NOTE]  
    > 如果公用文件夹的名称中包含反斜杠&amp;quot;\&amp;quot;，则公用文件夹会在父公用文件夹中进行创建。我们建议您查看 .csv 文件，并编辑所有包含反斜杠的名称。
    
    ```powershell
    .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    ```

      - *Maximum mailbox size in bytes*等于您要为新的公用文件夹邮箱设置的最大大小。在指定此设置时，请务必允许扩展，以便可以扩大公用文件夹邮箱。
    
      - *Folder to size map path*等于您在运行 `Export-PublicFolderStatistics.ps1` 脚本时创建的 .csv 文件的文件路径。
    
      - *Folder to mailbox map path*等于通过此步骤创建的文件夹到邮箱 .csv 文件的文件名和路径。如果您仅指定文件名，则会在本地计算机上的当前 PowerShell 目录中生成此文件。

## 第 4 步：在 Exchange 2013 中创建公用文件夹邮箱

1.  运行以下命令来创建目标公用文件夹邮箱。脚本将通过运行 PublicFoldertoMailboxMapGenerator.ps1 脚本，为您之前在步骤 3 中生成的 .csv 文件中的每个邮箱创建一个目标邮箱。
    
    ```powershell
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    ```

    *Mapping.csv* 是由 PublicFoldertoMailboxMapGenerator.ps1 脚本在步骤 3 中生成的文件。同时浏览某个公用文件夹层次结构的用户连接估计数量通常少于组织中的用户总数。

## 第 5 步：启动迁移请求

迁移 Exchange 2007 和 Exchange 2010 公用文件夹的步骤不同。

> [!TIP]  
> 无论是从 Exchange 2007 还是 Exchange 2010 进行迁移，使用适当的 cmdlet 创建批处理迁移请求后，您便可以在 EAC 中查看和管理这些请求。


**迁移 Exchange 2007 公用文件夹**

1.  由于 Exchange 2013 无法识别 Exchange 2007 中的旧版系统公用文件夹（例如 OWAScratchPad 和架构根文件夹子树），因此这些文件夹会被视为无效项目。这会导致迁移失败。作为迁移请求的一部分，您必须指定 `BadItemLimit` 参数的值。此值因您拥有的公用文件夹数据库的数量而异。以下命令可确定您拥有的公用文件夹数据库的数量，并为迁移请求计算 `BadItemLimit`。
    
    ```powershell
        $PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
    ```

    ```powershell
        $BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)
    ```

2.  在 Exchange 2013 服务器上，运行以下命令：
    
    ```powershell
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 
    ```

3.  使用以下命令开始迁移：
    
    ```powershell
    Start-MigrationBatch PFMigration
    ```

**迁移 Exchange 2010 公用文件夹**

1.  在 Exchange 2013 服务器上，运行以下命令。
    
    ```powershell
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
        `NotificationEmails` 参数是可选的。
    ```

2.  使用以下命令启动迁移：
    
    ```powershell
    Start-MigrationBatch PFMigration
    ```
    
    或：
    
    您可以在 EAC 中启动迁移。
    
    1.  登录 Exchange Online 并打开 EAC。
    
    2.  转到\&quot;收件人\&quot;\>\&quot;迁移\&quot;。
    
    3.  选择您刚刚创建的迁移批处理，然后单击启动按钮。

\&quot;状态\&quot;列会将初始批处理状态显示为\&quot;已创建\&quot;。在迁移期间，此状态会变为\&quot;正在同步\&quot;。在迁移请求完成后，此状态会变为\&quot;已同步\&quot;。您可以双击批处理，查看此批处理中各个邮箱的状态。邮箱作业的初始状态为\&quot;待运行\&quot;。在作业开始后，此状态会变为\&quot;正在同步\&quot;；当 `InitialSync` 完成后，此状态会变为\&quot;已同步\&quot;。

您可以在 EAC 中查看和管理迁移的进度和完成情况。因为 **New-MigrationBatch** cmdlet 可启动每个公用文件夹邮箱的邮箱迁移请求，所以您可以使用邮箱迁移页查看这些请求的状态。您可以转到邮箱迁移页，并通过执行以下操作，生成可以电子邮件方式发送给您的迁移报告：

1.  登录 Exchange Online 并打开 EAC。

2.  转到\&quot;邮箱\&quot;\>\&quot;迁移\&quot;。

3.  选择您刚刚创建的迁移请求，然后单击\&quot;详细信息\&quot;窗格中的\&quot;查看详细信息\&quot;。

有关语法和参数的详细信息，请参阅下列主题：

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-cn/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-cn/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-cn/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/zh-cn/library/jj218697\(v=exchg.150\))

## 步骤 6：锁定旧版 Exchange 服务器上的公用文件夹以进行最终迁移（需要停机时间）

在迁移过程中的此步骤之前，用户都可以访问公用文件夹。后续步骤会将用户从旧版公用文件夹中注销，并锁定这些文件夹直到迁移完成最终同步时为止。在此过程中，用户无法访问公用文件夹。此外，发送到启用邮件的公用文件夹的任何邮件都会排队，并且在公用文件夹迁移完成前不会进行传递。

如下所述，在运行`PublicFoldersLockedForMigration`命令之前，请确保所有作业都都处于**已同步**状态。您可以通过运行`Get-PublicFolderMailboxMigrationRequest`命令来执行此操作。只有在验证了所有作业都都处于**已同步**状态后继续此步骤。

在旧版 Exchange 服务器中，运行以下命令锁定旧版公用文件夹，以便完成迁移。

```powershell
Set-OrganizationConfig -PublicFoldersLockedForMigration:$true
```

> [!NOTE]  
> 如果由于某种原因，迁移批处理文件未完成（<strong>PublicFolderMigrationComplete</strong> 显示 <strong>False</strong>），请在旧版服务器上重启信息存储 (IS)。


有关语法和参数的详细信息，请参阅 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\))。

如果组织具有多个公用文件夹数据库，则需要等到公用文件夹复制完成，才能确保所有公用文件夹数据库都选取了 `PublicFoldersLockedForMigration` 标志，且用户最近对文件夹进行的任何挂起更改都已在整个组织中进行了融合。这可能需要几个小时。

## 步骤 7：完成公用文件夹迁移（需要停机时间）

首先，运行以下 cmdlet 以将 Exchange 2013 部署类型更改为\&quot;远程\&quot;：

```powershell
Set-OrganizationConfig -PublicFoldersEnabled Remote
```

完成此操作后，您可以通过运行下面的命令来完成公用文件夹迁移：

```powershell
Complete-MigrationBatch PublicFolderMigration
```

或者，您可以单击 EAC 中的\&quot;完成此迁移批处理\&quot;，以此来完成迁移。

迁移完成时，Exchange 将执行最终旧 Exchange 服务器和 Exchange 2013 之间同步。如果最终同步成功，Exchange 2013 服务器上的公用文件夹将解除锁定并迁移批处理的状态将更改为**完成**，然后**完成**。很常见的迁移批从**已同步**到**完成**需要几个小时之前它的状态更改，此时将开始最终同步。

## 第 8 步：测试和解除锁定公用文件夹迁移

完成公用文件夹迁移之后，您应该运行以下测试，以确保迁移成功。这样，您便能够在改为使用 Exchange 2013 公用文件夹之前测试迁移的公用文件夹层次结构。

1.  在 PowerShell 中运行以下命令，指定一些测试邮箱将任一新迁移的公用文件夹邮箱用作默认公用文件夹邮箱。
    
    ```powershell
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>
    ```

2.  使用上一步中确定的测试用户登录 Outlook 2007 或更高版本，然后执行以下公用文件夹测试：
    
      - 查看层次结构。
    
      - 检查权限。
    
      - 创建和删除公用文件夹。
    
      - 在公用文件夹中发布内容以及从中删除内容。

3.  如果您遇到任何问题，请参阅本主题后面的Roll back the migration。如果公用文件夹的内容和层次结构均可接受并符合预期，请运行以下命令，为其他所有用户解除锁定公用文件夹。
    
    ```powershell
    Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
    ```
    
    > [!IMPORTANT]  
    > 完成初始迁移验证后，请勿使用 <em>IsExcludedFromServingHierarchy</em> 参数，因为 Exchange Online 的自动存储管理服务使用此参数。


4.  在旧版 Exchange 服务器中，运行以下命令，以指示公用文件夹迁移已完成：
    
    ```powershell
    Set-OrganizationConfig -PublicFolderMigrationComplete:$true
    ```

5.  确认迁移完成后，请运行以下命令：
    
    ```powershell
    Set-OrganizationConfig -PublicFoldersEnabled Local
    ```

6.  最后，如果你想要让外部发件人向迁移的已启用邮件功能的公用文件夹发送邮件，则至少需要向\&quot;**匿名**\&quot;用户授予\&quot;**创建项目**\&quot;权限。如果不执行此操作，外部发件人将收到一封传递失败通知，邮件将不会传递到迁移的已启用邮件功能的公用文件夹。
    
    可以使用命令行管理程序或 Outlook 设置匿名用户的权限。要了解如何设置匿名用户的权限，请参阅[对公用文件夹启用或禁用邮件](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)。

## 我如何知道这有效？

在Step 2: Prepare for the migration中，我们建议您在开始迁移前先获取公用文件夹结构、统计信息和权限的快照。以下步骤会帮助您在迁移完成后获取相同的快照，以验证公用文件夹迁移是否成功。然后，您可以通过比较这两个文件中的数据来验证迁移是否成功。

1.  运行以下命令，获取新文件夹结构的快照。
    
    ```powershell
    Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml
    ```

2.  运行以下命令，获取公用文件夹统计信息（如项目计数、大小和所有者）的快照：
    
    ```powershell
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml
    ```

3.  运行以下命令，获取权限的快照。
    
    ```powershell
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml
    ```

## 从旧版 Exchange 服务器中删除公用文件夹数据库

在迁移完成且您已验证 Exchange 2013 公用文件夹可按预期运行后，您应该删除旧版 Exchange 服务器中的公用文件夹数据库。

  - 若要详细了解如何从 Exchange 2007 服务器中删除公用文件夹数据库，请参阅[删除公用文件夹数据库](https://go.microsoft.com/fwlink/?linkid=123678)。

  - 若要详细了解如何从 Exchange 2010 服务器中删除公用文件夹数据库，请参阅[删除公用文件夹数据库](https://go.microsoft.com/fwlink/?linkid=81409)。

## 回滚迁移

如果您在迁移过程中遇到问题，并且需要重新激活旧版 Exchange 公用文件夹，请按照下列步骤操作。

> [!WARNING]  
> 如果您将迁移回滚到旧版 Exchange 服务器，则会丢失发送到启用邮件的公用文件夹的所有电子邮件，或在迁移后发布到 Exchange 2013 公用文件夹中的内容。为了保存此内容，您必须将公用文件夹内容导出到 .pst 文件中，然后在回滚完成后将它再导入旧版公用文件夹中。


1.  在旧版 Exchange 服务器中，运行以下命令，解除锁定旧版 Exchange 公用文件夹。此进程可能需要几个小时才会完成。
    
    ```powershell
    Set-OrganizationConfig -PublicFoldersLockedForMigration:$False
    ```

2.  在 Exchange 2013 服务器中，运行以下命令，删除公用文件夹邮箱。
    
    ```powershell
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
    ```

3.  在旧版 Exchange 服务器中，运行以下命令，将 `PublicFolderMigrationComplete` 标志设置为 `$false`。
    
    ```powershell
    Set-OrganizationConfig -PublicFolderMigrationComplete:$False
    ```

