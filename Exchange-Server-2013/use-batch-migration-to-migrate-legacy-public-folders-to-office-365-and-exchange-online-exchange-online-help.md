---
title: '使用批处理迁移将旧版公用文件夹迁移到 Office 365 和 Exchange Online: Exchange Online Help'
TOCTitle: 使用批处理迁移将旧版公用文件夹迁移到 Office 365 和 Exchange Online
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63895119
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批处理迁移将旧版公用文件夹迁移到 Office 365 和 Exchange Online

 

_**适用于：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：**2018-03-26_

**摘要：**使用这些过程将您的 Exchange 2007 和 Exchange 2010 公用文件夹移动到 Office 365。

本主题说明如何将您的公用文件夹通过直接转换迁移或暂存迁移从 Exchange Server 2010 Service Pack 3 (SP3) 更新汇总 8 或 Exchange 2007 SP3 更新汇总 15 迁移到 Office 365 或 Exchange Online。

本主题将 Exchange 2010 SP3 RU8 和 Exchange 2007 SP3 RU15 服务器称为*旧版 Exchange 服务器*。此外，本主题中的步骤同时适用于 Exchange Online 和 Office 365。本主题中的术语可以互换使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本文中所述的批处理迁移方法是将旧版公用文件夹迁移到 Office 365 和 Exchange Online 的唯一受支持方法。公用文件夹迁移的旧串行迁移方法即将弃用且不再受 Microsoft 支持。</td>
</tr>
</tbody>
</table>


我们建议您不要使用 Outlook 的 PST 导出功能将公用文件夹迁移到 Office 365 或 Exchange Online。Office 365 和 Exchange Online 公用文件夹邮箱增长使用自动拆分功能进行管理，此功能可在公用文件夹邮箱超过大小配额时对其进行拆分。当您使用 PST 导出功能迁移公用文件夹时，自动拆分无法应对公用文件夹邮箱的突然增长，您可能必须至少等待两星期，自动拆分才会将数据从主邮箱中移出。我们建议您使用本文档中基于 cmdlet 的说明将公用文件夹迁移到 Office 365 和 Exchange Online。但是，如果您选择使用 PST 导出迁移公用文件夹，请参阅本主题后面的使用 Outlook PST 导出将公用文件夹迁移到 Office 365部分。

