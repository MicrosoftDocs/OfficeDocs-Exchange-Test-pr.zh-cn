---
title: '脱机通讯簿: Exchange 2013 Help'
TOCTitle: 脱机通讯簿
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 50491260
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 脱机通讯簿

 

_**适用于：** Exchange Server 2010, Exchange Server 2013_

_**上一次修改主题：** 2014-11-16_

脱机通讯簿 (OAB) 是已下载的地址列表集的副本，因此 Microsoft Outlook 用户可以在与服务器断开连接的情况下访问通讯簿。Microsoft Exchange 生成新的 OAB 文件，然后压缩文件并将其置于本地共享。可以决定脱机工作的用户可以使用哪些地址列表，也可以配置分发通讯簿的方式。

有关地址列表的详细信息，请参阅[地址列表](address-lists-exchange-2013-help.md)。

> [!important]
> OAB 数据由 Microsoft Exchange OABGen 服务生成，该服务是邮箱助理。如果使用安全描述符来防止用户查看 Active Directory 中的某些收件人，则下载 OAB 的用户将能够看到这些隐藏的收件人。因此，若要隐藏地址列表的收件人，请设置 <a href="https://technet.microsoft.com/zh-cn/library/aa998596(v=exchg.150)">Set-PublicFolder</a>、<a href="https://technet.microsoft.com/zh-cn/library/aa995950(v=exchg.150)">Set-MailContact</a>、<a href="https://technet.microsoft.com/zh-cn/library/aa995971(v=exchg.150)">Set-MailUser</a>、<a href="https://technet.microsoft.com/zh-cn/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</a>、<a href="https://technet.microsoft.com/zh-cn/library/bb123981(v=exchg.150)">Set-Mailbox</a> 和 <a href="https://technet.microsoft.com/zh-cn/library/bb124955(v=exchg.150)">Set-DistributionGroup</a> cmdlet 的 <em>HiddenFromAddressListsEnabled</em> 参数。另外，可以新建不包含隐藏的收件人的默认 OAB。有关如何在 OAB 中添加或删除地址列表的详细信息，请参阅<a href="add-an-address-list-to-or-remove-an-address-list-from-an-offline-address-book-exchange-2013-help.md">将地址列表添加至脱机通讯簿或从脱机通讯簿删除地址列表</a>。


正在寻找与 OAB 相关的管理任务？请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

**内容**

在 Exchange 版本之间移动 OAB

OAB 版本 4 和 Outlook 客户端

基于 Web 的分发

OAB 注意事项

## 在 Exchange 版本之间移动 OAB

在 Exchange 2007 和 Exchange 2010 中，使用 **Move-OfflineAddressBook** cmdlet 将 OAB 生成移至另一个邮箱服务器。Exchange 2013 仅支持 OAB（版本 4）。这与 Exchange 2010 中默认的版本相同。不能配置 Exchange 2013 以生成其他 OAB 版本，并且 OAB 生成发生在组织邮箱所在的邮箱服务器上。而且，若要移动 Exchange 2013 中的 OAB 生成，则必须移动组织邮箱。只能将 OAB 生成移至另一个 Exchange 2013 邮箱数据库。不能将 OAB 生成移至 Exchange 的早期版本。若要查找 Exchange 2013 OAB 组织邮箱，请运行以下 Shell 命令：

    Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}

然后，使用 **MoveRequest** cmdlet 移动邮箱。

## OAB 版本 4 和 Outlook 客户端

Exchange 2013 只支持 OAB 版本 4。OAB 版本 4 包含在 Exchange 2003 Service Pack 2 (SP2) 中，并受 Outlook 2007、Outlook 2010 和 Outlook 2013 的支持。这个 Unicode OAB 允许客户端计算机接收差异更新，而不支持完整的 OAB 下载和减小的文件大小。

## 使用 OAB 版本 4 的 Outlook 客户端

