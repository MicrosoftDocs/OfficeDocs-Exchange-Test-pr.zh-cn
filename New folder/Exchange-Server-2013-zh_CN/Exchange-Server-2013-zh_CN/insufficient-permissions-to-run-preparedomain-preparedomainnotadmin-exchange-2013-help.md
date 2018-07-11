---
title: '权限不足，无法运行 /PrepareDomain_PrepareDomainNotAdmin: Exchange 2013 Help'
TOCTitle: 权限不足，无法运行 /PrepareDomain_PrepareDomainNotAdmin
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 50491629
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 权限不足，无法运行 /PrepareDomain\_PrepareDomainNotAdmin

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007年安装程序无法继续，因为尝试运行**/PrepareDomain**进程失败。登录的用户没有足够的权限来执行**/PrepareDomain**过程。

Exchange 2007 安装程序要求运行 **/PrepareDomain** 进程时登录的用户是要准备的域的 Domain Admins 组成员，以及 Enterprise Admins 组的成员。

要解决此问题，请将所准备域的 Domain Admins 组权限授予已登录用户并在 Enterprise Admins 组中注册它们，或者使用拥有这些权限的帐户登录，然后重新运行 Exchange 2007 安装程序。

有关所需与 Microsoft Exchange Active Directory 权限的详细信息，请参阅"使用与活动目录的权限在 Exchange Server"([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))。

