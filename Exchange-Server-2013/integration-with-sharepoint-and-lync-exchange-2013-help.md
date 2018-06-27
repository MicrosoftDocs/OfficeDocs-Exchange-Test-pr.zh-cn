---
title: '与 SharePoint 和 Lync 的集成: Exchange 2013 Help'
TOCTitle: 与 SharePoint 和 Lync 的集成
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 50489858
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 与 SharePoint 和 Lync 的集成

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

MicrosoftExchange Server 2013 包含许多与 Microsoft SharePoint 2013 和 Microsoft Lync 2013 集成的功能。这些产品结合使用时可提供一整套功能，以实现可能使用站点邮箱的企业电子数据展示和协作之类的方案。

## 存档、保留和电子数据展示

在大多数组织中，电子邮件和文档的存档、在为满足监管合规性和业务要求所需的持续时间内保留它们以及能够快速搜索它们以实现电子数据展示这几点至关重要。Exchange 2013、SharePoint 2013 和 Lync Server 2013 结合起来提供集成的存档、保留和电子数据展示功能，从而使您可以跨 Exchange 邮箱、SharePoint 文档和网站以及存档的 Lync 内容，就地保留重要数据。SharePoint 2013 中的电子数据展示中心允许授权发现管理员跨这些存储对内容执行电子数据展示搜索、预览搜索结果并导出数据以进行法律审查。

## 在 Exchange 2013 中存档 Archive Lync Server 2013 内容