将使用 **\*-MigrationBatch** cmdlet 以及以下 PowerShell 脚本来执行迁移：

  - `Export-PublicFolderStatistics.ps1`   此脚本将创建文件夹名称到文件夹大小的映射文件。将在旧版 Exchange 服务器上运行此脚本。

  - `Export-PublicFolderStatistics.psd1`   此支持文件由 `Export-PublicFolderStatistics.ps1` 脚本使用，并且应该下载到同一位置。

  - `PublicFolderToMailboxMapGenerator.ps1`   此脚本使用 `Export-PublicFolderStatistics.ps1` 脚本的输出创建公用文件夹到邮箱的映射文件。将在旧版 Exchange 服务器上运行此脚本。

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   此支持文件由 `PublicFolderToMailboxMapGenerator.ps1` 脚本使用，并且应该下载到同一位置。

  - `Create-PublicFolderMailboxesForMigration.ps1` 该脚本创建用于迁移的目标公用文件夹邮箱。此外，此脚本依据[公用文件夹的限制](limits-for-public-folders-exchange-2013-help.md)中建议的每个公用文件夹邮箱上用户登录次数的准则，计算用于处理估计的用户负载所需要的邮箱数。

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` 此支持文件供 Create-PublicFolderMailboxesForMigration.ps1 脚本使用，应下载到相同的位置。

  - `Sync-MailPublicFolders.ps1`   此脚本在您的本地 Exchange 部署和 Office 365 之间同步已启用邮件的公用文件夹对象。将在旧版 Exchange 服务器上运行此脚本。

  - `SyncMailPublicFolders.strings.psd1`   这是由 `Sync-MailPublicFolders.ps1` 脚本使用的支持文件，并且应当将其复制至与上述脚本相同的位置。

步骤 1:下载迁移脚本详细介绍了从何处可以下载这些脚本。请确保所有脚本都下载到相同的位置。

有关与公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

## 将公用文件夹迁移到 Office 365 和 Exchange Online 的操作支持哪些 Exchange 版本？

Exchange 支持将您的公用文件夹从以下旧版 Exchange Server 移动至 Office 365 和 Exchange Online：

  - Exchange 2010 SP3 RU8 或更高版本

  - Exchange 2007 SP3 RU15 或更高版本

如果您需要将公用文件夹移动到 Exchange Online，但您的本地服务器未运行 Exchange 2010 或 Exchange 2007 的最低支持版本，我们强烈建议您升级本地服务器并使用批处理迁移，这是唯一受支持的公用文件夹迁移方法。

您不能将公用文件夹直接从 Exchange 2003 迁移出来。如果您的组织运行的是 Exchange 2003，您需将所有公用文件夹数据库和副本移动到 Exchange 2010 SP3 RU8 或更高版本或者 Exchange 2007 SP3 RU10 或更高版本。没有公用文件夹副本可以在 Exchange 2003 上保留。此外，发往 Exchange 2013 公用文件夹的邮件不能通过 Exchange 2003 服务器进行路由。

## 在开始之前，您需要知道什么？

  - Exchange 2010 服务器需要运行 Exchange 2010 SP3 RU8 或更高版本。

  - Exchange 2007 服务器需要运行 Exchange 2007 SP3 RU15 或更高版本。

  - 在 Office 365 和 Exchange Online 中，您必须是\&quot;组织管理\&quot;角色组的成员。该角色组与订阅 Office 365 或 Exchange Online 时分配给您的权限不同。有关如何启用\&quot;组织管理\&quot;角色组的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange 2010 中，必须是组织管理或服务器管理 RBAC 角色组的成员。有关详细信息，请参阅[向角色组添加成员](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 在 Exchange 2007 中，必须分配有 Exchange 组织管理员角色或 Exchange Server 管理员角色。此外，还必须分配有公用文件夹管理员角色和目标服务器的本地管理员组。有关详细信息，请参阅[如何向管理员角色添加用户或组](https://go.microsoft.com/fwlink/p/?linkid=81779)。

  - 在 Exchange 2007 服务器中，升级到 [Windows Server 2008 x64 Edition 的 Windows PowerShell 2.0 和 WinRM 2.0](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。

  - 迁移之前，如果组织中有任何公用文件夹大于 2 GB，我们建议删除该文件夹的内容或者将其拆分为多个公用文件夹。如果这两个选项都不可行，我们建议您不要将公用文件夹移动到 Office 365 和 Exchange Online。

  - 在 Office 365 和 Exchange Online 中，可以创建最多 1,000 个公用文件夹邮箱。

  - 在迁移公用文件夹之前，我们建议先将所有用户邮箱移动到 Office 365 和 Exchange Online。有关详细信息，请参阅[将多个电子邮件帐户迁移到 Office 365 的方法](https://go.microsoft.com/fwlink/p/?linkid=524030)。

  - 必须在旧版 Exchange 服务器上启用 Outlook 无处不在。有关如何在 Exchange 2010 服务器上启用 Outlook 无处不在的详细信息，请参阅[启用 Outlook 无处不在](https://go.microsoft.com/fwlink/p/?linkid=187249)。有关如何在 Exchange 2007 服务器上启用 Outlook 无处不在的详细信息，请参阅[如何启用 Outlook 无处不在](https://go.microsoft.com/fwlink/p/?linkid=167210)。

  - 不能使用 Exchange 管理中心 (EAC) 或 Exchange 管理控制台 (EMC) 执行此过程。在旧版 Exchange 服务器上，需要使用 Exchange 命令行管理程序。对于 Exchange Online，需要使用 Exchange Online PowerShell。有关详细信息，请参阅[使用远程 PowerShell 连接到 Exchange Online](https://technet.microsoft.com/zh-cn/library/jj984289\(v=exchg.150\))。

  - 在开始之前，我们建议完整阅读本主题，因为有些步骤需要停机。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您该如何做？

## 第 1 步：下载迁移脚本

1.  从 [Public Folders Migration Scripts](https://go.microsoft.com/fwlink/?linkid=299838)（公用文件夹迁移脚本）下载所有的脚本和支持文件。

2.  将脚本保存到将运行 PowerShell 的本地电脑。例如，C:\\PFScripts。请确保所有的脚本都保存在相同的位置。

3.  从 [Mail-enabled Public Folders - directory sync script](http://go.microsoft.com/fwlink/p/?linkid=532376)（启用邮件的公用文件夹 - 目录同步脚本）下载以下文件：
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  将脚本保存到与步骤 2 操作相同的位置。例如，C:\\PFScripts。

## 步骤 2：准备迁移

在开始迁移之前，执行以下先决条件步骤。

**一般先决条件步骤**

  - 请确保 Active Directory 中没有孤立的公用文件夹邮件对象，表示 Active Directory 中的对象没有对应的 Exchange 对象。

  - 确认为 Active Directory 中的公用文件夹配置的 SMTP 电子邮件地址与 Exchange 对象上的 SMTP 电子邮件地址匹配。

  - 请确保 Active Directory 中没有重复的公用文件夹对象，以避免两个或多个 Active Directory 对象 指向相同的启用邮件的公用文件夹这种情况。

**旧版 Exchange 服务器上的先决条件步骤**

1.  在旧版 Exchange 服务器上，确保可继续正常路由到将存在于 Office 365 或 Exchange Online 中的已启用邮件的公用文件夹，直到所有通过 Internet 的 DNS 缓存更新到指向您组织目前所在的 Office 365 或 Exchange Online DNS。为此，运行以下命令配置一个已知名称的接受域，它将会正确地将电子邮件消息路由到 Office 365 或 Exchange Online 域。
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  如果公用文件夹的名称包含反斜线 **\\**，在迁移发生时将在父公用文件夹中创建该公用文件夹。在迁移之前，我们建议您为名称中包含反斜线的公用文件夹重命名。
    
    1.  在 Exchange 2010 中，若要找到名称中包含反斜杠的公用文件夹，请运行以下命令：
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  在 Exchange 2007 中，若要找到名称中包含反斜杠的公用文件夹，请运行以下命令：
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  如果返回任何公用文件夹，您可以通过使用以下命令对它们进行重命名：
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  确保之前没有成功迁移的记录。如果存在，则需要将该值设置为 `$false`。如果该值设置为 `$true`，则迁移请求将失败。
    
    1.  下面的示例检查公用文件夹迁移状态。
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  如果 *PublicFoldersLockedforMigration* 或 *PublicFolderMigrationComplete* 属性的状态为 `$true`，请使用下面的命令将此值设置为 `$false`。
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在重置这些属性之后，必须等待 Exchange 检测到新设置。这可能需要两个小时才能完成。</td>
    </tr>
    </tbody>
    </table>


4.  为了在迁移结束时进行验证，我们建议您先在旧版 Exchange 服务器上运行以下 Exchange 命令行管理程序 命令，获取当前公用文件夹部署的快照。
    
    1.  运行以下命令以获取原始源文件夹结构的快照。
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  运行以下命令以获取公用文件夹统计信息（如项目计数、大小和所有者）的快照。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  运行以下命令获取权限的快照。
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    保存来自上述命令的信息以便在迁移结束时进行比较。

5.  如果正在使用 Microsoft Azure 活动目录连接 （Azure AD 连接） 与 Azure Active Directory 同步您的内部目录，您需要执行以下操作 （如果您没有使用 Azure AD 连接，您可以跳过此步骤）：
    
    1.  在本地计算机上，打开 Microsoft Azure 活动目录连接，然后选择**配置**。
    
    2.  在**其他任务**屏幕上，选择**自定义同步选项**，然后单击**下一步**。
    
    3.  在**连接到 Azure 广告**屏幕上，输入相应的凭据，然后单击**下一步**。一旦连接，连续单击**下一步**直到您是**可选功能，**在屏幕上。
    
    4.  请确保未选择的**Exchange 邮件的公用文件夹**。如果选择，您可以继续下一节， *Office 365 或 Exchange Online 中步骤的先决条件*。如果选择它，单击以清除复选框，然后单击**下一步**。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您看不到<strong>Exchange 邮件的公用文件夹</strong>作为<strong>可选功能，</strong>在屏幕上的选项，可以退出 Microsoft Azure 活动目录连接并前进到下一节， <em>Office 365 或 Exchange Online 中步骤的先决条件</em>。</td>
        </tr>
        </tbody>
        </table>
    
    5.  清除的**Exchange 邮件的公用文件夹**选择后，保留直到您正在**准备配置**屏幕中，单击**下一步**，然后单击**配置**。

有关语法和参数的详细信息，请参阅下列主题：

  - [New-AcceptedDomain](https://technet.microsoft.com/zh-cn/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/zh-cn/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-cn/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/zh-cn/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/zh-cn/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Office 365 或 Exchange Online 中的先决条件步骤**

1.  请确保没有现有的公用文件夹迁移请求。如果有，请清除它们，否则您自己的迁移请求将会失败。并非所有情况都需要此步骤；只有在您认为管道中可能存在现有迁移请求时，才需要此步骤。
    
    现有的迁移请求可以是下列两种类型之一：批处理迁移或串行迁移。用于检测每种类型请求和删除每种类型请求的命令如下所示。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在删除迁移请求之前，请务必了解现有公用文件夹的存在原因。运行以下命令可以确定上一个请求的提出时间并诊断可能发生的任何问题。您可能需要与组织中的其他管理员沟通，以确定更改原因。</td>
    </tr>
    </tbody>
    </table>
    
    下面的示例会发现任何现有的串行迁移请求。
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    下面的示例展示了如何删除任何现有的公用文件夹串行迁移请求。
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    下面的示例会发现任何现有的批处理迁移请求。
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    下面的示例展示了如何删除任何现有的公用文件夹批处理迁移请求。
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  确保 Office 365 中不存在任何公用文件夹或公用文件夹邮箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果看 Office 365 或联机 Exchange 中的公用文件夹，请务必确定为什么他们有和您的组织中谁之前删除公用文件夹和公用文件夹的邮箱启动公用文件夹层次结构。</td>
    </tr>
    </tbody>
    </table>
    
    1.  在 Office 365 或 Exchange Online PowerShell 中，运行以下命令，检查是否存在任何公用文件夹邮箱。
        
            Get-Mailbox -PublicFolder 
    
    2.  如果该命令没有返回任何公用文件夹邮箱，请继续进行Step 3: Generate the CSV files。如果该命令返回了所有公用文件夹邮箱，则运行以下命令，看看是否存在任何公用文件夹：
        
            Get-PublicFolder
    
    3.  如果 Office 365 或 Exchange Online 中有公用文件夹，则运行以下 Exchange Online PowerShell 命令将其删除。请确保您已保存了 Office 365 中公用文件夹内的任何信息。删除公用文件夹后，公用文件夹中包含的所有信息将永久删除。
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  删除公用文件夹之后，运行以下命令删除所有公用文件夹邮箱。
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

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

## 步骤 3：生成 .csv 文件

1.  在旧版 Exchange 服务器上，运行 `Export-PublicFolderStatistics.ps1` 脚本以创建文件夹名称到文件夹大小的映射文件。此脚本需始终由本地管理员运行。该文件具有两列：\&quot;FolderName\&quot;和\&quot;FolderSize\&quot;。\&quot;FolderSize\&quot;列的值将以字节为单位显示。例如\&quot;\\PublicFolder01,10000\&quot;。
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* 等于托管公用文件夹层次结构的邮箱服务器的完全限定域名。
    
      - *Folder to size map path* 等于要用于保存 .csv 文件的网络共享文件夹上的文件名称和路径。主题后面部分中，您将需要使用 Exchange Online PowerShell 来访问此文件。如果您仅指定文件名，则将在本地计算机上的当前 PowerShell 目录中生成文件。
    
      - 如有必要，从脚本输出删除任何已启用邮件的系统文件夹，然后再继续。

2.  运行 `PublicFolderToMailboxMapGenerator.ps1` 脚本来创建公用文件夹到邮箱的映射文件。此文件用于计算 Exchange Online 中公用文件夹邮箱的正确数量。
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>公用文件夹的邮箱的映射文件不应超过 1000 行。如果此文件超过 1000 行，公用文件夹结构需要进行简化。继续执行的文件大于 1000 行不推荐，会导致迁移错误。</td>
    </tr>
    </tbody>
    </table>
    
      - 在运行脚本之前，使用以下 cmdlet 来检查您联机 Exchange 组织中的当前公用文件夹限制。然后，记下的公用文件夹的当前配额值。 `Get-OrganizationConfig | fl *quota*`
        
        在 Exchange Online，默认值是**DefaultPublicFolderIssueWarningQuota**为 1.7 GB 和 2 GB 分配给**DefaultPublicFolderProhibitPostQuota**。
    
      - *Maximum mailbox size in bytes*等于您想设置为新的公用文件夹邮箱的最大大小。联机 Exchange 中的公用文件夹的邮箱的最大大小为 100 GB。我们建议使用 15 GB 的设置，以便每个公用文件夹的邮箱有增长的空间。Exchange Online 都有默认公用文件夹"禁止发布"配额为 2 GB。如果您具有单独的公用文件夹的大小超过 2 GB，可以使用下列选项来解决此问题：
        
          - 在开始迁移批之前，通过运行以下 cmdlet 增加默认公用文件夹"禁止发布"配额：
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - 在开始迁移批之前，删除公用文件夹内容以减少内容的大小为 2 GB 或更少。
        
          - 在开始迁移批之前，分割的公用文件夹到多个公用文件夹，每个 2 GB 或更少。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果公用文件夹是大于 30 GB，而如果它不可行，若要删除内容或将其拆分到多个公用文件夹，则建议您不要到 Exchange 联机移动公用文件夹。</td>
        </tr>
        </tbody>
        </table>
    
      - *Folder to size map path*等于时运行`Export-PublicFolderStatistics.ps1`脚本创建.csv 文件的文件路径。
    
      - *Folder to mailbox map path*等于文件的名称和您在此步骤中创建的文件夹到邮箱.csv 文件的路径。如果您指定的文件名，该文件是本地计算机上的当前 PowerShell 目录中生成。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将运行的脚本并生成的.csv 文件之后，任何新的公用文件夹或对现有的公用文件夹的更新将不会收集。</td>
</tr>
</tbody>
</table>


## 步骤 4：在 Exchange Online 中创建公用文件夹邮箱

1.  运行以下命令来创建目标公用文件夹邮箱。脚本将通过运行 PublicFoldertoMailboxMapGenerator.ps1 脚本，为您之前在步骤 3 中生成的 .csv 文件中的每个邮箱创建一个目标邮箱。
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* 是由 PublicFoldertoMailboxMapGenerator.ps1 脚本在步骤 3 中生成的文件。同时浏览某个公用文件夹层次结构的用户连接估计数量通常少于组织中的用户总数。

## 第 5 步：启动迁移请求

1.  在旧版 Exchange 服务器上，运行以下命令，将启用邮件的公用文件夹从本地 Active Directory 同步到 Exchange Online。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` 是您的 Office 365 用户名和密码。`CsvSummaryFile` 是您要以 .CSV 格式记录同步操作和错误的文件路径。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>我们建议您先模拟脚本操作，然后再实际运行此脚本（为此，可使用 <code>-WhatIf</code> 参数）。</td>
    </tr>
    </tbody>
    </table>


