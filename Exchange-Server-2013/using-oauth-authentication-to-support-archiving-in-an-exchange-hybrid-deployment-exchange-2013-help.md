---
title: '使用 OAuth 身份验证支持 Exchange 混合部署中的存档: Exchange 2013 Help'
TOCTitle: 使用 OAuth 身份验证支持 Exchange 混合部署中的存档
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62247384
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用 OAuth 身份验证支持 Exchange 混合部署中的存档

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

如果您位于 Exchange 2013 混合部署中并使用 Exchange Online Archiving (EOA) for Exchange Server，您必须在升级到 Exchange 2013 累积更新 5 (CU5) 之后在内部部署组织和 Exchange Online 组织之间配置 OAuth 身份验证。通过 EOA，可以对具有内部部署邮箱的用户使用基于云的存档。在此方案中，内部部署邮箱服务器上的邮件记录管理 (MRM) 助手将应用存档策略，并将邮件从用户邮箱自动移动到基于云的存档。在 Exchange 2013 CU5 中，它使用 OAuth 身份验证。

有关配置 OAuth 身份验证的分步说明，请参阅[配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)。

## 什么是 OAuth 身份验证？

OAuth 身份验证是允许应用程序互相进行身份验证的服务器间身份验证协议。使用 OAuth 身份验证，用户凭据和密码不会从一台计算机传递到另一台计算机。相反，身份验证和授权在安全令牌交换的基础上进行；这些令牌会授予在特定时间段内对一组特定资源的访问权限。

OAuth 身份验证通常涉及到三方：一台授权服务器和两个需要互相进行通信的领域。授权服务器（也称为安全令牌服务器）向需要通信的两个领域颁发安全令牌；这些令牌会确认来自一个领域的通信是否应受另一个领域信任。在本地 Exchange 组织或 Exchange Online 之间使用 OAuth 身份验证时，授权服务器的功能由 Office 365 组织中的 Azure Active Directory 访问控制服务 (ACS) 提供。例如，在跨界的电子数据展示搜索中，Azure Active Directory ACS 将发出令牌，以确认 Exchange 本地组织中的管理员或合规部主管可以访问 Exchange Online 组织中的邮箱，反之亦然。

## 将 OAuth 身份验证配置为支持存档

如上文所述，请参阅[配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)中的说明，将 OAuth 身份验证配置为支持 Exchange 混合部署中的存档。

如果未为 Exchange 混合部署配置 OAuth，则无法使用存档策略将内部部署组织中用户主邮箱的项目自动移动到 Exchange Online 中用户基于云的存档。

## 详细信息

  - 您还必须将 OAuth 身份验证配置为在单个电子数据展示搜索中执行内部部署邮箱和基于云的邮箱的跨内部部署电子数据展示搜索。请参阅[使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)。

  - 您还可以将 OAuth 身份验证配置为允许其他应用程序（例如 SharePoint 2013 和 Lync Server 2013）向 Exchange 2013 进行身份验证。有关详细信息，请参阅[配置采用 SharePoint 2013 和 Lync 2013 的 OAuth 身份验证](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)。

  - 您可以在 Exchange 2013 和 SharePoint 2013 之间配置服务器到服务器身份验证，以便管理员与合规部主管可以使用 SharePoint 2013 中的电子数据展示中心搜索 Exchange 2013 邮箱。有关详细信息，请参阅[针对 SharePoint eDiscovery 中心配置 Exchange](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。

  - 您可以使用 Exchange 2013 中的混合配置向导配置 Exchange 混合部署。有关定制的分步混合部署配置检查表，请参阅 [Exchange Server 部署助理](https://go.microsoft.com/fwlink/p/?linkid=277105)。

