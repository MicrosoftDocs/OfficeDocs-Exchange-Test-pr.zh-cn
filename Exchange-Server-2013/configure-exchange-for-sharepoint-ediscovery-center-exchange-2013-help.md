---
title: '针对 SharePoint eDiscovery 中心配置 Exchange: Exchange 2013 Help'
TOCTitle: 针对 SharePoint eDiscovery 中心配置 Exchange
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 50490869
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 针对 SharePoint eDiscovery 中心配置 Exchange

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

Microsoft Exchange Server 2013 包括使用 Microsoft SharePoint Server 2013 和 Microsoft Lync Server 2013 的功能，称为*合作伙伴应用程序*。要确保这些合作伙伴应用程序可以访问其他每个应用程序的资源，需要配置服务器到服务器的身份验证。

本主题显示如何在 Exchange 2013 和 SharePoint 2013 之间配置服务器到服务器的身份验证，以便用户可以使用 SharePoint 2013 中的电子数据展示中心来搜索 Exchange Server 2013 邮箱内容。要完全启用此功能，必须完成 SharePoint 2013 中的其他步骤。有关详细信息，请参阅[在 SharePoint Server 2013 中配置电子数据展示](https://go.microsoft.com/fwlink/?linkid=257727)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：30 分钟。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 支持在不同的域或林中安装 Exchange 2013 和 SharePoint 2013。Exchange 和 SharePoint 林之间的 Windows 信任关系不是必需的，因为在该环境中，Exchange 和 SharePoint 将依靠 OAuth 2.0 协议达成相互信任。

  - SharePoint 2013 站点必须配置为使用安全套接字层 (SSL)。

  - [Exchange Web 服务托管 API](https://go.microsoft.com/fwlink/?linkid=257726) 必须安装在运行 SharePoint 2013 的每个服务器上。安装后重置 Internet 信息服务器 (IIS)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您该如何做？

## 步骤 1：在运行 SharePoint Server 2013 的服务器上为 Exchange 2013 配置服务器到服务器的身份验证

运行以下命令创建 Exchange 2013 作为 SharePoint 2013 中的可信安全令牌颁发者。

    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1

## 步骤 2：在运行 Exchange 2013 的服务器上为 SharePoint 2013 配置服务器到服务器的身份验证

在 Exchange 2013 服务器上执行此步骤。您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“合作伙伴应用程序 - 配置”条目。

运行此命令配置 SharePoint 合作伙伴应用程序。

    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint

## 步骤 3：将授权用户添加到发现管理角色组

将需要使用 SharePoint 2013 执行电子数据展示搜索的用户添加到 Exchange 2013 中的发现管理角色组。有关详细信息，请参阅[在 Exchange 中分配电子数据展示权限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将用户添加到发现管理角色组之后，用户即可使用就地电子数据展示来搜索所有 Exchange 2013 邮箱并访问用户邮箱中可能敏感的电子邮件内容。默认情况下，不向任何用户分配此权限，包括组织管理角色组的成员。向任何用户分配此权限之前，与组织的法律或 HR 部门进行核查。</td>
</tr>
</tbody>
</table>