2.  在旧版 Exchange 服务器上，获取运行迁移请求所需的以下信息：
    
    1.  查找用户帐户的 `LegacyExchangeDN`，该用户帐户是\&quot;公用文件夹管理员\&quot;角色的成员。这将是此过程步骤 3 中您所需凭据的同一用户。
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  查找具有公用文件夹数据库的任何邮箱服务器的 `LegacyExchangeDN`。
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  查找 Outlook 无处不在 主机名的 FQDN。如果您有多个 Outlook 无处不在 实例，我们建议您选择最接近迁移终结点的实例或最接近旧版 Exchange 组织中公用文件夹副本的实例。以下命令将找到 Outlook 无处不在 的所有实例：
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  在 Office 365 PowerShell 中，运行以下命令，将前一步骤返回的信息传递到将在迁移请求中使用的变量。
    
    1.  将旧版 Exchange 服务器上具有管理权限的用户凭据传递到 `$Source_Credential` 变量中。Exchange Online 中运行的迁移请求将使用此凭据获取对旧版 Exchange 服务器的访问，以复制内容。
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  使用步骤 2a 中找到的旧版 Exchange 服务器上迁移用户的 `ExchangeLegacyDN`，将它传递到变量 `$Source_RemoteMailboxLegacyDN` 中。
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  使用以上步骤 2b 中找到的公用文件夹服务器的 `ExchangeLegacyDN`，将它传递到变量 `$Source_RemotePublicFolderServerLegacyDN`。
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  使用以上步骤 2c 中找到的 Outlook 无处不在 的外部主机名，将它传递到变量 `$Source_OutlookAnywhereExternalHostName` 中。
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  最后，在 Exchange Online PowerShell 中，运行以下命令，创建迁移请求。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>以下 Exchange 命令行管理程序 示例中的身份验证方法必须匹配您的 Outlook 无处不在 设置，否则命令将失败。</td>
    </tr>
    </tbody>
    </table>
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    其中 \<*folder\_mapping.csv*\> 文件是在Step 3: Generate the .csv files中生成的。

