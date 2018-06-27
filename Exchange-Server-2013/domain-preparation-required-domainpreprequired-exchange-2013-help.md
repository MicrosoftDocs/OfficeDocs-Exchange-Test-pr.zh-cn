---
title: '域准备 required_DomainPrepRequired: Exchange 2013 Help'
TOCTitle: 域准备 required_DomainPrepRequired
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 50491962
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 域准备 required\_DomainPrepRequired

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为安装服务器角色的尝试失败，所以 Microsoft Exchange Server 2007 安装程序无法继续进行。

Microsoft Exchange 安装程序要求在安装某些服务器角色之前为 Exchange Server 2007 准备本地域。

为 Exchange Server 2007 准备域包括下列任务：

  - 为 Exchange Servers、Exchange Organization Administrators、Authenticated Users 和 Exchange Mailbox Administrators 设置对 Domain 容器权限。

  - 创建 Microsoft Exchange System Objects 容器（如果它不存在），并为 Exchange Servers、Exchange Organization Administrators 和 Authenticated Users 设置对此容器的权限。

  - 在当前域中新建一个名为 Exchange Install Domain Servers 的域全局组。

  - 将 Exchange Install Domain Servers 组添加到根域中的 Exchange Servers USG。

若要解决此问题，请运行 **setup /PrepareDomain** 以准备本地域并重新安装服务器角色。

有关如何执行 PrepareDomain 过程的详细信息，请参阅"如何到准备活动目录和域"([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453))。