对于 Outlook 2013、Outlook 2010、Outlook 2007 和使用 OAB 版本 4 的客户端，如果 changes.oab 文件的大小是整个 OAB 文件的一半（或更多），则 Outlook 启动完全 OAB 下载。

## 基于 Web 的分发

*基于 Web 的分发*是一种分发方法，通过此方法，脱机工作的 Outlook 2013、Outlook 2010、Outlook 2007 客户端可以访问 OAB。

使用基于 Web 的分发有以下几点优势，包括：

  - 支持更多并发客户端计算机。

  - 减少所用带宽。

  - 对 OAB 分发点拥有更多控制。对于基于 Web 的分发，分发点是客户端计算机可以下载 OAB 的 HTTPS Web 地址。

若要从基于 Web 的分发获得最多的好处，客户端计算机必须运行 Outlook 2013、Outlook 2010 或 Outlook 2007。

要使基于 Web 的分发功能正常工作，需要使用下列组件：

  - **OAB 生成过程**   这是 Exchange 创建和更新 OAB 的过程。若要创建和更新 OAB，请在组织邮箱所在的邮箱服务器上运行 OABGen 服务。若要支持 OAB 分发，此服务器必须是 Exchange 邮箱服务器。

  - **OAB 分发**   如果客户端启动 OAB 分发请求，则会通过客户端访问服务器传入该请求。然后，客户端访问服务器将该请求路由至托管 OAB 文件的邮箱服务器。接下来，OAB 文件直接从邮箱服务器分发给客户端。

  - **OAB 虚拟目录**   OAB 虚拟目录是基于 Web 的分发方法所使用的分发点。默认情况下，在安装 Exchange 时，将在 Internet Information Services (IIS) 的默认内部网站中新建一个名为 **OAB** 的虚拟目录。如果有从组织防火墙外部连接到 Outlook 的客户端用户，则可以添加外部网站。另外，在 Shell 中运行 **New-OABVirtualDirectory** cmdlet 时，将在本地 Exchange 客户端访问服务器的默认 IIS 网站中新建一个名为 OAB 的虚拟目录。有关详细信息，请参阅 [创建脱机通讯簿虚拟目录](create-an-offline-address-book-virtual-directory-exchange-2013-help.md)。

  - **自动发现服务**   此功能在 Outlook 2013、Outlook 2010、Outlook 2007 以及自动配置客户端以访问 Exchange 的一些移动设备中可用。此服务在客户端访问服务器上运行并针对特定的客户端连接返回正确的 OAB URL。

## OAB 注意事项

最佳做法是，无论使用单个 OAB 还是多个 OAB，在计划和实现 OAB 策略时请考虑下列因素：

  - 组织中的每个 OAB 的大小。有关详细信息，请参阅本主题后面部分中的 OAB 大小注意事项。

  - OAB 下载数量。

  - 父级可分辨名称更改的数量和频率。

  - SMTP 地址不匹配。

  - 对目录所做的更改总数。

## OAB 大小注意事项

对于某些组织来说，OAB 是远程用户偶尔下载的一个小文件。对于这些组织，下载 OAB 通常不是问题。但是，对于拥有大型目录的大型组织，或已在缓存的 Exchange 模式中部署 Outlook 2003 的组织，这可能是个问题，特别是那些将 Exchange 服务器合并到地区数据中心的组织。

OAB 大小可以在几兆字节到几百兆字节之间变化。下列因素可能影响 OAB 的大小：

  - 公司中证书的使用。公钥基础结构 (PKI) 证书越多，OAB 就越大。PKI 证书大小介于 1 千字节 (KB) 到 3 KB 之间。这些证书是影响 OAB 大小的一个最大因素。

  - Active Directory 中的邮件收件人的数量。

  - Active Directory 中的通讯组的数量。

  - 公司向每个已启用的邮箱或已启用邮件的对象的 Active Directory 所添加的信息。例如，有些组织会对每个用户填充地址属性，而其他组织则不会。

