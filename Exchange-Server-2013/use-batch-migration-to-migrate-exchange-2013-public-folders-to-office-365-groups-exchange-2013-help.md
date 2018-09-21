---
title: '使用批处理的迁移，将 Exchange 2013 公用文件夹迁移到 Office 365 组: Exchange 2013 Help'
TOCTitle: 使用批处理的迁移，将 Exchange 2013 公用文件夹迁移到 Office 365 组
ms:assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt843873(v=EXCHG.150)
ms:contentKeyID: 74468737
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批处理的迁移，将 Exchange 2013 公用文件夹迁移到 Office 365 组

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2018-03-26_

**摘要：**  如何将您的 Exchange 2013 公用文件夹移动到 Office 365 组。

通过一个称为*批迁移*的过程，可以将部分或全部 Exchange 2013 公用文件夹移动到 Office 365 组。组是具有某些优点在公用文件夹上的 microsoft 提供的新协作。[将公用文件夹迁移到 Office 365 组](migrate-your-public-folders-to-office-365-groups-exchange-2013-help.md)有关公用文件夹和组，以及您的组织可能会或可能不会受益于切换到组原因之间的差异的概述，请参阅。

本文包含执行实际批迁移 Exchange 2013 公用文件夹的分步过程。

## 在开始之前，您需要知道什么？

