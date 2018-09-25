---
title: '配置采用 SharePoint 2013 和 Lync 2013 的 OAuth 身份验证: Exchange 2013 Help'
TOCTitle: 配置采用 SharePoint 2013 和 Lync 2013 的 OAuth 身份验证
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 50491692
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置采用 SharePoint 2013 和 Lync 2013 的 OAuth 身份验证

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-03-03_

Exchange Server 2013 允许其他应用程序使用 OAuth 对 Exchange 进行身份验证。应用程序必须配置为 Exchange 2013 中的合作伙伴应用程序。

在 Exchange 2013 中，只能通过使用 `Configure-EnterpriseApplication.ps1` 脚本来支持采用合作伙伴应用程序（例如 SharePoint 2013 和 Lync Server 2013）的 OAuth 配置。通过自动进行任务，脚本使其更加容易配置采用合作伙伴应用程序的身份验证并减少配置错误。此脚本执行下列任务：

1.  配置企业合作伙伴应用程序，其自行发出 OAuth 令牌以成功对 Exchange 进行身份验证。

2.  将基于角色的访问控制 (RBAC) 角色分配至合作伙伴应用程序以授予其权限，调用特定 Exchange Web 服务 API。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 合作伙伴应用程序必须为 Exchange 2013 发布 auth 元数据文档来建立对该应用程序的直接信任并接受身份验证请求。

  - 本主题中的示例使用 `\Scripts` 目录的以下默认位置：`C:\Program Files\Microsoft\Exchange Server\V15\Scripts`.

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“合作伙伴应用程序 - 配置”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用合作伙伴应用程序配置 OAuth 身份验证

该过程使用 `Configure-EntepririseApplication.ps1` 脚本来配置采用合作伙伴应用程序的 OAuth 身份验证。对资源的访问权限取决于分配至合作伙伴应用程序和/或其通过使用 RBAC 模拟的用户的权限。

在通过 Exchange 配置 OAuth 身份验证后，合作伙伴应用程序可使用 Exchange 2013 资源。如果 Exchange 2013 也需要访问合作伙伴应用程序提供的资源，则您还必须在合作伙伴应用程序中配置 OAuth 身份验证。

本示例将为 SharePoint 2013 配置 OAuth 身份验证。

  ```powershell
    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint
  ```

本示例将为 Lync Server 2013 配置 OAuth 身份验证。

  ```powershell
    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync
  ```
  
## 您如何知道这有效？

要验证是否成功配置了企业合作伙伴应用程序对 Exchange 2013 进行身份验证，可在命令行管理程序中运行 [Get-PartnerApplication](https://technet.microsoft.com/zh-cn/library/jj218721\(v=exchg.150\)) cmdlet 来检索配置。也可使用合作伙伴应用程序运行 [Test-OAuthConnectivity](https://technet.microsoft.com/zh-cn/library/jj218623\(v=exchg.150\)) cmdlet 来测试用户的 OAuth 连接性。

## 详细信息

  - 在混合部署中，您可以在本地 Exchange 2013 组织和 Exchange Online 组织之间使用 OAuth 身份验证。有关详细信息，请参阅[使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)。

  - 在本地部署中，您可以在 Exchange 2013 和 SharePoint 2013 之间配置服务器到服务器身份验证。这样，管理员和合规部主管就可以使用 SharePoint 2013 中的电子数据展示中心搜索 Exchange 2013 邮箱。有关详细信息，请参阅[针对 SharePoint eDiscovery 中心配置 Exchange](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。

