---
title: '使用批处理迁移将 Exchange 2013 公用文件夹迁移到 Exchange Online: Exchange Online Help'
TOCTitle: 使用批处理迁移将 Exchange 2013 公用文件夹迁移到 Exchange Online
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432704
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批处理迁移将 Exchange 2013 公用文件夹迁移到 Exchange Online

 

_**上一次修改主题：** 2018-03-26_

**摘要：** 本文介绍了如何将新式公用文件夹从 Exchange 2013 迁移到 Office 365。

将 Exchange 2013 公用文件夹迁移到 Exchange Online 需要 Exchange Server 2013 CU15 或者更高版本运行于您的内部环境。

> [!NOTE]  
> 如果组织中存在 Exchange 2013 和 Exchange 2016 公用文件夹，并且你想要将它们都移动到 Exchange Online，请使用<a href="https://go.microsoft.com/fwlink/p/?linkid=845314">本文的 Exchange 2016 版本</a>来规划和执行迁移。Exchange 2013 服务器仍需要安装 CU15 或更高版本。


## 在开始之前，您需要知道什么？

  - 在升级到 Exchange Server 2013 CU15 或更高版本时，还必须准备好 Active Directory，否则公用文件夹迁移将失败。准备好 Active Directory 可确保所有相关的 PowerShell cmdlet 和参数可供你用于准备和运行迁移。有关详细信息，请参阅[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)。

  - 在 Exchange Online 中，你必须是\&quot;组织管理\&quot;角色组的成员。该角色组与订阅 Office 365 或 Exchange Online 时分配给你的权限不同。有关如何启用\&quot;组织管理\&quot;角色组的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange Server 2013 中，你需要成为组织管理或服务器管理 RBAC 角色组的成员。有关详细信息，请参阅[向角色组添加成员](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 在开始执行公用文件夹迁移之前，如果组织中任何单个公用文件夹的大小超过 25 GB，建议你从该文件夹中删除内容以减小其大小，或者将公用文件夹的内容分为多个较小的公用文件夹。请注意，此处提到的 25 GB 限制只适用于公用文件夹，而不适用于相关文件夹可能带有的任何子级文件夹或子文件夹。如果这两种方法都不可行，建议你不要将公用文件夹移动到 Exchange Online。有关详细信息，请参阅 [Exchange Online 限制](https://go.microsoft.com/fwlink/p/?linkid=391188)。
    
    > [!NOTE]  
    > 如果 Exchange Online 中当前公用文件夹配额小于 25 GB，可以使用 <a href="https://go.microsoft.com/fwlink/p/?linkid=844062">Set-OrganizationConfig cmdlet</a>通过 DefaultPublicFolderIssueWarningQuota 和 DefaultPublicFolderProhibitPostQuota 参数来增加大小。


  - 在 Office 365 和 Exchange Online 中，可以创建最多 1000 个公用文件夹邮箱。

  - 如果你想要将用户迁移到 Office 365，应在迁移公用文件夹之前完成用户迁移。有关详细信息，请参阅[将多个电子邮件帐户迁移到 Office 365 的方法](https://go.microsoft.com/fwlink/p/?linkid=842798)。

  - 需要至少在一个同时托管公用文件夹邮箱的 Exchange 服务器上启用 MRS 代理。有关详细信息，请参阅[启用远程移动的 MRS 代理终结点](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md)。

  - 若要执行本文中的迁移过程，不能使用 Exchange 管理中心 (EAC)。而是需要使用 Exchange 2013 服务器上的 Exchange 命令行管理程序。在 Exchange Online 中，需要使用 Exchange Online PowerShell。有关详细信息，请参阅[连接到 Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=842801).。

  - 支持将已删除的项和已删除的文件夹从 Exchange 2013 迁移到 Exchange Online。在开始迁移之前，建议查看所有已删除的文件夹和文件夹项，并永久删除在 Exchange Online 中不需要的所有内容。请注意，一旦永久删除，将不能恢复。
    
    可以使用以下命令列出 Exchange 垃圾站中已删除的公用文件夹（在 Exchange 本地环境中）：
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    若要永久删除特定文件夹，请使用以下命令（本示例使用一个名为\&quot;Calendar2\&quot;的文件夹）：
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - 在开始之前，请通读本文。某些步骤需要故障时间。故障时间期间，任何人都无法访问公用文件夹。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 步骤 1：下载迁移脚本

1.  从 [Exchange 2013/2016 Public Folders Migration Scripts](https://go.microsoft.com/fwlink/p/?linkid=844893)（Exchange 2013/2016 公用文件夹迁移脚本）下载所有脚本和支持文件。

2.  将脚本保存到将运行 PowerShell 的本地电脑。例如，C:\\PFScripts。请确保所有的脚本都保存在相同的位置。

你正在下载的脚本和文件是：

  - `Sync-ModernMailPublicFolders.ps1` 此脚本在 Exchange 本地环境和 Office 365 之间同步已启用邮件的公用文件夹对象。将在 Exchange 2013 服务器上运行此脚本。

  - `SyncModernMailPublicFolders.strings.psd1` Sync-ModernMailPublicFolders.ps1 脚本使用此支持文件，应将此文件下载到同一位置。

  - `Export-ModernPublicFolderStatistics.ps1` 此脚本可创建文件夹名称到文件夹大小和已删除项大小的映射文件。将在 Exchange 2013 服务器上运行此脚本。

  - `Export-ModernPublicFolderStatistics.strings.psd1` Export-ModernPublicFolderStatistics.ps1 脚本使用此支持文件，应将此文件下载到同一位置。

  - `ModernPublicFolderToMailboxMapGenerator.ps1` 此脚本使用 Export-ModernPublicFolderStatistics.ps1 脚本的输出创建公用文件夹到邮箱的映射文件。将在 Exchange 2013 服务器上运行此脚本。

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` ModernPublicFolderToMailboxMapGenerator.ps1 脚本使用此支持文件，应将此文件下载到同一位置。

  - `SetMailPublicFolderExternalAddress.ps1` 此脚本将本地环境中已启用邮件的公用文件夹的 `ExternalEmailAddress` 更新为其 Exchange Online 对应项的该项。这将确保在迁移后，发送给已启用邮件的公用文件夹的电子邮件能够正确路由到 Exchange Online。你需要在 Exchange 2013 服务器上运行此脚本。

  - `SetMailPublicFolderExternalAddress.strings.psd1` SetMailPublicFolderExternalAddress.ps1 脚本使用此支持文件，应将此文件下载到同一位置。

## 步骤 2：准备迁移

在开始迁移公用文件夹之前，请执行以下各节中的所有先决条件步骤。

**一般先决条件步骤**

要成功迁移，应执行以下操作：

  - 请确保 Active Directory 中没有孤立的公用文件夹邮件对象。Active Directory 中的这些对象没有对应的 Exchange 对象。

  - 确认为 Active Directory 中的公用文件夹配置的 SMTP 电子邮件地址与 Exchange 对象上的 SMTP 电子邮件地址匹配。

  - 请确认 Active Directory 中没有重复的公用文件夹对象。对于避免两个或多个 Active Directory 对象指向相同的启用邮件的公用文件夹而言，这是必要的。

**本地 Exchange 2013 服务器环境中的先决条件步骤**

在 Exchange 命令行管理程序（本地）中执行以下步骤：

1.  迁移完成后，需要一些时间使 DNS 缓存通过 Internet 将邮件发送到 Exchange Online 新位置中已启用邮件的公用文件夹。可以确保新迁移的已启用邮件的公用文件夹在此 DNS 转换期间通过创建具备已知名称的接受域来接收邮件。为此，请在 Exchange 内部环境中运行以下命令。在本示例中，`target domain` 是 Office 365 或 Exchange Online 域，已通过混合配置向导为其配置发送连接器。
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **示例：** 
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    如果本地环境中已存在接受域，请将其重命名为 `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` 并保持其他属性不变。
    
    检查接受域是否已经存在于你的本地环境：
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    若要将接受域重命名为 `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`，请运行以下命令：
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    
    > [!NOTE]  
    > 如果你希望 Exchange Online 中已启用邮件的公用文件夹接收来自 Internet 的外部电子邮件，必须禁用 Exchange Online 和 Exchange Online Protection (EOP) 中的基于目录的边缘阻止 (DBEB)。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/dn600322(v=exchg.150)">使用基于目录的边缘阻止拒绝发送给无效收件人的邮件</a>。


2.  如果公用文件夹名包含反斜杠**\\**或正斜杠**/**，它可能无法在迁移过程中迁移到其指定邮箱。在迁移之前，重命名所有此类文件夹以删除这些字符
    
    1.  若要找到名称中包含反斜杠的公用文件夹，请运行以下命令：
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  您可以使用以下命令对返回的任何公用文件夹进行重命名：
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  执行以下步骤确认组织中没有上一次成功迁移的记录。如果有，则需要将该值设置为 `$false`。
    
    在更改值之前，请确认可以放弃此前尝试的迁移，以便不会意外地执行第二次迁移。
    
    1.  运行以下命令，检查是否存在之前的任何迁移过程，以及这些迁移的状态：
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        
        > [!NOTE]  
        > 如果 <code>PublicFoldersLockedforMigration</code> 或 <code>PublicFolderMigrationComplete</code> 参数是 <code>$true</code>，则意味着你曾在某个时刻迁移了旧版公用文件夹。在继续执行步骤 3b 之前，请确保已停止使用任何旧版公用文件夹数据库。
    
    2.  如果返回值设置为 `$true` 的任何以上内容，请运行以下命令，将其设置为 `$false`：
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  若要验证完成后迁移是否成功，建议在所有相应的 Exchange 2013 服务器上运行以下命令。这将获取当前公用文件夹部署的快照，可在以后使用当前部署与新迁移的公用文件夹进行比较。
    
    > [!NOTE]  
    > 由于 Exchange 组织的大小各异，它可能需要一些时间来运行这些命令。
    
      - 运行以下命令以获取原始源文件夹结构的快照。
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - 运行以下命令以获取公用文件夹统计信息（如项目计数、大小和所有者）的快照。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - 运行以下命令获取公用文件夹权限的快照。
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - 运行以下命令获取已启用邮件的公用文件夹的快照。
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - 将前面的命令生成的文件保存在安全位置，以便在迁移结束时进行比较。

5.  如果正在使用 Microsoft Azure 活动目录连接 （Azure AD 连接） 与 Azure Active Directory 同步您的内部目录，您必须执行以下操作 （如果您没有使用 Azure AD 连接，您可以跳过此步骤）：
    
    1.  在本地计算机上，打开 Microsoft Azure 活动目录连接，然后选择**配置**。
    
    2.  在**其他任务**屏幕上，选择**自定义同步选项**，然后单击**下一步**。
    
    3.  在**连接到 Azure 广告**屏幕上，输入相应的凭据，然后单击**下一步**。一旦连接，连续单击**下一步**直到您是**可选功能，**在屏幕上。
    
    4.  请确保未选择的**Exchange 邮件的公用文件夹**。如果选择，您可以继续下一节，*在 Exchange 联机系统必备组件的步骤*。如果选择它，单击以清除复选框，然后单击**下一步**。
        
        > [!NOTE]  
        > 如果您看不到<strong>Exchange 邮件的公用文件夹</strong>作为<strong>可选功能，</strong>在屏幕上的选项，可以退出 Microsoft Azure 活动目录连接并前进到下一节，<em>在 Exchange 联机系统必备组件的步骤</em>。
    
    5.  清除的**Exchange 邮件的公用文件夹**选择后，保留直到您正在**准备配置**屏幕中，单击**下一步**，然后单击**配置**。

**Exchange Online 中的先决条件步骤**

在 Exchange Online PowerShell 中运行以下命令：

1.  请确保没有现有的公用文件夹迁移请求。如果有，请清除它们，否则你自己的迁移请求将会失败。只有在你认为管道中可能存在现有迁移请求时（迁移失败或者想要中止迁移）才需要此步骤。
    
    现有的迁移请求可以是下列两种类型之一：批处理迁移或串行迁移。用于检测、删除每种类型请求的命令如下所示。
    
    下面的示例会发现任何现有的串行迁移请求：
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    下面的示例展示了如何删除任何现有的公用文件夹串行迁移请求：
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    下面的示例会发现任何现有的批处理迁移请求：
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    下面的示例展示了如何删除任何现有的公用文件夹批处理迁移请求：
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  你需要为 Office 365 租户启用迁移功能 **PAW**。在 Exchange Online PowerShell 中运行以下命令以检查此状态。
    
        Get-MigrationConfig
    
    如果\&quot;功能\&quot;下的输出具有\&quot;PAW\&quot;，则该功能已启用，你可以继续执行下一步。
    
    如果尚未为租户启用 PAW，则可能是因为你有一些现有的迁移批处理，可能是公用文件夹批处理，也可能是用户批处理。这些批处理可以处于任何状态，包括\&quot;已完成\&quot;状态。如果出现这种情况，请在运行 `Get-MigrationBatch` 后，完成并删除任何迁移批处理，直到没有记录返回。一旦删除所有现有的批处理，PAW 应自动启用。请注意，`Get-MigrationConfig` 中可能不会立即反映更改，但无需担心。在用户迁移的情况下，完成此步骤后可以继续创建新的批处理。

3.  确保 Exchange Online 中不存在任何公用文件夹或公用文件夹邮箱。如果你在遵循以下步骤后在 Exchange Online 中发现了公用文件夹，请务必在开始删除任何公用文件夹和公用文件夹邮箱之前确定它们为什么存在以及组织中的哪个人启动了公用文件夹层次结构。
    
    1.  在 Office 365 或 Exchange Online PowerShell 中，运行以下命令，检查是否存在任何公用文件夹邮箱。
        
            Get-Mailbox -PublicFolder
    
    2.  如果该命令没有返回任何公用文件夹邮箱，请继续进行Step 3: Generate the CSV files。如果该命令返回了所有公用文件夹邮箱，则运行以下命令，看看是否存在任何公用文件夹：
        
            Get-PublicFolder -Recurse
    
    3.  如果 Office 365 或 Exchange Online 中有任何公用文件夹，则（在确定不需要后）运行以下 PowerShell 命令将其删除。请在删除前确保你已保存这些公用文件夹中的任何信息，因为在你删除公用文件夹时，所有信息都将被永久删除。
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  删除公用文件夹之后，运行以下命令删除所有公用文件夹邮箱：
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## 步骤 3：生成 .csv 文件

使用以前下载的脚本生成在迁移过程中使用的 .csv 文件。

1.  从 Exchange 命令行管理程序（本地）运行 `Export-ModernPublicFolderStatistics.ps1` 脚本来创建文件夹名称到文件夹大小映射文件。必须具有本地管理员权限才能运行此脚本。生成的文件包含三列：** FolderName**、**FolderSize**，和 **DeletedItemSize**。**FolderSize** 和 **DeletedItemSize** 列的值以字节为单位显示。例如，**\\PublicFolder01,10240, 100** 表示名为 PublicFolder01 的层次结构的根中的公用文件夹大小为 10240 个字节或 10.240 MB，并且其中有 100 个字节的可恢复项。
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **示例：** 
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  运行 `ModernPublicFolderToMailboxMapGenerator.ps1` 脚本，在 Exchange Online 目的地创建将源公用文件夹映射到公用文件夹邮箱的 .csv 文件。此文件用于计算 Exchange Online 中公用文件夹邮箱的正确数量。
    
    > [!NOTE]  
    > 由<code>ModernPublicFolderToMailboxMapGenerator.ps1</code>生成的文件将不包含在您的组织中的每个公用文件夹的名称。它包含的引用指向父文件夹大文件夹树，或文件夹的名称自身都较大。您可以将此文件的&quot;异常&quot;文件用来确保某些文件夹树以及大文件夹获取放入特定公用文件夹的邮件框。是正常的看不到公用文件夹在此文件中的每一个。（除非明确提到在另一行中的映射文件，将其定向到一个不同的公用文件夹的邮箱），还将到与其父文件夹相同的公用文件夹邮箱迁移此映射文件中列出的任何文件夹的子文件夹。
    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes`是你要迁移到 Exchange Online 中任何单个公用文件夹邮箱的最大数据量。目前，此字段的最大大小为 50 GB，但我们建议使用较小的大小（例如最大大小的 50%），为以后增加大小提供空间。
    
      - `Maximum mailbox recoverable items size in bytes`是 Exchange Online 邮箱上的可恢复项配额。目前，Exchange Online 中公用文件夹邮箱的最大大小是 50 GB。我们建议将 ` RecoverableItemsQuota` 设置为 15 GB 或更小。
    
      - `Folder-to-size map path`是你在运行 `Export-ModernPublicFolderStatistics.ps1` 脚本时创建的 .csv 文件的文件路径。
    
      - `Folder-to-mailbox map path`是在此步骤中创建的文件夹到邮箱 .csv 文件的文件路径。如果仅指定文件名，则会在本地计算机上的当前 PowerShell 目录中生成此文件。

**示例：** 

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv

> [!NOTE]  
> 如果唯一的公用文件夹的邮箱中 Exchange Online 数超过 100 个，我们不支持对 Exchange 联机迁移公用文件夹。


## 步骤 4：在 Exchange Online 中创建公用文件夹邮箱

接下来，在 Exchange Online PowerShell 中创建将包含已迁移公用文件夹的目标公用文件夹邮箱。

1.  运行以下脚本来创建目标公用文件夹邮箱。在你运行 `ModernPublicFoldertoMailboxMapGenerator.ps1` 脚本后，此脚本将为你之前在*步骤 3：生成 .csv 文件*中生成的 .csv 文件中的每个邮箱创建一个目标邮箱。
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path`是由*步骤 3：生成 .csv 文件*中的 `ModernPublicFoldertoMailboxMapGenerator.ps1` 脚本生成的文件夹到邮箱 .csv 文件的文件路径。

## 步骤 5：启动迁移请求

现在需要在 Exchange 2013 本地环境和 Exchange Online 中运行大量命令。

1.  从托管公用文件夹邮箱的任何 Exchange 2013 服务器中，执行以下脚本。此脚本将启用了邮件的公用文件夹从本地 Active Directory 同步到 Exchange Online。确保你已下载此脚本的最新版本，并且你正从 Exchange 命令行管理程序中运行它。
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential`是 Exchange Online 管理用户名和密码。
    
      - `CsvSummaryFile`是你希望同步操作和错误的日志文件所在位置的文件路径。该日志将为 .csv 格式。

2.  在 Exchange 2013 服务器上，找到 MRS 代理终结点服务器并记录下来。你将需要此信息来运行迁移请求。保存此信息供以下步骤 3b 使用。

3.  在 Exchange Online PowerShell 中，运行以下命令，将凭据信息和 MRS 信息从上一步传递到将在迁移请求中使用的 cmdlet 变量。
    
    1.  将 Exchange 2013 本地环境中具有管理员权限的用户凭据传递到 `$Source_Credential` 变量中。Exchange Online 中运行的迁移请求将使用此凭据获取对本地 Exchange 2013 服务器的访问权限，将公用文件夹内容复制到 Exchange Online。
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  从 Exchange 2013 环境获取你在上述步骤 2 中找到的 MRS 代理服务器信息，并将其传入以下变量：
        
            $Source_RemoteServer = "<paste the value here>"

4.  在 Exchange Online PowerShell 中，运行以下命令，创建公用文件夹迁移终结点和公用文件夹迁移请求：
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    > [!NOTE]  
    > 用逗号分隔多个电子邮件地址。
    
    其中， `folder_mapping.csv`是映射文件中生成*步骤 3： 创建.csv 文件*。请务必提供完整的文件路径。如果出于任何原因移动映射文件，请务必使用新的位置。

5.  最后，在 Exchange Online PowerShell 中使用以下命令开始迁移：
    
        Start-MigrationBatch PublicFolderMigration

尽管批处理迁移的创建需要使用 Exchange Online PowerShell 中的 New-MigrationBatch cmdlet，但是迁移的进度和完成情况可在 EAC 中或通过运行 Get-MigrationBatch cmdlet 进行查看和管理。New-MigrationBatch cmdlet 可启动每个公用文件夹邮箱的邮箱迁移请求，并且你可以使用邮箱迁移页查看这些请求的状态。

转到邮箱迁移页：

1.  登录 Exchange Online 并打开 EAC。

2.  导航到\&quot;收件人\&quot;，然后选择\&quot;迁移\&quot;。

3.  选择你刚刚创建的迁移请求，然后在\&quot;详细信息\&quot;窗格中，选择\&quot;查看详细信息\&quot;。

在继续执行*步骤 6：在 Exchange 2013 服务器上锁定公用文件夹*之前，确认已复制所有数据，并且迁移过程正确无误。确认批处理已切换到\&quot;已同步\&quot;状态后，请运行*步骤 2：准备迁移*中提到的命令，在**本地 Exchange 2013 服务器环境中的先决条件步骤**下的最后一步中，获取本地公用文件夹的快照。在运行这些命令后，可以继续执行下一步。请注意，这些命令可能需要一段时间才能完成，具体取决于你的文件夹数目。

## 步骤 6：锁定 Exchange 2013 环境中的公用文件夹以实现最终迁移（需要公用文件夹故障时间）

在迁移过程中的此步骤之前，用户都可以访问你的本地公用文件夹。后续步骤会将用户从 Exchange 2013 公用文件夹中注销，然后锁定这些文件夹直到迁移过程完成最终同步时为止。在此过程中，用户无法访问公用文件夹，并且发送到这些已启用邮件的公用文件夹的任何邮件都会排队，并且在公用文件夹迁移完成前保持未送达状态。

如下所述，在运行`PublicFolderMailboxesLockedForNewConnections`命令之前，请确保所有作业都都处于**已同步**状态。您可以通过运行`Get-PublicFolderMailboxMigrationRequest`命令来执行此操作。只有在验证了所有作业都都处于**已同步**状态后继续此步骤。

在本地环境中，运行以下命令锁定 Exchange 2013 公用文件夹，以便完成迁移。

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true

> [!NOTE]  
> 如果您不能访问<code>-PublicFolderMailboxesLockedForNewConnections</code>参数，可能是因为将 Active Directory CU 在升级期间，未准备好因为我们建议在上面<em>您需要知道在开始之前？</em><a href="prepare-active-directory-and-domains-exchange-2013-help.md">准备 Active Directory 和域</a>的详细信息，请参阅。<br />
> 另请注意，在迁移公用文件夹本身<strong>之前</strong>，应首先迁移任何需要访问公用文件夹的用户。


如果组织在多个 Exchange 2013 服务器上具有公用文件夹邮箱，你需要等待 AD 复制完成。完成后，可以确认所有公用文件夹邮箱已选取 `PublicFolderMailboxesLockedForNewConnections` 标志，并确认整个组织中，用户最近对其公用文件夹所做的所有待定更改都已聚合。整个过程可能需要几个小时的时间。

## 步骤 7：完成公用文件夹迁移（需要公用文件夹故障时间）

您可以完成公用文件夹迁移之前，您需要确认移动没有其他公用文件夹的邮箱或公用文件夹上，将移动向内部 Exchange 环境中。要执行此操作，请使用`Get-MoveRequest`和`Get-PublicFolderMoveRequest` cmdlet 列出任何现有的公用文件夹移动。如果有任何移动正在进行或**已完成**状态，请将其删除。

下一步，要完成公用文件夹迁移，请运行以下命令 Exchange 联机 PowerShell:

    Complete-MigrationBatch PublicFolderMigration

当您运行此命令时，Exchange 将执行 Exchange 内部组织和 Exchange Online 之间最终同步。在此期间，迁移批处理的状态将变为从**已同步完成**，然后再最后对**已完成**。如果最终同步成功，则联机 Exchange 中的公用文件夹会解除。

很常见的迁移批从**已同步**到**完成**需要几个小时之前它的状态更改，此时将开始最终同步。

## 步骤 8：测试和解锁 Exchange Online 中的公用文件夹

完成公用文件夹迁移后，执行以下步骤测试迁移是否成功，并正式验证其是否完成。这些最后的任务让你可以先测试迁移的公用文件夹层次结构，然后再将组织永久切换到 Exchange Online 公用文件夹。

1.  在 Exchange Online PowerShell 中，指定一些测试用户邮箱将其中一个新迁移的公用文件夹邮箱用作其默认公用文件夹邮箱：
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    请确保测试用户具有必要的权限来创建公用文件夹。

2.  在前面的步骤中，指定，然后采取下列公用文件夹测试由测试用户登录到 Outlook。请注意，可能需要 15 到 30 分钟的更改才会生效。注意更改 Outlook 后，它可能会提示您重新启动几次。
    
    1.  查看层次结构。
    
    2.  检查权限。
    
    3.  创建一些公用文件夹，然后删除它们。
    
    4.  在公用文件夹中发布内容，以及从中删除内容。
    
    如果您遇到任何问题，并确定您不准备完全为 Exchange 联机切换您的组织的公用文件夹，请参阅[回滚从 Exchange 2013 到 Exchange Online 的公用文件夹迁移](roll-back-a-public-folder-migration-from-exchange-2013-to-exchange-online-exchange-2013-help.md)。

3.  运行下面的命令在 Exchange 联机 PowerShell 解锁自己的公用文件夹在 Exchange 联机。运行该命令后，可能需要大约 15 到 30 分钟以使更改生效。Outlook 将成为了解所做的更改后，它可能会提示您多次重新启动该程序的用户。
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 步骤 9： 完成内部部署迁移

若要启用电子邮件到部署已启用邮件的公用文件夹，请执行以下步骤：

1.  在本地环境中，运行以下脚本，确保发送到已启用邮件的公用文件夹的所有电子邮件正确路由到 Exchange Online。该脚本将使用 `ExternalEmailAddress` 标记已启用邮件的公用文件夹，将它们指向其 Exchange Online 对应项：
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  如果测试成功，则在本地环境中，运行以下命令来指示公用文件夹迁移已完成：
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## 我如何知道这有效？

在步骤 2：准备迁移中，你获取了本地公用文件夹结构、统计信息和权限的快照。以下步骤将帮助你通过在 Exchange Online 迁移后过程中获取这些相同的快照，验证公用文件夹是否成功迁移。比较这两个文件中的数据可以验证是否成功。

1.  在 Exchange Online PowerShell 中，运行以下命令以获取新文件夹结构的快照：
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  在 Exchange Online PowerShell 中，运行以下命令以获取公用文件夹统计信息（包括项目计数、大小和所有者）的快照：
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  在 Exchange Online PowerShell 中，运行以下命令以获取权限的快照：
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  在 Exchange Online PowerShell 中，运行以下命令以获取已启用邮箱的公用文件夹快照：
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## 已知问题

下面是您在您的组织中可能会遇到的常见公用文件夹迁移问题。

  - 如果唯一的公用文件夹的邮箱中 Exchange Online 数超过 100 个，我们不支持对 Exchange 联机迁移公用文件夹。

  - 根公用文件夹和 EFORMS REGISTRY 文件夹的权限不会迁移到 Exchange Online，并且必须手动将它们应用于 Exchange Online。若要执行此操作，请在 Exchange Online PowerShell 中运行以下命令。为存在于本地环境中但在 Exchange Online 中缺失的每个权限条目运行一次命令：
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - 如果某些公用文件夹的邮箱不给提供服务的公用文件夹层次结构，则某些公用文件夹迁移将失败。这意味着，对一个或多个邮箱的`IsExcludedFromServingHierarchy`参数设置为`$true`。若要避免此问题，请在 Exchange Online 提供层次结构设置所有邮箱。

  - **代理发送**和**代表发送**权限无法迁移到 Exchange Online。如果迁移期间发生这种情况，请在本地环境中使用以下命令来备注拥有这些权限的人员。
    
    查看哪些公用文件夹具有本地代理发送权限：
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    查看哪些公用文件夹具有本地代表发送权限：
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    若要在 Exchange Online 中将代理发送权限添加至已启用邮件的公用文件夹，请在 Exchange Online PowerShell 中键入以下内容：
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **示例：** 
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    若要在 Exchange Online 中将代表发送权限添加至已启用邮件的公用文件夹，请在 Exchange Online PowerShell 中键入以下内容：
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **示例：** 
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - 如果\&quot;\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT\&quot;文件夹下包含的文件夹数量超过 10,000 个，则会导致迁移失败。因此，请检查\&quot;\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT\&quot;文件夹，以查看其直接包含的文件夹（直接子级）数量是否超过了 10,000 个。可以使用以下命令查看该位置中公用文件夹的数量：
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    Exchange Online 支持的子文件夹数量不超过 10,000 个，因此迁移 10,000 个以上的文件夹将失败。目前我们正在开发脚本来破除此类配置。在此期间，建议耐心等待以迁移公用文件夹。

  - 迁移作业没有进展或已停止。如果并行运行的作业数量太多，导致作业出现间歇性错误而失败，则可能会出现此状况。可以将 `MaxConcurrentMigrations` 和 `MaxConcurrentIncrementalSyncs` 修改为较小数值，来减小并发作业数量。使用以下示例来设置这些值：
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - 迁移作业失败，出现错误\&quot;错误: 垃圾站文件夹的垃圾站。\&quot;如果看到此错误，停止批处理然后重启批处理应该可以解决此问题。

  - 迁移作业失败，并生成"请求被隔离由于如下的错误： 给定的键的字典中没有"错误消息。在迁移作业无法复制的文件夹中存在损坏的项目时，将发生这种情况。若要解决此问题：
    
    1.  停止迁移批处理。
    
    2.  标识包含错误项的文件夹。迁移报告应包括对发生错误时正在复制的文件夹的引用。
    
    3.  在本地环境中，将受影响的文件夹移动到主公用文件夹邮箱。可以使用 `New-PublicFolderMoveRequest` cmdlet 移动文件夹。
    
    4.  请等待文件夹移动来完成。完成之后，删除移动请求。然后，重新启动迁移批处理。

## 从 Exchange 本地环境中删除公用文件夹邮箱

在完成迁移并确认 Exchange Online 中的公用文件夹按预期方式工作且包含所有预期数据后，可以删除本地公用文件夹邮箱。

请注意，此步骤是不可逆的，因为一旦删除公用文件夹的邮箱时，他们就无法恢复。因此，我们强烈建议，除了验证迁移成功，也监视联机 Exchange 公用文件夹删除本地公用文件夹的邮箱之前的几周。

