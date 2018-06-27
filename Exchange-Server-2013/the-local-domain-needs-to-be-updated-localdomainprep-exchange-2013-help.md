---
title: '本地域需要 updated_LocalDomainPrep: Exchange 2013 Help'
TOCTitle: 本地域需要 updated_LocalDomainPrep
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 50491974
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 本地域需要 updated\_LocalDomainPrep

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为已登录用户没有域准备所需的帐户权限，所以 Microsoft Exchange Server 2007 安装程序无法继续进行。

Exchange 安装程序要求在运行 **Setup /PrepareDomain** 时登录的用户是 Domain Administrators 和 Exchange Organization Administrators 组或 Enterprise Admins 组的成员。

若要解决此问题，请向已登录的用户授予 Domain Admins 和 Exchange Organization Administrator 权限，在 Enterprise Admins 组中注册它们，或者使用拥有这些权限的帐户登录，并重新运行 Exchange 2007 安装程序。

有关所需与 Microsoft Exchange Active Directory 权限的详细信息，请参阅"使用与活动目录的权限在 Exchange Server"([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))。

