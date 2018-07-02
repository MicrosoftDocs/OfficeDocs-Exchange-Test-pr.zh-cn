---
title: 'OAB 服务器已删除_OffLineABServerDeleted: Exchange 2013 Help'
TOCTitle: OAB 服务器已删除_OffLineABServerDeleted
ms:assetid: 38b5dacf-ef65-4b25-97f6-d8dec956d7d5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.offlineabserverdeleted(v=EXCHG.150)
ms:contentKeyID: 50490320
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# OAB 服务器已删除\_OffLineABServerDeleted

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安装程序因其安装客户端访问服务器角色的尝试失败，而无法继续运行。指定托管脱机通讯簿 (OAB) 的 Exchange 邮箱服务器已被删除。

Exchange 2007 安装程序要求存在有效的承载 OAB 生成的 Exchange 邮箱服务器，客户端访问服务器角色安装才能继续进行。

若要解决此问题，请将有效的 Exchange 邮箱服务器指定为 OAB 生成主机，再重新运行 Exchange 2007 安装程序。

有关如何指定要作为脱机通讯簿生成宿主的 Exchange 服务器的信息，请参阅 Exchange 2007 产品文档中的"如何创建脱机通讯簿"([https://go.microsoft.com/fwlink/?LinkId=86314](https://go.microsoft.com/fwlink/?linkid=86314))。

