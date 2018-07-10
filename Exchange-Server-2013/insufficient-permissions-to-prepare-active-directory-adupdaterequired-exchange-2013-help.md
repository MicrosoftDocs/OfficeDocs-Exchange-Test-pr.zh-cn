---
title: '权限不足，无法准备 Active Directory_ADUpdateRequired: Exchange 2013 Help'
TOCTitle: 权限不足，无法准备 Active Directory_ADUpdateRequired
ms:assetid: 1412d8a1-605a-4b1e-bee3-0c97f2cc9e65
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.adupdaterequired(v=EXCHG.150)
ms:contentKeyID: 50490054
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 权限不足，无法准备 Active Directory\_ADUpdateRequired

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为尝试的域准备失败，所以 Microsoft Exchange Server 2007 安装程序无法继续进行。

Exchange 安装程序要求在准备 Active Directory 中的域之前修改 Exchange Server 2007 的 Active Directory 目录服务。

用于运行 **setup /PrepareAD** 命令的帐户没有足够的权限来执行此命令，即使它看起来属于企业管理员组，也是如此。此帐户可能已过期。

若要解决此问题，请验证已登录的用户帐户是否有效且属于 Enterprise Admins 组，或者使用拥有这些权限的帐户登录，然后重新运行 **setup /PrepareAD**。

有关如何执行 PrepareAD 过程的详细信息，请参阅"如何到准备活动目录和域"([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453))。

有关所需与 Microsoft Exchange Active Directory 权限的详细信息，请参阅"使用与活动目录的权限在 Exchange Server"([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))。

