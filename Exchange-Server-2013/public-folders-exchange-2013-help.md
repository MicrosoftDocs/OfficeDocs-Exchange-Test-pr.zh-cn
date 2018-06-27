---
title: '公用文件夹: Exchange 2013 Help'
TOCTitle: 公用文件夹
ms:assetid: 94c4fb69-9234-4b34-8c1c-da2a0a11da65
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150538(v=EXCHG.150)
ms:contentKeyID: 50491193
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 公用文件夹

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2017-03-27_

公用文件夹专为共享访问设计，为收集、组织信息及与您的工作组或组织中的其他人共享信息提供了一种轻松、有效的方式。公用文件夹帮助以易于浏览的深层次结构组织内容。用户将在 Outlook 中看到完整层次结构，这便于他们浏览感兴趣的内容。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>公用文件夹在以下 Outlook 客户端中可用：适用于 Exchange 2013 的 Outlook Web App、Outlook 2007、Outlook 2010、Outlook 2013 和 Outlook for Mac。</td>
</tr>
</tbody>
</table>


公用文件夹还可以用作通讯组的存档方法。当为公用文件夹启用邮件并将其添加为通讯组成员时，发送到组的电子邮件将自动添加到公用文件夹以供以后参考。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必须使用 Outlook 2007 或更高版本访问 Exchange 2013 服务器上的公用文件夹。</td>
</tr>
</tbody>
</table>


公用文件夹不具有以下用途：

  - **数据存档**有邮箱限制的用户有时会使用公用文件夹而非邮箱来存档数据。建议不要采取该做法，因为这会影响公用文件夹中的存储量，并且削弱了邮箱限制的目标。替代方法是，建议使用[Exchange 2013 中的就地存档](in-place-archiving-in-exchange-2013-exchange-2013-help.md)作为存档解决方案。

  - **文档共享和协作：**公用文件夹不提供版本控制或其他文档管理功能，如受控的签入和签出功能以及自动通知内容变更。我们建议改用 [SharePoint](https://go.microsoft.com/fwlink/?linkid=282474) 作为文档共享解决方案。

要了解有关 Exchange 2013 中公用文件夹和其他协作方法的详细信息，请参阅[协作](collaboration-exchange-2013-help.md)。

要浏览一些有关 Exchange 2013 中的公用文件夹的常见问题，请参阅[常见问题：公用文件夹](faq-public-folders-exchange-2013-help.md)。

有关公用文件夹限制和配额的详细信息，请参阅[公用文件夹的限制](limits-for-public-folders-exchange-2013-help.md)。

有关公用文件夹管理任务的列表，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

是否在查找此主题的 Exchange Online 版本？请参阅 [Office 365 和 Exchange Online 中的公用文件夹](https://technet.microsoft.com/zh-cn/library/jj200758\(v=exchg.150\))。

**目录**

公用文件夹体系结构

迁移公用文件夹

公用文件夹移动

公用文件夹配额

灾难恢复

## 公用文件夹体系结构

在 Exchange 2013 中，使用邮箱基础结构对公用文件夹进行重新工程设计，以利用邮箱数据库的现有高可用性和存储技术。公用文件夹体系结构使用专门设计的邮箱来存储公用文件夹层次结构和内容。这也意味着公用文件夹数据库已不存在。公用文件夹邮箱的高可用性由数据库可用性组 (DAG) 提供。若要了解有关 DAG 的详细信息，请参阅[数据库可用性组 (DAG)](database-availability-groups-dags-exchange-2013-help.md)。

公用文件夹的主要体系结构组件是公用文件夹邮箱，它们可以驻留在一个或多个邮箱数据库中。

## 公用文件夹邮箱

有两种类型的公用文件夹邮箱：*主层次结构邮箱*和*辅助层次结构邮箱*。这两种邮箱都可以包含下列内容：

  - **主层次结构邮箱**   主层次结构邮箱是公用文件夹层次结构的一个可写副本。公用文件夹层次结构复制到所有其他公用文件夹邮箱，但是它们将是只读副本。

  - **辅助层次结构邮箱**   辅助层次结构邮箱也包含公用文件夹内容，以及公用文件夹层次结构的只读副本。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>公用文件夹邮箱不支持保留策略。</td>
</tr>
</tbody>
</table>


管理公用文件夹邮箱可采用以下两种方法：

  - 在 Exchange 管理中心 (EAC) 中，导航到“公用文件夹”\>“公用文件夹邮箱”。

  - 在 Exchange 命令行管理程序中，使用 **\*-Mailbox** cmdlet 集。为了支持公用文件夹邮箱，下列参数已添加到 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\)) cmdlet 中：
    
      - *PublicFolder*   此参数与 **New-Mailbox** cmdlet 一起用于创建公用文件夹邮箱。当创建公用文件夹邮箱时，使用 `PublicFolder` 邮箱类型来创建新邮箱。有关详细信息，请参阅 [创建公用文件夹邮箱](create-a-public-folder-mailbox-exchange-2013-help.md)。
    
      - *HoldForMigration*   只有当将公用文件夹从以前版本迁移到 Exchange 2013 时才使用此参数。有关详细信息，请参阅本主题后面的迁移公用文件夹。
    
      - *IsHierarchyReady*   此参数表示公用文件夹邮箱是否已准备好为用户提供公用文件夹层次结构服务。只有在整个层次结构都同步到公用文件夹邮箱后，才能将其设置为 `$True`。如果该参数设置为 $False，用户将不会使用它来访问层次结构。但是，如果您在用户邮箱上将 *DefaultPublicFolderMailbox* 属性设置为某个特定的公用文件夹邮箱，则即使将 *IsHierarchyReady* 参数设置为 `$False`，用户仍可访问指定的公用文件夹邮箱。
    
      - *IsExcludedFromServingHierarchy*   此参数可防止用户访问指定公用文件夹邮箱上的公用文件夹层次结构。默认情况下，为了负载平衡，用户均匀分布在公用文件夹邮箱之间。如果在某个公用文件夹邮箱上设置此参数，则此自动负载平衡将不包括此邮箱，并且用户不会访问此邮箱来检索公用文件夹层次结构。但是，如果您在用户邮箱上将 *DefaultPublicFolderMailbox* 属性设置为某个特定的公用文件夹邮箱，则用户仍可访问指定的公用文件夹邮箱，不管是否为该公用文件夹邮箱设置了 *IsExcludedFromServingHierarchy* 参数。

