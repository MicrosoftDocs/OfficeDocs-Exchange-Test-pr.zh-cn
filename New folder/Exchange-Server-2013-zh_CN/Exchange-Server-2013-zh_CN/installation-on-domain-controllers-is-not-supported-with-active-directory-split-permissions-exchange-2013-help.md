---
title: 'Active Directory 拆分权限不支持在域控制器上安装: Exchange 2013 Help'
TOCTitle: Active Directory 拆分权限不支持在域控制器上安装
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 50491206
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory 拆分权限不支持在域控制器上安装

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-11-12_

Microsoft Exchange Server 2013 安装程序检测到您试图在 Active Directory 域控制器上运行安装程序，并且存在以下情况之一：

  - 已经为 Exchange 组织配置了 Active Directory 拆分权限。

  - 您在 Exchange 2013 安装程序中选择了 Active Directory 拆分权限。

如果为 Exchange 组织配置了 Active Directory 拆分权限，则不支持在域控制器上安装 Exchange 2013。

如果要在域控制器上安装 Exchange 2013，必须为 Exchange 组织配置基于角色的访问控制 (RBAC) 拆分权限或共享权限。

> [!important]
> 我们建议不要在 Active Directory 域控制器上安装 Exchange 2013。 有关详细信息，请参阅<a href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">建议不要在域控制器上安装 Exchange</a>。


如果要继续使用 Active Directory 拆分权限，必须在成员服务器上安装 Exchange 2013。

有关 Exchange 2013 中的拆分权限和共享权限的详细信息，请参阅以下主题：

[了解拆分权限](understanding-split-permissions-exchange-2013-help.md)

[为 Exchange 2013 配置拆分权限](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[为 Exchange 2013 配置共享权限](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

