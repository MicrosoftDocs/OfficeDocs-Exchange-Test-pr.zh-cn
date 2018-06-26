---
title: 'Exchange 2013/Exchange 2007 混合部署中的服务器角色: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2007 混合部署中的服务器角色
ms:assetid: d7104efe-6d2a-4260-bc4e-f05da477e30b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn151302(v=EXCHG.150)
ms:contentKeyID: 54652317
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2007 混合部署中的服务器角色

本主题正在进行。  

_<strong>适用于：</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>上一次修改主题：</strong>2016-12-09_

在 Exchange 2007 组织中配置了混合部署后，您需要在现有的 Exchange 2007 组织中至少安装一个具有客户端访问服务器角色和邮箱服务器角色的 Exchange 2013 服务器。Exchange 2013 客户端访问服务器和邮箱服务器协调现有的 Exchange 2007 内部部署组织和 Exchange Online 组织之间的通信。此通信包括内部部署组织与 Exchange Online 组织之间的邮件传输和消息功能。

我们强烈建议在内部部署组织中安装多个 Exchange 2013 服务器，以帮助提高混合部署功能的可靠性和可用性。

## 混合部署中的服务器角色

下面是混合部署中的 Exchange 2013 服务器角色的快速概述：

  - **客户端访问服务器角色**   Exchange 2013 客户端访问服务器角色继续提供许多由组织中的 Exchange 2007 客户端访问服务器提供的相同功能，外加支持混合部署和与 Exchange 2007 共存所需的一些其他功能。客户端访问服务器还处理由 Exchange Online 组织发送到内部部署组织的安全邮件，以及处理混合部署中的传输规则、日记策略和到邮箱服务器的邮件传递。默认情况下，在客户端访问服务器上配置有专门的接收连接器以支持安全混合邮件传输。所有客户端连接（包括 Outlook 客户端访问、Outlook Web App 和 Outlook Anywhere）都通过客户端访问服务器角色进行。内部部署组织与 Exchange Online 组织之间的组织关系功能（如忙/闲共享）也由客户端访问服务器角色处理。
    
    有关详细信息，请参阅[客户端访问服务器](https://technet.microsoft.com/zh-cn/library/dd298114\(v=exchg.150\))。

  - **邮箱服务器角色**   Exchange 2013 邮箱服务器角色处理从内部部署组织发送到 Exchange Online 组织中的安全邮件。尽管不典型，但它也可以托管内部部署收件人邮箱并与通过内部部署客户端访问服务器代理的 Exchange Online 组织通信。默认情况下，在邮箱服务器角色上配置有专门的发送连接器以支持安全混合邮件传输。
    
    有关详细信息，请参阅[邮箱服务器](https://technet.microsoft.com/zh-cn/library/jj150491\(v=exchg.150\))。

根据所需的混合部署配置，Exchange 2013 服务器需要安装一个或两个服务器角色：

  - **单个 Exchange 服务器**   如果选择在您的内部部署组织中安装单个 Exchange 服务器，则需要在该单个服务器上同时安装客户端访问和邮箱服务器角色。

  - **多个 Exchange 服务器**   如果选择在您的内部部署组织中安装多个 Exchange 服务器，则可在内部部署组织中的单独服务器上安装服务器角色。例如，可以安装一个安装了邮箱和客户端访问服务器角色的 Exchange 2013 服务器，同时也再安装一个仅安装了客户端访问服务器角色的 Exchange 服务器。但是，最佳实践及推荐的服务器配置是在内部部署组织中部署的“每个”Exchange 2013 服务器上同时安装客户端访问和邮箱服务器。

有关 Exchange 容量规则的详细信息，请参阅[了解容量规划中的多个服务器角色配置](http://go.microsoft.com/fwlink/?linkid=266576)。

## 混合部署中的 Exchange 服务器功能

Exchange 服务器为混合部署中的内部部署组织提供了几个重要功能：

  - **联合身份验证**   使用 Exchange 2013 服务器可以通过 Microsoft 联合网关为内部部署组织创建联合身份验证信任。Microsoft 联合网关是 Microsoft 提供的一项基于云的免费服务，该服务可充当内部部署组织与 Office 365 租户组织之间的信任代理。联合身份验证是关于在内部部署组织与 Exchange Online 组织之间创建组织关系的要求。
    
    有关详细信息，请参阅[联盟](https://technet.microsoft.com/zh-cn/library/dd335047\(v=exchg.150\))。

  - **组织关系**   具有客户端访问服务器角色的 Exchange 2013 服务器支持创建内部部署组织与 Exchange Online 组织之间的组织关系。混合部署中的许多其他服务（包括日历忙/闲信息共享、邮件跟踪以及内部部署组织与 Exchange Online 组织之间的邮箱移动）需要组织关系。
    
    有关详细信息，请参阅[共享](https://technet.microsoft.com/zh-cn/library/dd638083\(v=exchg.150\))。

  - **邮件传输**   具有客户端访问和邮箱服务器角色的 Exchange 2013 服务器负责混合部署中的邮件传输。通过使用发送和接收连接器，这些服务器可用作传入外部邮件的连接终结点，并提供到 Internet 和 Exchange Online 组织的出站邮件传递。
    
    有关详细信息，请参阅 [Exchange 2013/Exchange 2007 混合部署中的传输选项](transport-options-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md)。

  - **邮件传输安全**   具有客户端访问和邮箱服务器角色的 Exchange 2013 服务器可使用 Exchange 2013 中的域安全功能，帮助保护内部部署组织与 Exchange Online 组织之间的邮件通信安全。可以通过将相互传输层安全性身份验证和加密用于邮件通信，来增强安全。
    
    有关详细信息，请参阅[了解域安全性](http://go.microsoft.com/fwlink/p/?linkid=266581)。

  - **Outlook Web App**   具有客户端访问服务器角色的 Exchange 2013 服务器支持为与内部部署邮箱和 Exchange Online 的邮箱之间的外部连接配置单个 URL 终结点。对于内部部署邮箱，客户端访问服务器被配置为响应 Outlook Web App 请求。对于 Exchange Online 组织邮箱，客户端访问服务器被配置为自动显示到 Exchange Online 组织上的 Outlook Web App 终结点的链接。
    
    有关详细信息，请参阅 [Outlook Web App](https://technet.microsoft.com/zh-cn/library/jj657718\(v=exchg.150\))。

## Exchange 服务器拓扑

如果添加额外的 Exchange 2013 服务器来支持混合部署，则 Exchange 服务器的部署将与其他任何 Exchange 服务器部署到现有 Exchange 2007 组织的方式非常相似。为混合部署配置现有的内部部署 Exchange 2007 组织不需要任何特殊的 Exchange 服务器拓扑。但是必须在 Exchange 2007 服务器上安装 Exchange 2007 Service Pack 3 (SP3) 更新汇总 10 和 Exchange 2013 累积更新 1 (CU1) 或更高版本，以启用 Office 365 的兼容性和完全混合功能。

下表简要描述配置了混合部署后的服务更改。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服务</th>
<th>混合部署之前</th>
<th>混合部署之后</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮件传输（入站和出站）</p></td>
<td><p>Exchange 2007 客户端访问服务器</p></td>
<td><p>Office 365 包含 Exchange 2013 客户端访问服务器或 Exchange Online Protection (EOP)</p></td>
<td><p>域的 MX（邮件交换器）记录可以保留不变，或者更新为指向 EOP。</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App 公用 URL</p></td>
<td><p>Exchange 2007 客户端访问服务器</p></td>
<td><p>Exchange 2013 客户端访问服务器</p></td>
<td><p>Exchange 2013 客户端访问服务器代理内部部署邮箱到 Exchange 2007 客户端访问服务器的 Outlook Web App 请求。在 Outlook Web App Online 上托管邮箱的 Exchange 请求提供到 Exchange Online Outlook Web App URL 的链接。</p></td>
</tr>
</tbody>
</table>


## Exchange 服务器软件

Exchange 2013 CU1 或更高版本通过混合配置向导启用混合部署功能。在安装额外的 Exchange 2013 服务器时，可使用任何 Exchange 2013 CU1 或更高版本介质。

有关如何下载 Exchange 2013 最新版本的信息，请参阅 [Exchange 2013 更新](http://technet.microsoft.com/library/jj907309)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 Exchange 2013 或 2010 和 Office 365 配置混合部署时，需要对混合服务器授予许可。若要获取用于配置混合部署的免费 Exchange Server 产品密钥，请使用<a href="https://aka.ms/hybridkey">混合版产品密钥工具</a>。</td>
</tr>
</tbody>
</table>