5.  使用以下命令开始迁移：
    
        Start-MigrationBatch PublicFolderMigration

尽管批处理迁移的创建需要使用 Exchange 命令行管理程序 中的 **New-MigrationBatch** cmdlet，但是迁移的进度和完成情况可在 EAC 中进行查看和管理。因为 **New-MigrationBatch** cmdlet 可启动每个公用文件夹邮箱的邮箱迁移请求，你可以使用邮箱迁移页查看这些请求的状态。你可以进入邮箱迁移页，通过执行下列操作，创建可以通过电子邮件发送给你的迁移报告：

1.  登录到 Exchange Online 并打开 EAC。

2.  转到\&quot;邮箱\&quot;\>\&quot;迁移\&quot;。

3.  选择您刚刚创建的迁移请求，然后单击\&quot;详细信息\&quot;窗格中的\&quot;查看详细信息\&quot;。

有关语法和参数的详细信息，请参阅下列主题：

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/zh-cn/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/zh-cn/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-cn/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-cn/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-cn/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/zh-cn/library/jj218697\(v=exchg.150\))

## 步骤 6：锁定旧版 Exchange 服务器上的公用文件夹以进行最终迁移（需要停机时间）

在迁移过程中的此步骤之前，用户都可以访问公用文件夹。后续步骤会将用户从旧版公用文件夹中注销，并锁定这些文件夹直到迁移完成最终同步时为止。在此过程中，用户无法访问公用文件夹。此外，发送到启用邮件的公用文件夹的任何邮件都会排队，并且在公用文件夹迁移完成前不会进行传递。

