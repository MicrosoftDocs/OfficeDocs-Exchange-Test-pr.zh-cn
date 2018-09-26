---
title: '常见问题：公用文件夹: Exchange 2013 Help'
TOCTitle: 常见问题：公用文件夹
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 50490001
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 常见问题：公用文件夹

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-03-27_

本主题向您提供有关 Exchange Server 2013 中的公用文件夹的常见问题列表。有关公用文件夹的详细信息，请参阅[公用文件夹](public-folders-exchange-2013-help.md)。

是否有此处未回答的公用文件夹的相关问题？给我们发送电子邮件，地址是 [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com)。

## 有关公用文件夹迁移的常见问题

本部分包含公用文件夹迁移有关的常见问题。有关详细信息，请参阅[使用批处理迁移将公用文件夹从以前版本迁移到 Exchange 2013](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)、 [使用批处理迁移将旧版公用文件夹迁移到 Office 365 和 Exchange Online](https://technet.microsoft.com/zh-cn/library/dn874017(v=exchg.150))或[使用批处理迁移将 Exchange 2013 公用文件夹迁移到 Exchange Online](https://technet.microsoft.com/zh-cn/library/mt798260(v=exchg.150))。

## 受支持的公用文件夹迁移方案是什么？

下面的列表详细列出了将公用文件夹迁移到 Exchange 2013 或 Exchange Online 的可用选项。

  - Exchange 2007 公用文件夹（SP3 RU15 或更高版本）可以迁移到 Exchange 2013 或 Exchange Online。

  - Exchange 2010 公用文件夹（SP3 RU8 或更高版本）可以迁移到 Exchange 2013 或 Exchange Online。

  - Exchange 2013 公用文件夹 (CU15 或更高版本) 可以迁移到 Exchange 联机。

支持当前仅迁移到同一 Active Directory 目录林中的Exchange 2013 。我们将在将来支持跨目录林迁移。

## 迁移后，Exchange 2010 源服务器上的层次结构会发生什么情况？

在迁移的最终完成阶段，会对源服务器加锁，使用户无法访问该服务器。迁移完成后会继续加锁，以防止用户访问源公用文件夹。尽管您可以释放此锁，但不建议这么做，因为更改无法同步到 Exchange 2013。

## 迁移公用文件夹之后，现有公用文件夹规则将会发生什么？

公用文件夹规则将与数据一起迁移，并仍然是公用文件夹规则。它们不会转换为邮箱规则。

## 如果在生成初始 .csv 文件之后在源上执行层次结构更改，会发生什么情况？这些更改如何反映在目标上？

.csv 文件用于确定源层次结构和目标邮箱之间的映射。它只包含顶级文件夹。顶级文件夹下的子文件夹会自动迁移。因此，如果添加了新的子文件夹，则会在迁移过程中进行迁移。如果创建了新的顶级文件夹，则会在包含层次结构可写副本的邮箱中创建该文件夹。

## 在迁移到 Exchange 2013 公用文件夹期间，如果挂起和最终完成之间的时间很长，如何强制实施增量同步，以便用户可以在最终同步期间访问公用文件夹？

您可以通过运行以下命令行管理程序命令，在最终完成之前（锁定源之前）强制执行增量同步：

```powershell
Resume-PublicFolderMigrationRequest \PublicFolderMigration
```

有关语法和参数的详细信息，请参阅 [Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-cn/library/jj218689\(v=exchg.150\))。

## 对于地理位置发布的层次结构迁移，如何确保在最接近目标用户的位置中创建公用文件夹？

作为迁移过程的一部分，系统将生成 .csv 文件（通过使用 `publicfoldertomailboxmapgenerator.ps1` 脚本）。此文件包含新层次结构的文件夹到邮箱的映射。您可以使用此 .csv 文件在适当的地理位置创建公用文件夹邮箱并修改该文件，让必需文件夹位于适当的邮箱中以使其靠近目标用户。

可以通过运行位于目录 \<*Exchange 安装目录*\>\\V15\\Scripts 中的脚本 `AggregatePFData.ps1` 来生成输入 .csv 文件。脚本运行如下：

```powershell
    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>
```

## 是否会迁移现有的公用文件夹权限？

是，权限将自动在文件夹级别与数据一起迁移。您不必单独执行此步骤。

## 不使用公用文件夹吗？

不。公用文件夹非常适用于 Outlook 集成和简单共享方案，以及适用于允许大量受众访问相同数据。

## 哪些客户端支持公用文件夹？

Outlook 2007、Outlook 2010、 Outlook 2013 和 Outlook 2011 针对 Mac 用户可以访问公用文件夹。但是，邮箱位于 Exchange 2013 服务器上的用户无法从使用 Exchange Web Services (EWS) 的客户端（如 Mac 版 Outlook）连接至 Exchange 2007 和 Exchange 2010 公用文件夹。我们建议您将旧的公用文件夹迁移到 Exchange 2013 以维护这部分用户的访问权限。

## 客户端中是否存在限制？

支持 Outlook Web App，但是有限制条件。你可以添加和移除收藏的公用文件夹（如果是\&quot;邮件\&quot;、\&quot;公告\&quot;、\&quot;日历\&quot;和\&quot;联系人\&quot;公用文件夹），并执行项目级操作，比如创建、编辑、删除和回复公告。但是，你在 Outlook Web App 中不能执行以下操作：

  - 创建或删除公用文件夹

  - 拖放内容

  - 访问运行早期版本 Exchange 的服务器上的公用文件夹

> [!NOTE]  
> 在已启用邮件的公用文件夹中，您只能创建包含元素<strong>使用特定模板答复</strong>的公用文件夹规则。包含<strong>使用特定模板答复</strong>的预先存在的规则可能将继续在未启用邮件的公用文件夹上工作，但无法通过此模板元素在这些文件夹中创建新规则或编辑现有规则。


在混合方案中，跨内部公用文件夹不支持 Outlook 网页版和 Outlook 2011 for Mac。用户必须与公用文件夹处于相同位置才能通过 Outlook 2011 for Mac 或 Outlook 网页版对其访问。如果遵循[混合部署过程](https://technet.microsoft.com/zh-cn/library/jj200788\(v=exchg.150\).aspx)下的过程操作，且 Outlook 2016 for Mac 的 2016 年 4 月更新已安装在所有客户端上，则 Outlook 2016 for Mac 的用户可以在混合方案中访问公用文件夹。

## 如何在公用文件夹邮箱中存储大型层次结构？

有关公用文件夹存储限制的详细信息，请参阅[公用文件夹的限制](limits-for-public-folders-exchange-2013-help.md)。

## 如何查看层次结构公用文件夹邮箱？

运行以下命令：

```powershell
Get-OrganizationConfig | Format-List RootPublicFolderMailbox
```

有关详细的语法和参数信息，请参阅 [Get-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997571\(v=exchg.150\))。

## 如何使用 Exchange 命令行管理程序 cmdlet 为公用文件夹创建内容邮箱？

运行以下命令可创建第一个主层次结构公用文件夹邮箱和辅助层次结构邮箱。

```powershell
New-Mailbox -PublicFolder -Name <name of public folder>
```

有关详细信息，请参阅[创建公用文件夹](https://technet.microsoft.com/zh-cn/library/bb691104(v=exchg.150))。

## 在早期版本的 Exchange 中，可以通过一个选项指定每个邮箱数据库的公用文件夹数据库。在 Exchange 2013 中的工作方式如何？

Exchange 2013 中没有数据库级别的设置。Exchange 2013 的邮箱级别功能支持您指定公用文件夹邮箱，但在默认情况下，Exchange 将自动计算每个用户的层次结构邮箱。

## 如何在 Exchange 2013 中使用公用文件夹指标工具？

在 Exchange 2013 中，您可以使用 [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa998663\(v=exchg.150\)) 和 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-cn/library/ee332344\(v=exchg.150\)) cmdlet 来获取公用文件夹指标数据。这是 Exchange 2010 中的同一个解决方案，因此没有任何变化。公用文件夹不需要额外的报告加载项。

## 公用文件夹能否区分内部对公用文件夹的访问与第三方访问？

在 Exchange 2013 中，通过使用基于角色的访问控制 (RBAC) 管理公用文件夹权限。Exchange 2013 中不使用访问控制列表 (ACL)。您可以使用 [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa998663\(v=exchg.150\)) 和 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-cn/library/ee332344\(v=exchg.150\)) cmdlet 跟踪执行管理任务的帐户，并稍后相应地审核访问。有关 RBAC 的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 邮箱审核日志记录是否作用于公用文件夹？

否。此时不作用。

## 对公用文件夹的限制是什么？有哪些建议？

有关公用文件夹限制的详细信息，请参阅[公用文件夹的限制](limits-for-public-folders-exchange-2013-help.md)。

## 关于拆分公用文件夹邮箱有哪些建议？它们是否应位于同一数据库中？

在以前的 Exchange 版本中，您可以跨公用文件夹数据库拆分公用文件夹。您可以决定是将公用文件夹邮箱的内容拆分到相同邮箱数据库中的邮箱中，还是拆分到其他数据库中的邮箱中。通常，建议拆分到独立的数据库中，因为您需要平衡存储和 I\\O。

## 能否在公用文件夹中设置保留策略？

与早期版本的 Exchange 一样，您可以在项目中设置保留限制。有关详细信息，请参阅[公用文件夹的限制](limits-for-public-folders-exchange-2013-help.md)。

## 能否指定哪些用户可以使用特定的公用文件夹邮箱？

在 Exchange 2007 和 Exchange 2010 中，您可以指定哪些用户有权访问特定的公用文件夹。在 Exchange 2013 中，可以为每个用户设置默认公用文件夹邮箱。为此，需要运行带 *DefaultPublicFolderMailbox* 参数的 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet。

```powershell
Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"
```

## 如果主层次结构不可用，对用户有什么影响？

如果主层次结构公用文件夹邮箱不可用，用户可以查看公用文件夹，但无法写入。要防止层次结构不可用，建议在数据库可用性组 (DAG) 中包含您的公用文件夹。若要了解 DAG，请参阅[数据库可用性组 (DAG)](database-availability-groups-dags-exchange-2013-help.md)。

## 能否更改哪些公用文件夹邮箱是主层次结构邮箱？

不能。如果您尝试更改主层次结构邮箱，则会收到错误消息。

## 公用文件夹是否具有全文搜索功能？

是，Exchange 2013 中的公用文件夹具有全文搜索功能。但是，您无法跨多个公用文件夹进行搜索。