如果使用 *DefaultPublicFolderMailbox* 属性在用户邮箱上显式指定了辅助层次结构邮箱，或者如果满足以下条件，辅助层次结构邮箱将仅为用户提供公用文件夹层次结构信息：

  - 公用文件夹邮箱上的 *IsHierarchyReady* 属性设置为 `$True`。

  - 公用文件夹邮箱上的 *IsExcludedFromServingHierarchy* 属性设置为 `$False`。

## 公用文件夹层次结构

公用文件夹层次结构包含文件夹的属性和组织信息，包括树结构。每个公用文件夹邮箱都包含公用文件夹层次结构的副本。层次结构的唯一可写副本位于主公用文件夹邮箱中。对于特定文件夹，层次结构信息用于标识下列内容：

  - 文件夹上的权限

  - 文件夹在公用文件夹树中的位置（包括其父文件夹和子文件夹）

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>层次结构不存储有关已启用邮件公用文件夹的电子邮件地址的信息。电子邮件地址存储在 Active Directory 中的目录对象中。</td>
</tr>
</tbody>
</table>


## 层次结构同步

公用文件夹层次结构同步过程使用增量更改同步 (ICS)，它提供了监视机制并将更改与 Exchange 存储层次结构或内容同步。更改包括创建、修改和删除文件夹和邮件。当用户连接到并使用内容邮箱时，每 15 分钟发生一次同步。如果没有用户连接到内容邮箱，则触发同步的频率将下降（每 24 小时同步一次）。如果在主层次结构中执行写入操作（例如创建文件夹），则立即（同步）触发与内容邮箱的同步。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由于只有一个层次结构的可写副本，因此文件夹创建代理到内容邮箱用户连接的层次结构邮箱。</td>
</tr>
</tbody>
</table>