如下所述，在运行`PublicFoldersLockedForMigration`命令之前，请确保所有作业都都处于**已同步**状态。您可以通过运行`Get-PublicFolderMailboxMigrationRequest`命令来执行此操作。只有在验证了所有作业都都处于**已同步**状态后继续此步骤。

在旧版 Exchange 服务器中，运行以下命令锁定旧版公用文件夹，以便完成迁移。

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

有关语法和参数的详细信息，请参阅 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\))。

如果组织具有多个公用文件夹数据库，则需要等到公用文件夹复制完成，才能确保所有公用文件夹数据库都选取了 `PublicFoldersLockedForMigration` 标志，且用户最近对文件夹进行的任何挂起更改都已在整个组织中进行了融合。这可能需要几个小时。

## 步骤 7：完成公用文件夹迁移（需要停机时间）

若要完成公用文件夹迁移，请运行以下命令：

    Complete-MigrationBatch PublicFolderMigration

迁移完成时，Exchange 将执行最终同步之间的旧 Exchange 服务器和 Exchange 联机。如果最终同步成功，联机 Exchange 中的公用文件夹将解除锁定并迁移批处理的状态将更改为**已完成**。很常见的迁移批从**已同步**到**完成**需要几个小时之前它的状态更改，此时将开始最终同步。

