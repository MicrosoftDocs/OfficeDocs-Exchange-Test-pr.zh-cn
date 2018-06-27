---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 50491014
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

Microsoft Exchange Server 2013 使用 Active Directory 存储以及与 Windows 共享目录信息。Exchange 2013 的 Active Directory 林设计类似于 Exchange Server 2010，但也有一些不同之处，下面将加以讨论。

## Active Directory 驱动程序

Active Directory 驱动程序是 Microsoft Exchange 的核心组件，它使 Exchange 服务可以创建、修改、删除和查询 Active Directory 域服务 (AD DS) 数据。在 Exchange 2013 中，所有对 Active Directory 的访问均使用 Active Directory 驱动程序本身完成。以前在 Exchange 2010 中，DSAccess 为 SMTP、邮件传输代理 (MTA) 和 Exchange 存储等组件提供了目录查询服务。

Active Directory 驱动程序还可利用 Microsoft ExchangeActive Directory Topology (MSExchangeADTopology)，该服务使 Active Directory 驱动程序可以使用目录服务访问 (DSAccess) 拓扑数据。这些数据包括可用的域控制器列表和可用于处理 Exchange 请求的全局编录服务器。有关 Active Directory 驱动程序的详细信息，请参阅 [Active Directory 域服务](https://go.microsoft.com/fwlink/p/?linkid=110942)。

## Active Directory 架构更改

Exchange 2013 向 Active Directory 域服务架构中添加了新的属性，并对现有的类和属性进行了其他修改。有关安装 Exchange 2013 时的 Active Directory 更改的详细信息，请参阅 [Exchange 2013 Active Directory 架构更改](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)。

## 详细信息

要进一步了解 Exchange 2013 如何在 Active Directory 中存储和检索信息以便规划对 Active Directory 的访问，请参阅[Active Directory 的访问权限](access-to-active-directory-exchange-2013-help.md)。

有关 Active Directory 林设计的详细信息，请参阅 [AD DS 设计指南](https://go.microsoft.com/fwlink/p/?linkid=264957)。

要了解有关计算机在 Active Directory 域中运行 Windows，以及在有脱节命名空间的域中部署 Exchange 2013 的详细信息，请参阅[非连续命名空间应用场景](disjoint-namespace-scenarios-exchange-2013-help.md)。

