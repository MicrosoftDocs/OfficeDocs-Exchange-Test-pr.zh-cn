---
title: 'Exchange 2013 中的邮箱移动: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的邮箱移动
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 50491222
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的邮箱移动

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

移动邮箱时，它将从*源邮箱数据库*移动到*目标邮箱数据库*。目标邮箱数据库可以位于不同的 Active Directory 站点中不同域的相同服务器或不同服务器上，还可以位于另一个林中。

## 移动邮箱的原因

您可能需要在以下方案中移动邮箱：

  - **升级**   当您将现有的 Exchange Server 2010 或 Exchange Server 2007 组织升级为 Exchange Server 2013 时，需要将邮箱从现有的 Exchange 服务器移动到 Exchange 2013 邮箱服务器。

  - **重新调整**   可以移动邮箱以进行重新调整。例如，可能需要将邮箱从一个数据库移动到邮箱大小限制更大的数据库。

  - **调查问题**   如果需要调查邮箱的问题，可以将该邮箱移动到其他服务器。例如，可以将活动多的所有邮箱移动到另一台服务器。

  - **损坏的邮箱**   如果遇到损坏的邮箱，则可以将其移动到其他服务器或数据库。已损坏的邮件将不会移动。

  - **物理位置更改**   可以将邮箱移动到其他 Active Directory 站点中的服务器。例如，如果用户搬到其他物理位置，则可以将该用户的邮箱移动到距离新位置更近的服务器。

  - **分离管理角色**   您可能需要将 Exchange 管理与 Windows 操作系统帐户管理分开。为此，可以将邮箱从单个林移动到资源林方案。在此方案中，Exchange 邮箱驻留在一个林中，其关联的 Windows 用户帐户驻留在独立的林中。

  - **外包电子邮件管理**   您可能需要外包电子邮件的管理，并保留 Windows 用户帐户的管理。为此，可以将邮箱从单个林移动到资源林方案。

  - **将电子邮件管理和用户帐户管理集成在一起**   您可能需要从分离的或外包的电子邮件管理模型改为可以在同一个林中管理电子邮件和用户帐户的模型。为此，可以将邮箱从资源林方案移动到一个林。在此方案中，Exchange 邮箱和 Windows 用户帐户驻留在同一个林中。

## Exchange 2013 移动

Microsoft Exchange Server 2013 引入了*批处理移动*和*迁移端点*的概念。迁移端点是管理对象，介绍可以与一个或多个批次关联的远程服务器和连接。而且，新的批处理移动体系结构改进了 MRS（邮箱复制服务）移动，具有增强的管理功能。Exchange 2013 中的批处理移动体系结构具有以下功能：

  - 能够采用大型批次移动多个邮箱。

  - 在移动过程中发送电子邮件通知（包含报告）。

  - 移动的自动重试和自动优先级设置。

  - 主存档和个人存档邮箱可以一起或单独移动。

  - 用于手动移动请求完成的选项，使您可以检查移动的完成情况。

  - 用于更新迁移更改的定期增量同步。

在 Exchange 2013 中，必须使用 Exchange 2013 管理中心 (EAC) 和 Exchange 命令行管理程序在 Exchange 2007、Exchange 2010 和 Exchange 2013 之间移动邮箱。

> [!NOTE]
> 通过使用 EAC 或者移动请求或迁移批处理 cmdlet，您还可以在 Exchange 2013 中执行单个邮箱移动，类似于 Exchange Server 2010。


> [!NOTE]
> 不能将内部部署邮箱从 Exchange Server 2003 移动到 Exchange 2013。


有关管理新的和现有移动的详细信息，请参阅[管理内部部署移动](manage-on-premises-moves-exchange-2013-help.md)。

## 迁移端点

迁移端点将捕获远程服务器信息并存留迁移数据和来源限制设置所需的凭据。也可使用迁移端点为远程和跨林移动配置设置。本地移动不需要使用终结点。（本地移动指在两个不同的内部部署 Exchange 数据库之间移动邮箱。）

以下列表显示支持迁移端点的移动类型：

  - **跨林移动**   在两个不同的内部部署 Exchange 林之间移动邮箱。跨林移动需要使用 Exchange RemoteMove 终结点。

  - **远程移动**   在混合部署中，远程移动涉及“加入”或“分离”迁移。远程移动需要使用 RemoteMove 终结点。“加入”将邮箱从内部部署 Exchange 组织移到 Microsoft Office 365 中的 Exchange Online，并使用 RemoteMove 终结点作为迁移批处理的源终结点。“分离”将邮箱从 Office 365 中的 Exchange Online 移到内部部署 Exchange 组织，并使用 Exchange RemoteMove 终结点作为迁移批处理的目标终结点。

下表显示了可以在 Exchange 2013 中管理的迁移端点类型和值。

### 迁移端点类型的值

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange RemoteMove</th>
<th>Exchange LocalMove</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Site</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>Databases</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Forest</p></td>
</tr>
</tbody>
</table>


有关迁移终结点的详细信息，请参阅 EAC 中的“迁移”用户界面和 [New-MigrationEndpoint](https://technet.microsoft.com/zh-cn/library/jj218611\(v=exchg.150\))。

有关管理新的和现有移动的详细信息，请参阅[管理内部部署移动](manage-on-premises-moves-exchange-2013-help.md)。