如果已在本地 Exchange 服务器和 Office 365 之间配置混合部署，则在迁移完成后，需要在 Exchange Online PowerShell 中运行以下命令：

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 步骤 8：测试和解锁公用文件夹迁移

完成公用文件夹迁移之后，您应该运行以下测试，确保迁移成功。这样便能够在转而使用 Office 365 或 Exchange Online 公用文件夹之前测试迁移的公用文件夹层次结构。

1.  在 Office 365 或 Exchange Online PowerShell 中，指定一些测试邮箱将任何新迁移的公用文件夹邮箱用作默认公用文件夹邮箱。
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  使用之前步骤中确定的测试用户登录 Outlook 2007 或更新版本，然后执行以下公用文件夹测试：
    
      - 查看层次结构。
    
      - 检查权限。
    
      - 创建和删除公用文件夹。
    
      - 发布内容到公用文件夹并从公用文件夹删除内容。

3.  如果您遇到任何问题，请参阅本主题后面部分中的回滚迁移。如果公用文件夹内容和层次结构是可以接受的并且可以按照预期方式，则继续执行下一步。

4.  在旧版 Exchange 服务器中，运行以下命令，以指示公用文件夹迁移已完成：
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  确认迁移完成后，在 Exchange Online PowerShell 中的命令行管理程序中运行以下命令，确保 **Set-OrganizationConfig** 上的 *PublicFoldersEnabled* 参数设置为 `Local`：
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

