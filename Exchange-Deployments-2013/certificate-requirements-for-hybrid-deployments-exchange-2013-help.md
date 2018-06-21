---
title: '混合部署的证书要求: Exchange 2013 Help'
TOCTitle: 混合部署的证书要求
ms:assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh563848(v=EXCHG.150)
ms:contentKeyID: 50492075
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合部署的证书要求

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-12-09_

在混合部署中，数字证书是保护内部部署 Exchange 组织和 Office 365 之间通信的重要部分。证书允许每个 Exchange 组织信任另一个组织的身份。证书还有助确保每个 Exchange 组织与正确的源通信。

在混合部署中，许多服务都使用证书：

  - **Azure Active Directory Connect (Azure AD Connect) 和 Active Directory 联合身份验证服务 (AD FS)**   如果选择作为混合部署的一部分而部署 Azure AD Connect 和 AD FS，那么使用受信任的第三方证书颁发机构 (CA) 颁发的证书在 Web 客户端与联合服务器代理之间建立信任，以对安全令牌进行签名并对安全令牌进行解密。
    
    有关更多信息，请参阅[证书](http://go.microsoft.com/fwlink/p/?linkid=205993)。

  - **Exchange 联合身份验证**   自签名证书用于在本地 Exchange 服务器和 Azure Active Directory 身份验证系统之间创建安全连接。
    
    有关详细信息，请参阅 [共享](https://technet.microsoft.com/zh-cn/library/dd638083\(v=exchg.150\))。

  - **Exchange 服务**   受信任第三方 CA 颁发的证书用于帮助保护 Exchange 服务器与客户端之间的安全套接字层 (SSL) 通信的安全。使用证书的服务包括 Web 上的 Outlook、Exchange ActiveSync、Outlook Anywhere 和安全邮件传输。

  - **现有 Exchange 服务器** 现有的 Exchange 服务器可利用证书帮助保护 Web 上的 Outlook 通信、邮件传输等的安全。根据在 Exchange 服务器上使用证书的方式，可以使用自签名证书或受信任第三方 CA 颁发的证书。

## 混合部署的证书要求

当配置混合部署时，您必须使用和配置从受信任的第三方 CA 购买的证书。必须在所有内部部署邮箱（Exchange 2016 及更高版本）、邮箱和客户端访问（Exchange 2013 及之前版本）服务器上安装用于混合安全邮件传输的证书。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果在多个 Active Directory 林中都部署了 Exchange 服务器的组织中配置混合部署，必须对<em>每个</em> Active Directory 林使用单独的第三方 CA 证书。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当在本地组织中部署 Exchange 边缘传输服务器时，此证书还必须安装在所有边缘传输服务器上。每个传输服务器必须使用共享相同颁发 CA 和相同主题的证书，以便混合安全邮件正常运行。</td>
</tr>
</tbody>
</table>


多种服务，如 AD FS、Exchange联合身份验证、服务和Exchange，各自都需要证书。根据组织，可以决定执行以下操作之一：

  - 跨多个服务器使用由所有服务使用的第三方证书。

  - 对提供服务的每部服务器使用第三方证书。

是选择对所有服务使用相同证书还是对每种服务使用专用证书，取决于您的组织和要实现的服务。下面是针对每个选项需要考虑的一些事项：

  - **跨多个服务器的第三方证书**   跨多个服务器的服务使用的第三方证书的获取费用可能稍低一些，但是其续订和替换可能比较复杂。出现这种复杂性是因为：当证书需要替换时，您需要在安装证书的每部服务器上都替换证书。

  - **每个服务器的第三方证书**   通过对承载服务的每个服务器都使用专用证书，可以为该服务器上的服务专门配置证书。如果需要替换证书或续订证书，则只需在安装服务的服务器上进行替换。其他服务器不会受到影响。

建议您对任何可选 AD FS 服务器使用专用第三方证书，对混合部署的 Exchange 服务使用另一个证书，并对其他所需服务或功能的 Exchange 服务器使用另一个证书（如果需要）。默认情况下，在混合部署联合共享中配置的内部部署联合信任使用自签名证书。除非您有特定要求，否则无需对混合部署中配置的联合身份验证信任使用第三方证书。

安装在单个服务器上的服务可能需要您为该服务器配置多个完全限定域名 (FQDN)。应该购买允许使用最大所需 FQDN 数目的证书。证书包含主题（也称为主体名称）以及一个或多个主题备用名称 (SAN)。主题名称是向其颁发证书的 FQDN，并应该使用在内部部署与 Exchange Online 组织之间共享的主 SMTP 域。SAN 是除了主题名称之外，可以添加到证书的其他 FQDN。如果需要证书支持五个 FQDN，请购买允许向证书添加五个域的证书：一个主题名称和四个 SAN。

下表概括了在混合部署中使用的配置证书应包括的最小建议 FQDN。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>服务</th>
<th>建议的 FQDN</th>
<th>字段</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要共享 SMTP 域</p></td>
<td><p>contoso.com</p></td>
<td><p>使用者名称</p></td>
</tr>
<tr class="even">
<td><p>自动发现</p></td>
<td><p>与 Exchange 2013 客户端访问服务器的外部自动发现 FQDN 相匹配的标签，如 autodiscover.contoso.com</p></td>
<td><p>使用者替代名称</p></td>
</tr>
<tr class="odd">
<td><p>传输</p></td>
<td><p>与边缘传输服务器的外部 FQDN 匹配的标签，如 edge.contoso.com</p></td>
<td><p>使用者替代名称</p></td>
</tr>
</tbody>
</table>