在大型组织中，当您创建新公用文件夹邮箱时，层次结构必须在用户连接到该公用文件夹之前与它同步。否则，用户在与 Outlook 连接时可能看到不完整的公用文件夹结构。要在用户未尝试连接到新公用文件夹邮箱的情况下允许一定时间让此同步发生，请在创建公用文件夹邮箱时在 **New-Mailbox** cmdlet 中设置 *IsExcludedFromServingHierarchy* 参数。此参数阻止用户连接到新创建的公用文件夹邮箱。当同步完成时，运行 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet，其中 *IsExcludedFromServingHierarchy* 参数设置为 `false` 以指示已可以连接到公用文件夹邮箱。还可以使用 [Get-PublicFolderMailboxDiagnostics](https://technet.microsoft.com/zh-cn/library/jj218720\(v=exchg.150\)) cmdlet 按 *SyncInfo* 和 *AssistantInfo* 属性查看同步状态。

有关详细信息，请参阅 [创建公用文件夹](create-a-public-folder-exchange-2013-help.md)。

## 公用文件夹内容

公用文件夹内容可以包括电子邮件、公告、文档和电子表格。内容存储在公用文件夹邮箱中，但是不跨多个公用文件夹邮箱复制。所有用户访问同一公用文件夹邮箱来获取同样的内容集。尽管提供了公用文件夹内容的全文搜索，当仍不能跨公用文件夹搜索公用文件夹内容，且 Exchange Search 不编制内容索引。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook Web App 受支持，但是有一定限制。可以添加和删除收藏夹文件夹，并执行项目级别操作，例如创建、编辑、删除公告和答复公告。但是，不能从 Outlook Web App 创建或删除公用文件夹。此外，在 Outlook Web App 中，您只能将“邮件”、“文章”、“日历”和“联系人”公用文件夹添加到收藏夹列表中。</td>
</tr>
</tbody>
</table>


## 迁移公用文件夹

可以将公共文件夹从以前版本的 Exchange Server 迁移至 Exchange 2013，或从以前版本的 Exchange Server 迁移至 Exchange Online。此外，可以将 Exchange 2013 公用文件夹迁移到 Exchange Online。

如果在安装 Exchange 2013 之前组织中已经有 Exchange 2010 SP3 或 Exchange 2007 SP3 RU10 公用文件夹，则必须将这些文件夹迁移到 Exchange 2013。为此，请使用 **PublicFolderMigrationRequst** cmdlet。有关详细信息，请参阅[使用批处理迁移将公用文件夹从以前版本迁移到 Exchange 2013](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)。如果你的组织正在移动到 Exchange Online，你可以将公用文件夹迁移到云，同时对它们进行升级。有关详细信息，请参阅[使用批处理迁移将旧版公用文件夹迁移到 Office 365 和 Exchange Online](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md) 和[使用批处理迁移将 Exchange 2013 公用文件夹迁移到 Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)。

由于公用文件夹的存储方式发生更改，因此旧版 Exchange 邮箱无法访问 Exchange 2013 服务器或 Exchange Online 上的公用文件夹层次结构。不过，Exchange 2013 服务器或 Exchange Online 上的用户邮箱可以连接到旧版公用文件夹。Exchange 2013 公用文件夹和旧版公用文件夹不能在 Exchange 组织中同时存在。这实际意味着版本间不能共存。将公用文件夹迁移到 Exchange Server 2013 或 Exchange Online 目前是一次性转换过程。

因此，我们建议你在迁移公用文件夹之前，应先将旧版邮箱迁移到 Exchange 2013 或 Exchange Online。若要详细了解如何迁移邮箱，请参阅 [Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)、[使用直接转换迁移将电子邮件迁移到 Office 365](https://go.microsoft.com/fwlink/p/?linkid=536689) 和[使用暂存迁移将电子邮件迁移到 Office 365](https://go.microsoft.com/fwlink/p/?linkid=536687)。

## 公用文件夹移动

可以将公用文件夹移动到不同的公用文件夹邮箱，且可以将公用文件夹邮箱移动到不同邮箱数据库。要将公用文件夹移动到不同公用文件夹邮箱，请使用 **PublicFolderMoveRequest** cmdlet 集。默认情况下，不会移动正在移动的公用文件夹下的子文件夹。如果希望移动公用文件夹的分支，可以使用 Exchange 2013 默认安装的 `Move-PublicFolderBranch.ps1` 脚本。有关详细信息，请参阅[将公用文件夹移动到不同的公用文件夹的邮箱](move-a-public-folder-to-a-different-public-folder-mailbox-exchange-2013-help.md)。

除了移动公用文件夹，还可以使用 **MoveRequest** cmdlet 集将公用文件夹邮箱移动到不同邮箱数据库。这与移动常规邮箱所使用的 cmdlet 集相同。有关详细信息，请参阅[将公用文件夹邮箱移动至不同的邮箱数据库中](move-a-public-folder-mailbox-to-a-different-mailbox-database-exchange-2013-help.md)。

**PublicFolderMoveRequest** cmdlet 和 **MoveRequest** cmdlet 使用邮箱复制服务异步移动公用文件夹。这意味着 cmdlet 不执行实际工作，在大部分移动中，公用文件夹和公用文件夹邮箱仍可供用户使用。由于邮箱复制服务执行邮箱移动、导入和导出请求和公用文件夹移动请求，因此有必要考虑限制和工作负载管理。

## 公用文件夹配额

当创建时，公用文件夹邮箱自动继承邮箱数据库默认设置的大小限制。因此，若要在使用 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) cmdlet 时准确评估当前存储配额状态，则除了 *ProhibitSendQuota*、*ProhibitSendReceiveQuota* 和 *IssueWarningQuota* 属性外，还必须查看 *UseDatabaseQuotaDefaults* 属性。如果 *UseDatabaseQuotaDefaults* 属性设置为 `true`，则忽略每个邮箱设置，而使用邮箱数据库限制。如果此属性设置为 `true` 而 *ProhibitSendQuota*、*ProhibitSendReceiveQuota* 和 *IssueWarningQuota* 属性设置为 `unlimited`，则实际上不限制邮箱大小。您必须转而使用 **Get-MailboxDatabase** cmdlet 并查看邮箱数据库存储限制，才能找到邮箱的限制。如果 *UseDatabaseQuotaDefaults* 属性设置为 `false`，则使用每个邮箱设置。在 Exchange 2013 中，默认邮箱数据库配额限制如下：

  - *发出警告配额*：1.9 GB

  - *禁止发送配额*：2 GB

  - *禁止接收配额*：2.3 GB

要找到邮箱数据库配额，请运行 [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\)) cmdlet。

要对公用文件夹邮箱设置配额，请使用 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\)) cmdlet。

## 灾难恢复

Exchange 2013 公用文件夹构建于邮箱基础结构上，使用相同的机制实现可用性和冗余。每个公用文件夹邮箱可以像常规邮箱一样，拥有多个带有自动故障转移功能的冗余副本。若要了解详细信息，请参阅[高可用性和站点恢复](high-availability-and-site-resilience-exchange-2013-help.md)。

除了整体灾难恢复方案，还可以在下列情况下还原公用文件夹：

  - **软删除公用文件夹还原**   公用文件夹已删除，但是仍在保留期内。

  - **软删除公用文件夹邮箱还原**   公用文件夹邮箱已删除，但是仍在邮箱保留期内。

  - **从恢复数据库还原公用文件夹邮箱**   可以在删除的邮箱保留期已过时，从备份恢复单个公用文件夹邮箱。然后，从已还原的邮箱中提取数据并将其复制到目标文件夹或与其他邮箱进行合并。

在所有这些情况中，都可使用 **MailboxRestoreRequest** cmdlet 恢复公用文件夹或公用文件夹邮箱。

有关详细信息，请参阅[恢复失败的移动公用文件夹和公用文件夹的邮箱](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)。

