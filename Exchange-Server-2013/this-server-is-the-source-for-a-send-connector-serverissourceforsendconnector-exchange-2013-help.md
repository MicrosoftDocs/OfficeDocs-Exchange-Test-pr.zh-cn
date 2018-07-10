---
title: '此服务器是发送连接器的源_ServerIsSourceForSendConnector: Exchange 2013 Help'
TOCTitle: 此服务器是发送连接器的源_ServerIsSourceForSendConnector
ms:assetid: 151c0014-c90c-4c52-8e74-4b3f1bc7aaf1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.serverissourceforsendconnector(v=EXCHG.150)
ms:contentKeyID: 50490059
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 此服务器是发送连接器的源\_ServerIsSourceForSendConnector

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安装程序因其删除集线器传输服务器角色的尝试失败，而无法继续运行。本地计算机是 Exchange 组织中一个或多个发送连接器的源。

发送连接器表示通过其发送出站邮件的逻辑网关。

Exchange 2007 安装程序要求在删除该服务器角色之前，从集线器传输服务器计算机中移动或删除 Exchange 组织的所有发送连接器。

若要解决此问题，请从本地计算机中移动或删除所有发送连接器，再重新运行安装程序。

有关修改或删除发送连接器的详细信息，请参阅 Exchange Server 2007 产品文档中的下列主题：

  - “如何删除发送连接器”([http://go.microsoft.com/fwlink/?LinkId=86655](https://go.microsoft.com/fwlink/?linkid=86655))。

  - “如何修改发送连接器配置”([https://go.microsoft.com/fwlink/?LinkId=86656](https://go.microsoft.com/fwlink/?linkid=86656))。