确保所有以下条件满足之前就开始准备迁移。

  - Exchange 2013 服务器需要运行**Exchange 2013 CU15**或更高版本。

  - 在 Exchange Online 中，你必须是\&quot;组织管理\&quot;角色组的成员。该角色组与订阅 Office 365 或 Exchange Online 时分配给你的权限不同。有关如何启用\&quot;组织管理\&quot;角色组的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange 2013，您必须是组织管理或服务器管理 RBAC 角色组的成员。有关详细信息，请参阅[添加到角色组的成员](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 将公用文件夹迁移到 Office 365 组之前，我们建议，第一次进入用户邮箱 Office365 对于那些迁移后需要访问 Office 365 组。有关详细信息，请参阅[迁移多个电子邮件帐户添加到 Office 365 的方法](https://support.office.com/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842)。

  - 先生： 您代理需要在至少一个 Exchange 服务器上，启用，该服务器还必须承载公用文件夹的邮箱。[启用远程移动的 MRS 代理终结点](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md)的详细信息，请参阅。

  - 不能使用 Exchange 管理员中心 (EAC) 或 Exchange 管理控制台 (EMC) 来执行此过程。在 Exchange 2013 服务器中，您需要使用 Exchange 管理外壳程序。对于 Exchange 联机状态，您需要使用Exchange Online PowerShell。有关详细信息，请参阅[连接到 Exchange 联机使用远程 PowerShell](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx)。

  - 只有类型日历和邮件的公用文件夹可以迁移到 Office 365 组这次;不支持的其他类型的公用文件夹迁移。此外，Office 365 中的目标组应在迁移之前创建。

  - 批次迁移过程仅复制邮件和日历项从公用文件夹迁移到 Office 365 组。因为那些不支持 Office 365 组，它不会复制的策略、 规则和权限，如公用文件夹的其他实体。

  - Office 365 组附带的 50 GB 的邮箱。确保要迁移公用文件夹数据的总数合计不超过 50 GB。此外，迁移后保留其他内容由您的用户在将来添加的存储空间。我们建议迁移公用文件夹不大于 25 GB 的总大小。

  - 这不是"全部或者没有"迁移。您可以挑选特定的公用文件夹，若要迁移，并且只有这些公用文件夹将会被迁移。如果正在迁移公用文件夹具有子文件夹，这些子文件夹将不会自动包括在迁移。如果您需要将其迁移，您需要显式包含它们。

  - 公用文件夹将不会受到任何方式迁移。但是，一次使用我们锁定脚本以只读的您的用户将不得不使用 Office 365 组而不是公用文件夹迁移公用文件夹。

  - 在开始之前，我们建议您阅读这篇文章中完整的停机时间是需要执行一些步骤。

## 步骤 1： 获取脚本

批次迁移到 Office 365 组需要在迁移中，不同时间点上运行多个脚本按如下所述，在这篇文章。下载脚本和其支持文件[从此位置](https://www.microsoft.com/en-us/download/details.aspx?id=55985)。所有脚本和文件都下载后，将其保存到同一位置，如`c:\PFtoGroups\Scripts`。

继续之前，请验证您已经下载并保存的所有下面的脚本和文件：

> [!NOTE]  
> 请确保将所有脚本和文件都保存到同一位置。


  - **AddMembersToGroups.ps1**。 此脚本将添加成员和所有者到 Office 365 组基于源公用文件夹中的权限项。

  - **AddMembersToGroups.strings.psd1**。 `AddMembersToGroups.ps1`脚本使用此支持文件。

  - **LockAndSavePublicFolderProperties.ps1**。 只读，以防止任何的修改，该脚本会在公用文件夹和它转移与邮件相关的公用文件夹属性 （前提是公用文件夹启用邮件） 到目标组中，其将重新路由电子邮件的公用文件夹到目标组。此脚本还备份权限条目和邮件属性之前对其进行修改。

  - **LockAndSavePublicFolderProperties.strings.psd1:**  `LockAndSavePublicFolderProperties.ps1`脚本使用此支持文件。

  - **UnlockAndRestorePublicFolderProperties.ps1**。 此脚本恢复的访问权限，并使用由`LockandSavePublicFolderProperties.ps1`创建的备份文件的公用文件夹的邮件属性。

  - **UnlockAndRestorePublicFolderProperties.strings.psd1**。 `UnlockAndRestorePublicFolderProperties.ps1`脚本使用此支持文件。

  - **WriteLog.ps1**。 此脚本启用前的三个脚本写入日志。

  - **RetryScriptBlock.ps1**。 此脚本启用的`AddMembersToGroups`、 `LockAndSavePublicFolderProperties`和`UnlockAndRestorePublicFolderProperties`的脚本尝试在瞬态错误发生某些操作。

有关`AddMembersToGroups.ps1`的详细信息， `LockAndSavePublicFolderProperties.ps1`，和`UnlockAndRestorePublicFolderProperties.ps1`，以及它们在您环境中执行的任务，请参阅迁移脚本本文内下文中。

## 步骤 2：准备迁移

以下步骤是必需准备迁移组织：

1.  编译您想迁移到 Office 365 组的公用文件夹 （邮件和日历类型） 的列表。

2.  必须为要迁移的每个公用文件夹的相应目标组的列表。您可以在 Office 365 的每个公用文件夹中创建新的组，或使用现有的组。如果您正在创建一个新组，请参阅[了解有关 Office 365 组](https://go.microsoft.com/fwlink/p/?linkid=858521)了解必须具有一组的设置。如果您正在迁移公用文件夹的默认权限集为**作者**或更高，应与**公用**的隐私设置在 Office 365 中创建相应的组。但是，对于用户，请参阅在 Outlook 中的**组**节点下的公共组，他们仍需要加入的组。

3.  重命名包含反斜杠 (\\) 在其名称中的所有公用文件夹。否则，这些公用文件夹可能无法正确迁移。

4.  您需要具有**小爪印**为 Office 365 租户启用迁移功能。若要验证这一点，请在 Exchange 联机 PowerShell 运行下面的命令：
    
    ```powershell
Get-MigrationConfig
```
    
    如果输出**功能**下，列出**小爪印**，则启用该功能，您可以继续到*第 3 步： 博客.csv 文件*。
    
    如果爪尚未为您的组织启用了，则可能是因为有一些现有的迁移批，批次公用文件夹或用户的批。这些批处理可以在任何状态下，其中包括已完成。如果出现这种情况，请完成并删除任何现有的迁移批，直到没有记录返回时您运行`Get-MigrationBatch`。一旦将删除所有现有批，爪应获得自动启用。请注意，更改可能不会反映在`Get-MigrationConfig`立即，这没什么。一旦完成此步骤后，您可以继续创建新的用户迁移的批。

## 步骤 3： 创建.csv 文件

创建.csv 文件中，这将为迁移脚本之一提供输入。

该.csv 文件需要包含以下各列：

  - **采用文件夹路径**。要迁移该公用文件夹的路径。

  - **TargetGroupMailbox**。Office 365 中的目标组的 SMTP 地址。您可以运行下面的命令以查看主 SMTP 地址。
    
    ```powershell
Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress
```

示例.csv:

    "FolderPath","TargetGroupMailbox"
    "\Sales","sales@contoso.onmicrosoft.com"
    "\Sales\EMEA","emeasales@contoso.onmicrosoft.com"

请注意一个邮件文件夹和一个日历文件夹可以合并到 Office 365 中的单个组。但是，合并到一个组中的多个公用文件夹的任何其他情况下不支持在一个批处理中单一迁移。如果需要将多个公共文件夹映射到相同的 Office 365 组，可以通过运行应执行连续、 一个接一个的不同的迁移批来实现此目的。迁移的每个批处理中可以有多达 500 项。

应将一个公用文件夹迁移到批一次迁移中的一个组。

## 第 4 步： 开始迁移请求

在此步骤中，您从您的 Exchange 环境，收集信息，然后使用该信息中Exchange Online PowerShell创建迁移批。在此之后，在开始迁移。

1.  在 Exchange 2013 服务器上，找到女士代理终结点服务器，请记下它。运行迁移请求时，将需要此信息。

2.  在Exchange Online PowerShell，使用上面返回步骤 1，运行以下命令中的信息。这些命令中的变量将步骤 1 中的值。
    
    1.  将 Exchange 2013 环境具有管理员权限的用户的凭据传递到变量`$Source_Credential`。在最终运行时迁移请求在 Exchange 联机，您将使用此凭据才能访问到 Exchange 2013 服务器才能将内容复制到 Exchange Online。
        
            $Source_Credential = Get-Credential
            <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  使用上面的步骤 1 中记下您 Exchange 2013 环境女士代理服务器信息，然后将该值传递给变量`$Source_RemoteServer`。
        
        ```powershell
$Source_RemoteServer = "<MRS proxy endpoint>"
```

3.  在Exchange Online PowerShell，运行以下命令来创建迁移终结点：
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential

4.  运行以下命令来创建新的公用文件夹到 Office 365 组迁移批。在此命令：
    
      - **CSVData**是在上面创建.csv 文件*步骤 3： 创建.csv 文件*。请务必提供该文件的完整路径。如果该文件被移动由于某种原因，请务必确认和使用新的位置。
    
      - **NotificationEmails**是一个可选参数，可以用于设置将收到有关状态和显示迁移的进度通知的电子邮件地址。
    
      - **自动启动**是可选参数，使用时，将按其创建启动迁移批处理。
    
      - **PublicFolderToUnifiedGroup**是要表明它是到 Office 365 组迁移批公用文件夹的参数。
    
    <!-- end list -->
    
        New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

5.  通过在Exchange Online PowerShell中运行下面的命令启动迁移。请注意此步骤是必需的只有当在步骤 4 中创建上面批时不使用`-AutoStart`参数。
    
    ```powershell
Start-MigrationBatch PublicFolderToGroupMigration
```

批次迁移需要在Exchange Online PowerShell中使用`New-MigrationBatch` cmdlet 来创建，而都可以查看和管理在Exchange 管理中心中显示迁移的进度。通过运行[Get-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219164\(v=exchg.150\))和[Get-MigrationUser](https://technet.microsoft.com/zh-cn/library/jj218702\(v=exchg.150\))的 cmdlet，您还可以查看显示迁移的进度。`New-MigrationBatch` cmdlet 启动每个 Office 365 组邮箱，迁移用户，您可以查看使用邮箱迁移页这些请求的状态。

若要查看邮箱迁移页：

1.  在 Exchange Online，打开Exchange 管理中心。

2.  导航到**收件人**，然后选择**迁移**。

3.  选择你刚刚创建的迁移请求，然后在\&quot;详细信息\&quot;窗格中，选择\&quot;查看详细信息\&quot;。

**已完成**的批次状态时，您可以移动到*步骤 5： 从公用文件夹中将成员添加到 Office 365 组*。

## 步骤 5： 从公用文件夹将成员添加到 Office 365 组

您可以向 Office 365 中根据需要手动的目标组中添加成员。但是，如果您想要将成员添加到组中公用文件夹的权限条目，您需要通过以下命令所示 Exchange 2013 服务器上运行`AddMembersToGroups.ps1`脚本执行此操作。必须为 Exchange 联机同步用户邮箱，才能被添加为 Office 365 组的成员。 若要了解哪些公用文件夹权限添加为 Office 365 中的组成员资格，请参阅本文后面的迁移脚本。

在下面的命令：

  - **MappingCsv**是在上面创建.csv 文件*步骤 3： 创建.csv 文件*。请务必提供该文件的完整路径。如果该文件被移动由于某种原因，请务必确认和使用新的位置。

  - **BackupDir**是迁移日志文件存储的目录。

  - **ArePublicFoldersOnPremises**是一个参数，指示是否使用公用文件夹可以位于的本地或联机 Exchange 中。

  - **凭据**是 Exchange 联机用户名称和密码。

<!-- end list -->

    .\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

用户添加到 Office 365 中的一个组后，用户就可以开始使用它。

## 步骤 6： 锁定公共文件夹 （公用文件夹所需的停机） 时间

在公用文件夹中的数据大部分有迁移到 Office 365 组，您可以运行脚本`LockAndSavePublicFolderProperties.ps1` Exchange 2013 将公用文件夹设为只读的服务器上。此步骤可确保在迁移完成之前，任何新的数据添加到公用文件夹。

> [!NOTE]  
> 如果没有已启用邮件的公用文件夹 (MEPFs) 在公众之间要迁移的文件夹此步骤将 SMTP 地址，例如 MEPFs，某些属性复制到 Office 365 中的相应组，然后禁用邮件的公用文件夹。因为迁移 MEPFs 将会禁用邮件功能之后执行此脚本，您将开始看到电子邮件发送至 MEPFs，而是接收到相应的组中。有关详细信息，请参阅本文中稍后介绍的迁移脚本。


在下面的命令：

  - **MappingCsv**是在上面创建.csv 文件*步骤 3： 创建.csv 文件*。请务必提供该文件的完整路径。如果该文件被移动由于某种原因，请务必确认和使用新的位置。

  - **BackupDir**是存储权限项目、 MEPF 属性和迁移日志文件的备份文件的目录。以防您需要回滚到公用文件夹，则该备份将非常有用。

  - **ArePublicFoldersOnPremises**是一个参数，指示是否使用公用文件夹可以位于的本地或联机 Exchange 中。

  - **凭据**是 Exchange 联机用户名称和密码。

<!-- end list -->

    .\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

## 第 7 步： 定版 Office 365 组迁移到公用文件夹

只读的做出自己的公用文件夹后，您需要执行再次迁移。这是所需的数据最终增量复制。您可以运行再次迁移之前，您需要删除现有批处理，可以通过运行下面的命令来执行此操作：

```powershell
Remove-MigrationBatch <name of migration batch>
```

接下来，一批新使用同一个.csv 文件创建通过运行下面的命令。在此命令：

  - **CsvData**是在上面创建.csv 文件*步骤 3： 创建.csv 文件*。请务必提供该文件的完整路径。如果该文件被移动由于某种原因，请务必确认和使用新的位置。

  - **NotificationEmails**是一个可选参数，可以用于设置将收到有关状态和显示迁移的进度通知的电子邮件地址。

  - **自动启动**是可选参数，使用时，将按其创建启动迁移批处理。

<!-- end list -->

    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

创建新的批处理后，通过在Exchange Online PowerShell中运行下面的命令启动迁移。请注意，此步骤才是必需的`-AutoStart`参数未使用在前面的命令。

```powershell
Start-MigrationBatch PublicFolderToGroupMigration
```

完成这一步 （批次状态为**已完成**） 后，验证所有的数据，已复制到 Office 365 组。此时，只要您满意组体验，您可以开始迁移公用文件夹删除 Exchange 2013 环境。

> [!IMPORTANT]  
> 虽然有支持回滚迁移并返回到公用文件夹的过程，这可能不后源公用文件夹已被删除。 请参阅如何执行回滚到公用文件夹从 Office 365 组？的详细信息。


## 已知问题

以下已知的问题可能会发生典型的公用文件夹到 Office 365 组迁移。

  - 已启用邮件的公用文件夹传输 SMTP 地址到 Office 365 组仅作为辅助的电子邮件添加地址的脚本在 Exchange 地址联机。因此，如果您的环境中在线保护 Exchange (EOP) 或集中式邮件流的设置，必须将电子邮件发送到组 （对第二电子邮件地址中） 迁移后的问题。

  - 如果.csv 映射文件具有无效的公共文件夹路径条目，迁移批显示为**已完成**而不会引发错误，并没有进一步的数据将被复制。

## 迁移的脚本

为了便于参考，本部分提供深入说明迁移脚本以及它们在您的 Exchange 环境中执行的任务中的三个。所有脚本和支持文件都可以[从该位置下载](https://www.microsoft.com/en-us/download/details.aspx?id=55985)。

## AddMembersToGroups.ps1

此脚本将读取正在迁移公用文件夹的权限，然后添加成员和所有者到 Office 365 组，如下所示：

  - 用下列权限角色的用户将被添加为成员到 Office 365 中的组。 **权限的角色：**  所有者、 PublishingEditor、 编辑器、 PublishingAuthor、 作者

  - 除上述，以下的最小访问权限与用户权限将还作为成员添加到 Office 365 中的组。 **访问权限：**  ReadItems、 CreateItems、 FolderVisible、 EditOwnedItems、 DeleteOwnedItems

  - 用户具有访问权限的"所有者"将向组添加为所有者，并与其他有资格的访问权限的用户将被添加为成员。

  - 无法将安全组作为成员添加到 Office 365 中的组。因此他们将被扩展，并且然后各个用户将被添加为成员或所有者到基于访问权限的安全组的组。

  - 当在安全组中的用户具有访问权限通过公用文件夹拥有自己明确的权限通过同一个公用文件夹时，显式权限将给予优先。 例如，请考虑在其中安全组称为"SG1"案例的 User1 和 User2 的成员。为公用文件夹"PF1"权限条目如下所示：
    
    在 PF1 SG1： 作者
    
    在 PF1 User1： 所有者
    
    在这种情况下，User1 将作为所有者添加到 Office 365 中的组。

  - 迁移公用文件夹的默认权限是 '作者' 或更高，该脚本将建议设置的相应组的隐私设置为公共。

运行此脚本可以锁定的公用文件夹，即使使用参数设置为` $true``ArePublicFoldersLocked` 。在这种情况下，脚本将读取权限从锁定过程中创建文件的备份。

## LockAndSavePublicFolderProperties.ps1

此脚本将只读的迁移公用文件夹。已启用邮件的公用文件夹迁移时，使用它们将首先被禁用邮件功能和其 SMTP 地址将被添加到 Office 365 中的各个组。然后的权限项将被修改以使其成为只读的。在其上执行任何修改之前，将复制备份的已启用邮件的公用文件夹的邮件属性，以及所有公用文件夹的权限项。

如果有多个迁移批，应与每个映射.csv 文件使用单独的备份目录。

将存储下面的邮件属性，以及各自的已启用邮件的公用文件夹和 Office 365 组：

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - SendAs 受信者列表

上述邮件属性将存储在.csv 文件中，可以在恢复过程回滚使用 (如果您想要返回到使用公用文件夹，请参阅如何执行回滚到公用文件夹从 Office 365 组？的详细信息)。此外将在名为 PfMailProperties.csv 的文件中存储的已启用邮件的公用文件夹的属性快照。此文件不需要回滚过程，但仍可供您参考使用。

下列邮件属性将被移植到目标组作为锁定的一部分：

  - PrimarySMTPAddress

  - EmailAddresses

  - SendAs 受信者列表

  - GrantSendOnBehalfTo

该脚本可以确保 PrimarySMTPAddress 和 EmailAddresses 的迁移已启用邮件的公用文件夹将添加为辅助的 Office 365 中的相应组的 SMTP 地址。此外，SendAs 和 SendOnBehalfTo 权限的已启用邮件的公用文件夹的用户将获得等效权限对应的目标组中。

**允许的访问权限**

仅以下访问权限将允许用户以确保公用文件夹的所有用户以只读方式进行。这些模板存储在**ListOfAccessRightsAllowed**中。

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

权限项将被修改，如下所示：

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>在锁定之前</th>
    <th>之后锁定</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>无</p></td>
    <td><p>无</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>参与者</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Reviewer</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Aughor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>编辑器</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>所有者</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  没有读权限的用户的访问权限将保持不变，并且他们将继续阻止读取权限。

3.  对于具有自定义角色的用户，将删除不是**ListOfAccessRightsAllowed**中的所有访问权限。筛选后，用户不能从允许列表中的任何访问权限，这些用户的访问权限将设置为无。

可能发送电子邮件到已启用邮件的公用文件夹之间的时间内文件夹会禁用邮件功能和其 SMTP 地址添加到 Office 365 组时的中断。

## UnlockAndRestorePublicFolderProperties.ps1

此脚本将重新分配回基于休公用文件夹锁定的文件备份的公用文件夹的权限。此脚本将还启用邮件的公用文件夹必须已禁用邮件功能、 后它从 Office 365 中它们各自的组中删除文件夹的 SMTP 地址。在此过程中可能有轻微的停机时间。

## 如何回滚到公用文件夹从 Office 365 组？

那如果您改变主意，想要恢复到后使用 Office 365 组，下面列出的命令将恢复您的环境的状态，请使用公用文件夹是迁移前。前滚回可执行只要备份文件存在，并且，只要不删除公用文件夹迁移后。

在 Exchange 2013 服务器上，运行以下命令。在此命令：

  - **BackupDir**是存储权限项目、 MEPF 属性和迁移日志文件的备份文件的目录。请确保使用相同的位置中指定*步骤 6： 锁定在一个位置的公用文件夹来切换 （公用文件夹所需的停机） 时间*。

  - **ArePublicFoldersOnPremises**是一个参数，指示是否使用公用文件夹可以位于的本地或联机 Exchange 中。

  - **凭据**是 Exchange 联机用户名称和密码。

<!-- end list -->

    .\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

请注意添加到 Office 365 的组中或在组中，执行任何编辑操作的任何项目不会复制到公用文件夹。因此将会有数据丢失，假定为新数据添加了一组公用文件夹时。

还要注意不能恢复公用文件夹，这就意味着所有的公用文件夹迁移应恢复的一个子集。

Office 365 中的相应组不会删除作为掷骰恢复进程的一部分。您需要清理或手动删除这些组。

