---
title: '使用混合配置向导创建混合部署: Exchange 2013 Help'
TOCTitle: 使用混合配置向导创建混合部署
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 50492080
ms.date: 03/15/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用混合配置向导创建混合部署

本主题正在进行。  

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-12-09_

通过建立混合部署，您可以将随其现有内部部署 Exchange Server 组织提供的功能丰富的体验和管理控制扩展到云。混合部署还使用 Exchange Online 存档，为内部部署邮箱的基于云的存档解决方案提供支持，同时还可作为完全迁移您的内部部署邮箱到 Exchange Online 的中间步骤。

本主题包括使用混合配置向导在面向企业的 Office 365 中为内部部署 Exchange 组织与 Exchange Online 组织配置混合部署。在本主题中，将为以下组织配置创建混合部署：

  - 内部部署组织为单林内部部署 Exchange 组织。

  - 内部部署组织不使用现有 Microsoft Exchange Online Protection (EOP) 服务用于内部部署保护。

  - 内部部署组织并不部署边缘传输服务器。作为混合部署的一部分，混合配置向导支持配置边缘传输服务器。但是本主题并不包括在向导中配置边缘传输服务器。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用混合配置向导配置混合部署要求某些重要的先决条件，这些先决条件有助于向导成功完成任务，以及有助于混合部署功能的正常工作。必须完成在 <a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署先决条件</a> 中概括的先决条件后，才可使用混合配置向导创建与配置混合部署。<br />
此外，<a href="http://technet.microsoft.com/exdeploy2013">Exchange Server 部署助理</a>是一款免费的 Web 工具，可帮助您在内部部署组织和 Office 365 之间配置混合部署，或完全迁移到 Office 365。该工具会询问您一些简单的问题，然后根据您的回答，创建一个自定义检查表，其中包含配置混合部署的说明。我们强烈建议您使用部署助理生成针对特定组织需求的自定义混合部署检查表。</td>
</tr>
</tbody>
</table>


关于混合部署的更多管理任务，参阅 [Hybrid Deployment procedures](hybrid-deployment-procedures-exchange-2013-help.md)。

