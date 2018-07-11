---
title: '使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示: Exchange 2013 Help'
TOCTitle: 使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61297549
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

若要在 Exchange 2013 混合组织中成功执行跨界电子数据展示搜索，必须在 Exchange 本地组织和 Exchange Online 组织之间配置 OAuth（开放授权）身份验证，以便能够使用就地电子数据展示搜索本地和基于云的邮箱。OAuth 身份验证支持 Exchange 混合部署中的以下电子数据展示方案：

  - 在使用 Exchange Online Archiving 的内部部署邮箱中搜索基于云的存档邮箱。

  - 在同一个电子数据展示搜索中搜索内部部署邮箱和基于云的邮箱。

有关配置 OAuth 身份验证以支持电子数据展示的分步说明，请参阅[配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)。

## 什么是 OAuth 身份验证？

OAuth 身份验证是允许应用程序互相进行身份验证的服务器间身份验证协议。使用 OAuth 身份验证，用户凭据和密码不会从一台计算机传递到另一台计算机。相反，身份验证和授权在安全令牌交换的基础上进行；这些令牌会授予在特定时间段内对一组特定资源的访问权限。

OAuth 身份验证通常涉及到三方：一台授权服务器和两个需要互相进行通信的领域。授权服务器（也称为安全令牌服务器）向需要通信的两个领域颁发安全令牌；这些令牌会确认来自一个领域的通信是否应受另一个领域信任。当在内部部署 Exchange 组织和 Exchange Online 之间使用 OAuth 身份验证时，授权服务器的功能由 Office 365 组织中的 Microsoft Azure Active Directory 访问控制服务 (ACS) 提供。例如，在跨内部部署的电子数据展示搜索中，Azure ACS 将发出令牌，以确认 Exchange 内部部署组织中的管理员或合规部主管可以访问 Exchange Online 组织的邮箱，反之亦然。

## 混合部署中的电子数据展示方案

下表可识别需要 OAuth 身份验证的 Exchange 混合部署中的电子数据展示方案。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>电子数据展示方案</th>
<th>需要 OAuth 身份验证？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在从 Exchange 内部部署组织启动的相同电子数据展示搜索中，搜索 Exchange 内部部署邮箱和 Exchange Online 邮箱。例如，在单个电子数据展示搜索中搜索组织中的所有邮箱。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>在使用 Exchange Online Archiving 的 Exchange 内部部署邮箱中搜索基于云的存档邮箱。使用就地电子数据展示时，将搜索主要和存档邮箱。</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>在管理员或合规部主管从 Exchange 内部部署组织启动的电子数据展示搜索中，搜索 Exchange Online 邮箱。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>使用管理员或合规部主管从 Exchange 内部部署组织启动的电子数据展示搜索，搜索内部部署邮箱。</p></td>
<td><p>否</p>

> [!NOTE]
> 如上文所述，如果内部部署邮箱与基于云的存档邮箱一起配置，则都需要 OAuth 身份验证。

</td>
</tr>
<tr class="odd">
<td><p>在登录到 Office 365 用户帐户的 Office 365 租户管理员或合规部主管从 Exchange Online 或从 SharePoint Online 电子数据展示中心启动的电子数据展示搜索中，搜索 Exchange Online 邮箱。</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 将 OAuth 身份验证配置为支持电子数据展示

如上文所述，请参阅[配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)中的说明，将 OAuth 身份验证配置为支持 Exchange 混合部署中的电子数据展示。

如果没有为 Exchange 混合部署配置 OAuth，则无法使用电子数据展示来搜索同一电子数据展示搜索中的 Exchange 内部部署和 Exchange Online 邮箱。您必须在从内部部署组织启动的电子数据展示搜索中搜索内部部署邮箱。同样，您只能在从 Exchange Online 组织启动的电子数据展示搜索中，或者使用 SharePoint Online 中的电子数据展示中心搜索 Exchange Online 邮箱。此外，如果相应的存档邮箱位于 Exchange Online 或 Exchange Online Archiving 组织中，您将无法搜索主要的内部部署邮箱。

## 详细信息

  - 您还可以使用 OAuth 身份验证允许其他应用程序（例如 SharePoint 2013 和 Lync Server 2013）向 Exchange 2013 进行身份验证。有关详细信息，请参阅[配置采用 SharePoint 2013 和 Lync 2013 的 OAuth 身份验证](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)。

  - 您可以在 Exchange 2013 和 SharePoint 2013 之间配置服务器到服务器身份验证，以便管理员与合规部主管可以使用 SharePoint 2013 中的电子数据展示中心搜索 Exchange 2013 邮箱。有关详细信息，请参阅[针对 SharePoint eDiscovery 中心配置 Exchange](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。

  - 您可以使用 Exchange 2013 中的混合配置向导配置 Exchange 混合部署。有关定制的分步混合部署配置检查表，请参阅 [Exchange Server 部署助理](https://go.microsoft.com/fwlink/p/?linkid=277105)。