在具有 Exchange 2013 的组织中部署了 Lync Server 2013 之后，便可以配置 Lync 以将即时消息和联机会议内容（如共享演示文稿或文档）存档在用户的 Exchange 2013 邮箱中。通过将 Lync 数据存档在 Exchange 2013 中可以对其应用保留策略。也可通过任何电子数据展示搜索找到存档的 Lync 内容。有关 Lync 存档以及如何部署它的详细信息，请参阅下列主题：

  - [规划存档](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [部署存档](https://go.microsoft.com/fwlink/p/?linkid=265006)

## 使用 SharePoint 2013 电子数据展示中心搜索 Exchange、SharePoint 和 Lync 数据

Exchange 2013 允许 SharePoint 2013 使用联合搜索 API 搜索 Exchange 邮箱内容。SharePoint 2013 提供了一个电子数据展示中心，使授权人员可以执行电子数据展示。Microsoft Search Foundation 提供了一个对 Exchange 2013 和 SharePoint 2013 公用的索引和搜索基础结构，使您可以在这两个应用程序间使用相同查询语法。这可确保在 SharePoint 2013 中执行的电子数据展示搜索返回的 Exchange 2013 内容与在 Exchange 2013 中使用就地电子数据展示执行的相同搜索相同。SharePoint 2013 电子数据展示中心还允许您导出电子数据展示搜索中返回的内容，包括将 Exchange 2013 内容导出到 PST 文件。

有关详细信息，请参阅下列主题：

  - [就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)

  - [就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md)

  - [在 SharePoint Server 2013 中配置电子数据展示](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [SharePoint Server 2013 中的电子数据展示的新增功能](https://go.microsoft.com/fwlink/?linkid=275091)

  - [针对 SharePoint eDiscovery 中心配置 Exchange](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## 站点邮箱

在许多组织中，信息驻留在两个不同的存储中（电子邮件在 Microsoft Exchange 中，而文档在 SharePoint 中），需要使用两个不同的接口来访问它们。这样便形成了脱节了用户体验并阻碍了高效协作。站点邮箱使用户可以将 Exchange 电子邮件与 SharePoint 文档结合在一起，从而高效地协作。对于用户，站点邮箱充当中心档案柜，提供了一个位置用于对只能由站点成员访问和编辑的项目电子邮件和文档进行归档。用户可以使用 Outlook 2013 中的站点邮箱轻松访问他们所关心的项目的电子邮件和文档。此外，还可以从本身的 SharePoint 站点直接访问同一个内容集。

在站点邮箱的覆盖范围内，内容保留在其所属的位置中。Exchange 存储电子邮件，为用户提供与用户自己的邮箱日常所使用的邮件视图一样的电子邮件会话邮件视图。SharePoint 会存储文档，从而可实现文档合著和版本控制。Exchange 从 SharePoint 中同步适量元数据用于创建 Outlook 中的文档视图（例如文档标题、上次修改日期、上次修改作者、大小）。

站点邮箱通过 SharePoint 2013 进行设置和管理。有关详细信息，请参阅下列主题：

  - [网站邮箱](site-mailboxes-exchange-2013-help.md)

  - [在 SharePoint Server 2013 中配置网站邮箱](https://go.microsoft.com/fwlink/p/?linkid=258264)

## 统一联系人存储

统一联系人存储 (UCS) 是一种跨 Microsoft Office 产品提供一致的联系人体验的功能。此功能使用户可以将所有联系人信息存储在其 Exchange 2013 邮箱中，以便可以跨 Lync、Exchange、Outlook 和 Outlook Web App 全局使用相同联系人信息。

在具有 Exchange 2013 的环境中安装了 Lync Server 2013，并且在这两者之间配置了服务器到服务器身份验证之后，用户便可以开始将现有联系人从 Lync Server 2013 迁移到 Exchange 2013。有关详细信息，请参阅[规划和部署统一联系人存储](https://go.microsoft.com/fwlink/p/?linkid=275092)。

## 用户照片

用户照片是这样一种功能：使您可以将高分辨率用户照片存储在可以通过客户端应用程序（包括 Outlook、Outlook Web App、SharePoint 2013、Lync 2013 和移动电子邮件客户端）访问的 Exchange 2013 中。Active Directory 中也会存储低分辨率照片。与统一联系人存储一样，用户照片使组织可以保持可通过客户端应用程序使用的一致的用户配置文件照片，而无需每个应用程序都具有自己的用户照片以及用于添加和管理照片的不同方式。用户可以使用 Outlook Web App、SharePoint 2013 或 Lync 2013 管理自己的照片。有关在 Outlook Web App 上管理照片的详细信息，请参阅[我的帐户](https://go.microsoft.com/fwlink/p/?linkid=269646)。

## Outlook Web App 中的 Lync 状态

在安装了 Lync Server 2013 的 Exchange 2013 环境中，可以配置它们以使用户可以在 Outlook Web App 中查看状态信息。用户可以在 Outlook Web App 的导航窗格中查看其即时消息联系人和组、从 Outlook Web App 响应或发起即时消息会话以及管理其即时消息联系人和组。

## OAuth 身份验证

Exchange 2013、SharePoint 2013 和 Lync Server 2013 通过将 OAuth 授权协议用于服务器到服务器身份验证来提供上述丰富的跨产品功能。使用相同身份验证协议使这些应用程序可以无缝且安全地进行相互身份验证。该身份验证机制支持将身份验证作为一个使用链接帐户和用户模拟的上下文的应用程序（其中是在用户上下文中进行访问请求）。

OAuth 是许多网站和 Web 服务使用的标准授权协议。它允许客户端访问资源服务器提供的资源，而不必提供用户名和密码。身份验证由资源所有者（由它向客户端提供访问令牌）所信任的授权服务器执行。令牌授予在指定时间段内对一组特定资源的访问权限。有关 Exchange 2013 的 OAuth 实现的详细信息，请参阅 [\[MS-XOAUTH\]：OAuth 2.0 授权协议扩展](https://go.microsoft.com/fwlink/p/?linkid=275093)。

**内部部署中的 OAuth**

在内部部署中，Exchange 2013、SharePoint 2013 和 Lync Server 2013 无需授权服务器来颁发令牌。所有这些应用程序都颁发自签名令牌来访问其他应用程序提供的资源。提供对资源的访问权限的应用程序（例如 Exchange 2013）必须信任调用应用程序提供的自签名令牌。通过为调用应用程序创建*合作伙伴应用程序*配置来建立信任，这包括调用应用程序的 ApplicationID、证书和 AuthMetadataUrl。Exchange 2013、SharePoint 2013 和 Lync Server 2013 会采用已知 URL 发布其身份验证元数据文档。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>服务器</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Exchange 2013 服务器身份验证证书**

Exchange 2013 安装程序会使用友好名称 Microsoft Exchange Server 身份验证证书来创建自签名证书。该证书会复制到 Exchange 2013 组织中的所有前端服务器。证书的指纹在 Exchange 2013 的授权配置中与其服务名称（表示内部部署 Exchange 2013 的已知 GUID）一起指定。Exchange 使用授权配置发布其身份验证元数据文档。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 创建的默认服务器身份验证证书有效期为五年。必须确保授权配置包含当前证书。</td>
</tr>
</tbody>
</table>


当 Exchange 2013 通过 Exchange Web 服务 (EWS) 从合作伙伴应用程序收到访问请求时，它会分析 https 请求的 `www-authenticate` 标头（其中包含调用服务器使用其私钥签名的访问令牌）。身份验证模块会使用合作伙伴应用程序配置验证访问令牌。随后基于向应用程序授予的 RBAC 权限来授予对资源的访问权限。如果访问令牌代表用户，则会检查向用户授予的 RBAC 权限。例如，如果用户使用 SharePoint 2013 中的电子数据展示中心执行电子数据展示搜索，则 Exchange 会检查用户是否为发现管理角色组的成员，或是否分配了邮箱搜索角色并且搜索的邮箱是否处于 RBAC 角色分配的作用域内。有关更多详细信息，请参阅[权限](permissions-exchange-2013-help.md)。

## 管理 OAuth 身份验证

在 Exchange 2013 中，存在两个您必须通过合作伙伴应用程序管理以用于进行 OAuth 身份验证的配置对象：

  - **AuthConfig**   AuthConfig 由 Exchange 2013 安装程序创建，用于发布身份验证元数据。除了在现有证书即将过期时配置新证书之外，无需管理身份验证配置。发生这种情况时，可以续订现有证书并在 AuthConfig 中将新证书配置为下一个证书（并配置其生效日期）。新证书会自动复制到组织中的其他 Exchange 2013，身份验证元数据文档会使用新证书的详细信息进行刷新，并且 AuthConfig 会在生效日期滚动到新证书。

  - **合作伙伴应用程序**   若要使合作伙伴应用程序可以从 Exchange 2013 请求访问令牌，必须创建合作伙伴应用程序配置。Exchange 2013 提供了 `Configure-EnterprisePartnerApplication.ps1` 脚本，使用该脚本可以快速且方便地创建合作伙伴应用程序配置并最大程度减少配置错误。有关详细信息，请参阅[配置采用 SharePoint 2013 和 Lync 2013 的 OAuth 身份验证](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)。