有关混合部署的详细信息，请参阅 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。有关 Office 365 的更多信息，请参阅[什么是 Office 365？](http://go.microsoft.com/fwlink/?linkid=266712)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：30 分钟
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>该主题概述了完成混合配置向导步骤的估计完成时间。配置混合部署要求将会花费比估计完成时间长得多的时间。例如，注册企业 Office 365、配置 Active Directory 同步、分配 Exchange Online 许可证要求巨大的时间投资，并且可能也包括网络拓扑更改。考虑到完成端到端混合部署配置需要的整体时间，您应该计划出比所列的完成该步骤需要的时间更长的时间。</td>
    </tr>
    </tbody>
    </table>


  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](https://technet.microsoft.com/zh-cn/library/dd638114\(v=exchg.150\))主题中的“混合部署”条目。

  - 您需要通过运行且版本受支持的最新 Exchange 发行版的计算机运行混合配置向导。配置 Exchange OAuth 身份验证的混合配置向导中的最后步骤要求从内部部署 Exchange 服务器或从任何连接域的服务器或工作站执行这些步骤。此外，OAuth 身份验证进程在使用 Internet Explorer 11 或更高版本的桌面版时效果最佳。

  - 检查 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md) 主题，并确保您清楚会受到配置混合部署影响的方面。

  - 检查并完成 [混合部署先决条件](hybrid-deployment-prerequisites-exchange-2013-help.md) 概括的所有混合部署要求。

  - Microsoft 远程连接分析工具可以检查内部部署 Exchange 组织的外部连接，确保做好配置混合部署的准备。强烈建议在使用混合配置向导配置混合部署之前，使用远程连接分析工具检查内部部署组织。有关更多信息，请参阅[远程连接分析工具](http://go.microsoft.com/fwlink/p/?linkid=167905)。

  - 我们强烈建议使用 Azure Active Directory Connect 的密码同步配置单一登录。单一登录使用户可以使用一个用户名和密码访问内部部署组织和 Exchange Online 组织。单一登录也确保用户在使用 “Exchange Online Archiving” 访问 Exchange Online 组织中的存档内容时，不会获得凭据提示。有关密码同步的详细信息，请参阅 [Azure AD Connect 同步：实施密码同步](http://go.microsoft.com/fwlink/p/?linkid=723513)

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](https://technet.microsoft.com/zh-cn/library/jj150484\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ659053.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 Exchange 管理中心与混合配置向导创建混合部署

使用以下过程来创建和配置混合部署：

1.  在您的内部部署组织中某个 Exchange 服务器上的 EAC 中，导航到“混合”节点。

2.  在“混合”节点中，单击“配置”以输入您的 Office 365 凭据。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的内部部署组织位于中国并且您的 Office 365 租户由世纪互联托管，则必须选中“我的 Office 365 组织由世纪互联托管”复选框。如果您的 Office 365 租户由世纪互联托管但未选中此复选框，混合配置向导将无法连接到世纪互联服务，您的 Office 365 帐户凭据不会被识别，因此无法正确完成向导。</td>
    </tr>
    </tbody>
    </table>


3.  提示您登录到 Office 365 时，选择“登录到 Office 365”并输入帐户凭据。您登录到的帐户需要是 Office 365 中的全局管理员。

4.  单击“配置”以启动“混合配置”向导。

5.  在“Microsoft Office 365 混合配置向导下载”页面上，单击“单击此处” 下载向导。系统提示时，在“应用程序安装”对话框上单击“安装”。

6.  单击“下一步”，然后在“内部部署 Exchange Server 组织”部分中，选择“检测运行 Exchange 2013 CA 或 Exchange 2016 的服务器”。该向导将尝试检测内部部署 Exchange 服务器。如果该向导没有检测到 Exchange 服务器，或者如果您想要使用另一台服务器，请选择“指定运行 Exchange 2013 CA 或 Exchange 2016 的服务器” ，然后指定 Exchange 邮箱服务器的内部 FQDN。

7.  在 **Office 365 Exchange Online** 部分中，选择 **Microsoft Office 365** ，然后单击“下一步”。

8.  在“凭据”页面上的“输入内部部署帐户凭据”部分中，选择“使用当前的 Windows 凭据”让向导使用您已登录的帐户来访问内部部署 Active Directory 和 Exchange 服务器。如果您想要指定一组不同的凭据，则取消选择“使用当前的 Windows 凭据” ，并指定您要使用的 Active Directory 帐户的用户名和密码。无论选择哪种方式，使用的帐户都需要为企业管理员安全组的成员。

9.  在“输入您的 Office 365” 凭据部分中，指定具有全局管理员权限的 Office 365 帐户的用户名和密码 。单击“下一步”。

10. 在“验证连接和凭据”页面中，该向导将连接到您的内部组织和 Office 365 组织来验证凭据并检查这两个组织的当前配置。完成时单击“下一步”。

11. 在“混合域”中，选择您想要在混合部署中包含的域。在大多数部署中，对于每个域，您可以将“自动发现”列设置为 **False**。如果您需要强制向导使用特定域中的自动发现信息，只能选择域旁边的 **True** 。单击“下一步”。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>当您运行向导时，混合配置向导的这一域选择步骤可能不会显示。<br />
    在以下情况下，此步骤将不会显示：
    <ul>
    <li><p>您仅添加一个内部部署接受的域到 Office 365 租户。由于这是混合部署配置可用的唯一域，该域将自动选定，同时向导中的步骤将跳过。</p></li>
    <li><p>没有添加任何内部部署接受的域到您的 Office 365 租户。在这种情况下，您将收到错误，同时需要在继续之前添加至少一个域到 Office 365 租户。可以通过使用 Office 365 管理门户完成此操作，也可以通过在内部部署组织中有选择地配置 Active Directory 联合身份验证服务 (AD FS) 完成此操作。</p></li>
    </ul>
    如果您添加了不止一个内部部署接受的域到 Office 365 租户，该步骤将显示。</td>
    </tr>
    </tbody>
    </table>


12. 在“联合身份验证信任”页面上，单击“启用” ，然后单击“下一步”。

13. 在“域所有权”页面上，单击“单击以复制到剪贴板”以为您选择的域复制域验证令牌信息，以包含在混合部署中。打开文本编辑器，如“记事本”，并粘贴这些域的令牌信息。在混合配置向导继续运行之前，必须使用该信息为公共 DNS 中的每个域创建一个 TXT 记录。请参考 DNS 主机的帮助，了解有关如何将 TXT 记录添加到 DNS 区域的信息。在创建 TXT 记录以及复制 DNS 记录后，单击“下一步”。

14. 在“传输证书”页面上的“选择引用服务器”字段中，选择具有您先前在检查列表中配置的证书的 Exchange 服务器。

15. 在“选择证书”字段中，选择用于安全邮箱传输的数字证书。该列表显示了安装在上一步所选的邮箱服务器上的，由第三方证书颁发机构 (CA) 颁发的数字证书。单击“下一步”。

16. 在“组织 FQDN”页面中，为您面向 Internet 的 Exchange 服务器输入可进行外部访问的 FQDN。Office 365 使用该 FQDN 来为 Exchange 组织之间的安全邮件传输配置服务连接器。例如，输入“mail.contoso.com”。单击“下一步”。

17. 混合部署配置选择已经更新，且您已准备好进行 Exchange 服务改变与混合部署配置。单击“更新”以开始配置过程。在混合配置过程进行时，向导显示正在为混合部署进行配置的各功能与服务方面，就如其已经更新过。

18. 向导将显示完成消息和“关闭”按钮。单击“关闭”以完成混合部署配置过程，并关闭向导。

## 配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证

对于 Exchange 2013/2010 与 Exchange 2013/2007 混合部署，Office 365 和内部部署组织之间基于新混合部署 OAuth 的身份验证连接不由混合配置向导配置。默认情况下，这些部署继续使用联合身份验证信任过程。但是，邮件记录管理 (MRM)、Exchange 就地存档和就地电子数据展示等特定 Exchange 2013 功能仅当使用新的 Exchange OAuth 身份验证协议时，才在组织中完全可用。对于希望将这些功能作为 Exchange Online 混合部署一部分来实施的所有混合 Exchange 2013/2010 与 Exchange 2013/2007 组织，我们建议在使用混合配置向导配置混合部署后再配置 Exchange OAuth 身份验证。

有关详细的配置步骤，请参阅[配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证](https://technet.microsoft.com/zh-cn/library/dn594521\(v=exchg.150\))

有关使用 OAuth 身份验证的 Exchange 安全与合规性功能的详细信息，请参阅：

  - [使用 OAuth 身份验证支持 Exchange 混合部署中的存档](https://technet.microsoft.com/zh-cn/library/dn689104\(v=exchg.150\))

  - [使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示](https://technet.microsoft.com/zh-cn/library/dn497703\(v=exchg.150\))

## 您如何知道这有效？

混合配置向导的成功完成会是混合配置步骤按预期进行的第一个指示。

为了进一步确认您已经成功创建与配置了混合部署，请执行下列操作：

  - 在 Exchange 命令行管理程序中为内部部署组织运行以下命令。该命令会显示混合部署配置值与设置、混合功能与传输终结点。确认这些值正确无误。
    
        Get-HybridConfiguration

  - 通过检查混合配置日志来确认混合配置向导是否完成了所有配置步骤。默认情况下，日志位于内部部署邮箱服务器的以下位置：C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration。

  - 将现有内部部署邮箱移至 Exchange Online 组织，以测试邮箱的移动功能支持；或在 Exchange Online 组织中创建新的用户邮箱，以测试两个组织之间共享的忙/闲日历信息。任一邮箱操作也会允许您测试与确认内部部署与 Exchange Online 组织之间的邮件传递是否正在与现有的邮箱一起正常工作，以及到 Exchange 组织的邮件传递是否为安全的，且是否在按内部邮件进行处理。
    
      - 使用 EAC，并导航至“企业” \> “收件人” \> “邮箱”，以在 Exchange Online 中创建新的邮箱。
    
      - 使用 EAC，并导航至“Office 365” \> “收件人” \> “迁移”，以移动现有邮箱到 Exchange Online。

