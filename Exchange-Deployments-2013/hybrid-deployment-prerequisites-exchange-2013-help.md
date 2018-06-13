---
title: '混合部署先决条件: Exchange 2013 Help'
TOCTitle: 混合部署先决条件
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 50492089
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合部署先决条件

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2017-07-25_

**摘要：**在设置混合部署之前，您的 Exchange 环境需要满足的要求。

在使用“混合配置”向导创建和配置混合部署之前，现有的内部部署 Exchange 组织必须满足特定的要求。如果不满足这些要求，将无法完成“混合配置”向导中的步骤，且无法配置内部部署 Exchange 组织与 Exchange Online 之间的混合部署。

## 混合部署的先决条件

配置混合部署必须满足以下先决条件：

  - **内部部署 Exchange 组织**   可为基于 Exchange 2007 或更高版本的内部部署组织配置混合部署。
    
    已安装在您的本地组织中的 Exchange 版本决定了您可以安装的混合部署版本。通常应该配置在您组织中支持的最新混合部署版本。例如，如果您的本地组织运行 Exchange 2007，则需配置基于 Exchange 2013 的混合部署。有关 Exchange Server 和 Office 365 企业混合部署兼容性的完整列表，请参阅下表。
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>内部部署环境</th>
    <th>基于 Exchange 2016 的混合部署</th>
    <th>基于 Exchange 2013 的混合部署</th>
    <th>基于 Exchange 2010 的混合部署</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>支持</p></td>
    <td><p>不支持</p></td>
    <td><p>不支持</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>支持</p></td>
    <td><p>支持</p></td>
    <td><p>不支持</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>支持</p></td>
    <td><p>支持</p></td>
    <td><p>支持</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>不支持</p></td>
    <td><p>支持</p></td>
    <td><p>支持</p></td>
    </tr>
    </tbody>
    </table>


  - **内部部署 Exchange 版本** 混合部署需要最新的累积更新或更新汇总，以便用于已安装在您本地组织中的 Exchange 版本。如果您无法安装最新的累积更新或更新汇总，则也支持前一版本。不支持更早的累积更新或更新汇总。
    
    例如，假设您已在您的本地组织中安装了 Exchange 2013 累积更新 8，则 Exchange 2013 的最新可用版本就是累积更新 10。为了保持在受支持的混合配置中，您需要将您的 Exchange 2013 服务器至少升级到累积更新 9。但是，我们强烈建议您升级到累积更新 10。
    
    累积更新和更新汇总按季度有规律地进行发布，因此，如果您定期需要额外一些时间来完成升级，那么让您的服务器始终使用最新的累积更新或更新汇总就可以使您拥有更多的灵活性。

  - **内部部署服务器角色** 需要在本地组织中安装的服务器角色取决于已经安装的 Exchange 版本。
    
      - **Exchange 2010** 至少有一台已安装邮箱服务器角色、集线器传输服务器角色和客户端访问服务器角色的服务器。虽然可以在单独的服务器上安装邮箱服务器角色、集线器传输服务器角色和客户端访问服务器角色，但我们强烈建议您在每台服务器上都安装所有角色，这样可以提供额外的可靠性和更好的性能。
    
      - **Exchange 2013** 至少有一台已安装邮箱服务器角色和客户端访问服务器角色的服务器。虽然可以在单独的服务器上安装邮箱服务器角色和客户端访问服务器角色，但我们强烈建议您在每台服务器上都安装这两种角色，这样可以提供额外的可靠性和更好的性能。
    
      - **Exchange 2016 及其较新的版本** 至少有一台已安装邮箱服务器角色的服务器。
    
    混合部署还支持运行边缘传输服务器角色的 Exchange 服务器。边缘传输服务器还需要更新到最新的累积更新或更新汇总，以便可以用于您已安装的 Exchange 版本。我们强烈建议您将边缘传输服务器部署在外围网络中。无法在外围网络中部署邮箱服务器和客户端访问服务器。

  - **Office 365**   混合部署在支持 Azure Active Directory 同步的所有 Office 365 计划中均受支持。所有 Office 365 Enterprise、Government、Academic 和 Midsize 计划都支持混合部署。Office 365 Business 和 Office 365 Home 计划不支持混合部署。
    
    详细了解如何[注册 Office 365](https://go.microsoft.com/fwlink/p/?linkid=203981)。

  - **自定义域** 注册您希望在 Office 365 的混合部署中使用的任何自定义域。您可以使用 Office 365 管理入口网站或选择在您的内部部署组织中配置 Active Directory 联合身份验证服务 (AD FS)。
    
    详细了解如何[将域添加到 Office 365](https://go.microsoft.com/fwlink/p/?linkid=229238)。

  - **Active Directory 同步**   部署 Azure Active Directory Connect 工具，以将 Active Directory 与您的内部部署组织同步。
    
    若要了解详细信息，请参阅 [Azure AD Connect 用户登录选项](http://go.microsoft.com/fwlink/p/?linkid=723514)。

  - **自动发现 DNS 记录**   为现有的 SMTP 域配置自动发现公用 DNS 记录以指向某个内部部署 Exchange 2013 客户端访问服务器。

  - **Exchange 管理中心 (EAC) 中的 Office 365 组织**   本地 EAC 中默认包含 Office 365 组织节点，但是您必须先使用 Office 365 管理员凭据将 EAC 连接到 Office 365 组织，然后才能使用“混合配置”向导。这还允许您通过一个管理控制台管理内部部署组织和 Exchange 联机组织。
    
    有关详细信息，请参阅[Exchange 混合部署中的混合管理](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md)。

  - 
    
    **证书**   安装 Exchange 服务并为其分配一个从受信任的公共证书颁发机构 (CA) 购买的有效数字证书。虽然自签名证书应用于带 Microsoft 联合网关的内部部署联合身份验证信任，但自签名证书不能用于混合部署中的 Exchange 服务。在混合部署中配置的 Exchange 服务器上的 Internet 信息服务 (IIS) 实例必须具有从受信任的 CA 购买的有效数字证书。此外，在公用 DNS 中指定的 EWS 外部 URL 和自动发现终结点必须列在证书的主题备用名称 (SAN) 中。安装在用于混合部署邮件传输的 Exchange 服务器上的证书必须使用相同的证书（即，由同一 CA 颁发并具有相同主题）。
    
    有关详细信息，请参阅 [混合部署的证书要求](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)。

  - **EdgeSync**   如果已在内部部署组织部署边缘传输服务器，同时希望为混合安全邮件传输配置边缘传输服务器，则必须在使用“混合配置”向导之前配置 EdgeSync。此外，每次向边缘传输服务器应用新的累积更新或更新汇总时，您都需要运行 EdgeSync。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>尽管 EdgeSync 是部署边缘传输服务器的要求，但是当为混合安全邮件传输配置边缘传输服务器时，还需要额外的手动传输配置设置。</td>
    </tr>
    </tbody>
    </table>
    
    有关详细信息，请参阅[混合部署中的边缘传输服务器](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md)。

  - **已启用统一消息 (UM) 的邮箱** 如果具有已启用 UM 的邮箱，并且希望将其移动到 Office 365，则除进行 Exchange 混合部署外，还需要完成以下操作。必须满足这些要求**才能**将任意已启用 UM 的邮箱移动到 Office 365。
    
      - 与本地电话服务系统 **或** 集成的 Lync Server 2010、Lync Server 2013、Skype for Business Server 2015 或更高版本
    
      - 与本地电话服务系统 集成的 Skype for Business Online
    
      - 传统的本地 PBX 或 IP-PBX 解决方案。
    
      - 在 Exchange Online 中创建的，镜像本地组织中 UM 邮箱策略名称的 UM 邮箱策略。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>可以将多个本地 UM 邮箱策略映射到 Exchange Online 中的一个 UM 邮箱策略中。如果要执行此操作，需要使用 Exchange 命令行管理程序，手动将每个本地 UM 邮箱策略映射到 Exchange Online 策略。</td>
        </tr>
        </tbody>
        </table>
    
    有关详细信息，请查看[与 UM 电话系统集成](https://technet.microsoft.com/zh-cn/library/jj673558\(v=exchg.150\))、[Exchange 2013 电话顾问](https://technet.microsoft.com/zh-cn/library/ee364753\(v=exchg.150\)) 和 [设置云 PBX 语音邮件](https://go.microsoft.com/fwlink/p/?linkid=826207)。

## 混合部署协议、端口和终结点

混合部署功能和组件要求特定传入协议、端口和连接终结点必须可供 Office 365 访问，这样才能正常运行。配置混合部署之前，请先确认本地网络和安全配置能否支持下表中的功能和组件。除了允许特定的入站协议、端口和终结点之外，网络上的计算机还需要能够访问 [Office 365 URL 和 IP 地址范围](https://go.microsoft.com/fwlink/?linkid=823100)中列出的 IP 地址和端口和 URL。


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>传输协议</th>
<th>较高级别的协议</th>
<th>功能/组件</th>
<th>本地终结点</th>
<th>本地路径</th>
<th>身份验证提供程序</th>
<th>授权方法</th>
<th>是否支持预身份验证？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25 (SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Office 365 和本地之间的邮件流</p></td>
<td><p>Exchange 2016 邮箱/边缘</p>
<p>Exchange 2013 CAS/EDGE</p>
<p>Exchange 2010 HUB/EDGE</p></td>
<td><p>不适用</p></td>
<td><p>不适用</p></td>
<td><p>基于证书</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>自动发现</p></td>
<td><p>自动发现</p></td>
<td><p>Exchange 2016 邮箱</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Azure AD 身份验证系统</p></td>
<td><p>WS-Security 身份验证</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>忙/闲、邮件提示、邮件跟踪</p></td>
<td><p>Exchange 2016 邮箱</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Azure AD 身份验证系统</p></td>
<td><p>WS-Security 身份验证</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>多邮箱搜索</p></td>
<td><p>Exchange 2016 邮箱</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>身份验证服务器</p></td>
<td><p>WS-Security 身份验证</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>邮箱迁移</p></td>
<td><p>Exchange 2016 邮箱</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>Basic</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>自动发现</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Exchange 2016 邮箱</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>身份验证服务器</p></td>
<td><p>WS-Security 身份验证</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>不适用</p></td>
<td><p>AD FS（包括在 Windows 中）</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 身份验证系统</p></td>
<td><p>根据配置而异。</p></td>
<td><p>双重</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>不适用</p></td>
<td><p>Azure Active Directory Connect 和 AD FS</p></td>
<td><p>Windows 2012 R2 服务器</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 身份验证系统</p></td>
<td><p>根据配置而异。</p></td>
<td><p>双重</p></td>
</tr>
</tbody>
</table>


## 推荐的工具和服务

除了前面介绍的必备先决条件外，在使用“混合配置”向导配置混合部署时，还可使用一些其他的工具和服务：

  - **Exchange Server 部署助理**   Exchange Server 部署助理是一款基于 Web 的免费工具，可帮助您在本地组织中部署 Exchange、在本地组织和 Office 365 之间配置混合部署，或完全迁移到 Office 365。该工具会询问您一组简单的问题，并根据您的回答创建一个自定义检查表，其中包含部署或配置 Exchange Server 的说明。部署助理可以准确提供您配置混合部署所需要的信息。
    
    详细了解 [Exchange Server 部署助理](https://technet.microsoft.com/exdeploy2013)。
    
     

  - **远程连接分析工具**   Microsoft 远程连接分析工具可以检查内部部署 Exchange 组织的外部连接，确保做好配置混合部署的准备。强烈建议在使用“混合配置”向导配置混合部署之前，使用远程连接分析工具检查内部部署组织。
    
    可在以下位置了解详细信息：[Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/)。
    
     

  - **单一登录**   单一登录使用户可以使用一个用户名和密码访问内部部署组织和 Exchange 联机组织。它向用户提供了一种熟悉的登录体验，并允许管理员使用内部部署 Active Directory 管理工具轻松控制 Exchange Online 组织邮箱的帐户策略。
    
    部署单一登录时有多个选项：密码同步和 Active Directory 联合身份验证服务。这两个选项均由 Azure Active Directory Connect 提供。密码同步使几乎任何组织（不论大小）都能轻松实现单一登录。由于这个原因，并且由于混合部署中的用户体验在启用单一登录后会得到极大的改善，因此我们强烈建议您实现单一登录。对于超大型组织，例如具有多个需要加入混合部署的 Active Directory 林的组织，需要 Active Directory 联合身份验证服务。
    
    有关详细信息，请参阅[混合部署中的单一登录](single-sign-on-with-hybrid-deployments-exchange-2013-help.md)。