有关语法和参数的详细信息，请参阅下列主题：

[Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\))

## 我如何知道这有效？

在Step 2: Prepare for the migration中，会指导您在迁移开始之前获取公用文件夹结构、统计信息和权限的快照。以下步骤将帮助您通过在迁移完成后获取这些相同的快照，验证公用文件夹迁移是否成功。然后，您可以比较这两个文件中的数据以验证是否成功。

1.  在 Exchange Online PowerShell 中，运行以下命令以获取新文件夹结构的快照。
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  在 Exchange Online PowerShell 中，运行以下命令以获取公用文件夹统计信息（如项目计数、大小和所有者）的快照。
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  在 Exchange Online PowerShell 中，运行以下命令以获取权限的快照。
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## 从旧版 Exchange 服务器中删除公用文件夹数据库

在迁移完成且您已验证 Exchange Online 公用文件夹可按预期方式工作后，您应该删除旧版 Exchange 服务器中的公用文件夹数据库。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因为你的所有邮箱在公用文件夹迁移前已被迁移至 Office 365，所以我们强烈建议你通过 Office 365（分散式邮件流）而非你本地环境的集中式邮件流传送流量。如果选择保持集中式邮件流，则可能导致公用文件夹的传送问题，因为你已从你的本地组织中删除公用文件夹邮箱数据库。</td>
</tr>
</tbody>
</table>


  - 若要详细了解如何从 Exchange 2007 服务器中删除公用文件夹数据库，请参阅[删除公用文件夹数据库](https://go.microsoft.com/fwlink/?linkid=123678)。

  - 若要详细了解如何从 Exchange 2010 服务器中删除公用文件夹数据库，请参阅[删除公用文件夹数据库](https://go.microsoft.com/fwlink/?linkid=81409)。

## 回滚迁移

如果在迁移过程中遇到问题，并且需要重新激活旧版 Exchange 公用文件夹，请执行以下步骤。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您将迁移回滚到旧版 Exchange 服务器，将丢失发送到已启用邮箱的公用文件夹中的任何电子邮件或迁移后投递到公用文件夹的内容。为保存此内容，需将公用文件夹内容导出到 .pst 文件，然后在回滚完成时将它导入到旧版公用文件夹。</td>
</tr>
</tbody>
</table>


1.  在旧版 Exchange 服务器中，运行以下命令解锁旧版 Exchange 公用文件夹。此进程可能需要几个小时。
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  在 Exchange Online PowerShell 中，运行以下命令以删除所有 Exchange Online 公用文件夹。
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  在旧版 Exchange 服务器中，运行以下命令，将 `PublicFolderMigrationComplete` 标志设置为 `$false`。
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## 使用 Outlook PST 导出将公用文件夹迁移至 Office 365

如果您的内部部署公用文件夹层次结构大于 30 GB，我们建议您不要使用 Outlook PST 导出功能将公用文件夹迁移到 Office 365 或 Exchange Online。Office 365 Online 公用文件夹邮箱增长使用自动拆分功能进行管理，此功能可在公用文件夹邮箱超过大小配额时对其进行拆分。当您使用 PST 导出功能迁移公用文件夹时，自动拆分无法应对公用文件夹邮箱的突然增长，您可能必须至少等待两星期，自动拆分才会将数据从主邮箱中移出。此外，在使用 Outlook PST 将公用文件夹导出到 Office 365 或 Exchange Online 之前，请考虑以下事项：

  - 在此过程中，公用文件夹权限将会丢失。在迁移之前捕获当前权限，并在迁移完成后手动将其添加回去。

  - 如果您使用复杂权限或有很多文件夹要迁移，我们建议使用 cmdlet 方法进行迁移。

  - PST 导出迁移期间对源公用文件夹所做的任何项目和文件夹更改都将丢失。因此，如果此导出和导入过程需要很长一段时间才能完成，我们建议您使用 cmdlet 方法。

如果您还是想使用 PST 文件迁移公用文件夹，请按照以下步骤操作，以确保迁移成功。

1.  使用Step 1: Download the migration scripts中的说明下载迁移脚本。您只需下载 `PublicFolderToMailboxMapGenerator.ps1` 文件。

2.  按照Step 3: Generate the .csv files中的步骤 2 来创建公用文件夹到邮箱的映射文件。此文件用于计算 Exchange Online 中公用文件夹邮箱的正确数量。

3.  创建所需的公用文件夹邮箱，具体取决于映射文件。有关详细信息，请参阅[创建公用文件夹邮箱](create-a-public-folder-mailbox-exchange-2013-help.md)。

4.  使用 New-PublicFolder cmdlet 可以利用 *Mailbox* 参数在每个公用文件夹邮箱中创建顶级公用文件夹。

5.  使用 Outlook 导出和导入 PST 文件。

6.  使用 EAC 设置公用文件夹的权限。有关详细信息，请遵循[设置新组织中的公用文件夹](set-up-public-folders-in-a-new-organization-exchange-2013-help.md)主题中的[Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md)。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您已经启动 PST 迁移并且遇到主邮箱已满的问题，您有两个选择来恢复 PST 迁移：
<ol>
<li><p>等待自动拆分将数据从主邮箱中移出。此过程可能最多需要两星期。但是，在自动拆分完成之前，全满公用文件夹邮箱中的所有公用文件夹都无法接收新内容。</p></li>
<li><p><a href="create-a-public-folder-mailbox-exchange-2013-help.md">创建公用文件夹邮箱</a>，然后使用 <strong>New-PublicFolder</strong> cmdlet 与 <em>Mailbox</em> 参数在辅助公用文件夹邮箱中创建其余的公用文件夹。本示例将在辅助公用文件夹邮箱中创建一个名为 PF201 的新公用文件夹。</p>
<pre><code>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</code></pre></li>
</ol></td>
</tr>
</tbody>
</table>


## 刚开始接触 Office 365？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="&amp;quot;领英学习&amp;quot;短图标" alt="&amp;quot;领英学习&amp;quot;短图标" /> <strong>刚开始接触 Office 365？</strong><br />
发现 LinkedIn Learning 向 <a href="https://support.office.com/zh-cn/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>提供的免费视频课程。</p></td>
</tr>
</tbody>
</table>

