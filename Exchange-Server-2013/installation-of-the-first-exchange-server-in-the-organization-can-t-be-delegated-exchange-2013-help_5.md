---
title: 'Exchange server 在组织中的首次安装无法委派: Exchange 2013 Help'
TOCTitle: Exchange server 在组织中的首次安装无法委派
ms:assetid: 0f4c5b2f-85ae-4160-9a53-f4b890d8ccdb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.delegatedfrontendtransportfirstinstall(v=EXCHG.150)
ms:contentKeyID: 50490012
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange server 在组织中的首次安装无法委派

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2014-11-05_

Microsoft Exchange Server 2013 安装程序无法继续，因为登录的用户没有所需的帐户权限，无法在组织中安装第一个 Exchange 2013 服务器。

虽然 Exchange 2013 安装程序允许使用委派安装连续服务器角色，但是安装程序要求在组织中安装第一个 Exchange 2013 服务器时，所登录的用户是 Enterprise Admins Windows 安全组的成员。这是因为，Exchange 2013 安装程序会在安装期间在 Active Directory 的 Exchange 组织容器中创建和配置对象。

> [!NOTE]  
> 如果以前没有为 Exchange 2013 准备 Active Directory 架构，则所登录的用户必须是 Schema Admins Windows 安全组的成员。或者，Schema Admins Windows 组的其他成员用户也可以在安装 Exchange 2013 之前准备 Active Directory 架构。


若要解决此问题，请将已登录的用户添加为 Enterprise Admins 安全组的成员。或者，登录到属于 Enterprise Admins 安全组的帐户。然后再次运行 Exchange 2013 安装程序。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

