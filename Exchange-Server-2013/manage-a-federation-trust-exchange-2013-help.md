---
title: '管理联合身份验证信任: Exchange 2013 Help'
TOCTitle: 管理联合身份验证信任
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 50489848
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理联合身份验证信任

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-01-01_

联合身份验证信任将建立 Microsoft Exchange 2013 组织和 Azure Active Directory 身份验证系统之间的信任关系，并支持与其他联合 Exchange 组织的联合共享。创建联合身份验证信任之后，通常不必对其进行管理或修改。但是，在某些情况下可能需要添加或删除联盟域，或是重置用于为联合身份验证信任配置组织标识符 (OrgID) 的域。

> [!NOTE]  
> 修改现有联合身份验证信任（尤其是用于定义 OrgID 的主共享域）可能会中断联盟 Exchange 组织之间的联合共享或针对具有 Office 365 组织的混合部署的联合共享。


有关与联合身份验证相关的更多管理任务，请参阅[联合程序](federation-procedures-exchange-2013-help.md)。

> [!IMPORTANT]  
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


## 在开始之前，您需要知道什么？

  - 估计完成时间：30 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅*Federation and certificates*[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的权限条目。

  - 需要针对添加到联合身份验证信任的每个新联盟域，将一条 TXT 记录添加到公用 DNS。查看向托管公用 DNS 记录的组织添加 TXT 记录的要求。

  - 针对本主题的用途，使用以下设置配置了一个现有联合身份验证信任：
    
      - “Contoso.com”是联合身份验证信任的主共享域。（此域将不会更改。）
    
      - 联盟域“service.contoso.com”和“sales.contoso.com”包含在现有联合身份验证信任中。
    
      - “Marketing.contoso.com”是 Exchange 组织中的接受域。

  - 本主题还涉及其他联合身份验证管理任务，如查看和管理用于联合身份验证信任的证书，以及在命令行管理程序中查看联合身份验证信任参数信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 管理联合身份验证信任

1.  在内部部署组织中的 Exchange 2013 服务器上，导航到“组织”\>“共享”。

2.  在“联合身份验证信任”部分中，单击“修改”。

3.  在“启用共享的域”中，跳过“步骤 1”，因为主共享域不会更改。

4.  在“步骤 2”中，选择“service.contoso.com”域，然后单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 以从联合身份验证信任中删除该域。

5.  在“步骤 2”中，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

6.  在“选择接受域”中，从接受域列表中选择“marketing.contoso.com”，然后单击“确定”以将该域添加到联合身份验证信任中。
    
    > [!IMPORTANT]  
    > 系统将为“marketing.contoso.com”域创建一个联盟域证明字符串。必须为此域在公用 DNS 上创建单独的 TXT 记录。


7.  通过使用为“marketing.contoso.com”域创建的联盟域证明字符串，在公用 DNS 服务器上创建一个 TXT 记录。根据公用 DNS 主机的更新计划，DNS 更改的复制可能需要 15 分钟或更久。

8.  在创建并复制该 TXT 记录之后，单击“更新”。

## 使用命令行管理程序管理联合身份验证信任

1.  本示例从联合身份验证信任中删除 service.contoso.com 域。
    
        Remove-FederatedDomain -DomainName service.contoso.com

2.  本示例将 marketing.contoso.com 域添加到联合身份验证信任。
    
        Add-FederatedDomain -DomainName marketing.contoso.com

有关语法和参数的详细信息，请参阅 [Remove-FederatedDomain](https://technet.microsoft.com/zh-cn/library/dd298128\(v=exchg.150\)) 和 [Add-FederatedDomain](https://technet.microsoft.com/zh-cn/library/dd351208\(v=exchg.150\))。

运行以下命令行管理程序命令以管理联合身份验证信任的其他方面：

1.  **查看联盟 OrgID 和联盟域**
    
    本示例将显示 Exchange 组织的联盟 OrgID 和相关信息，包括联盟域和状态。
    
        Get-FederatedOrganizationIdentifier

2.  **查看联合身份验证信任证书**
    
    本示例将显示联合身份验证信任 Azure AD 身份验证所使用的上一个、当前和下一个证书。
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **检查联合身份验证证书状态**
    
    本示例将显示组织中所有邮箱和客户端访问服务器上的联合身份验证证书的状态。
    
        Test-FederationTrustCertificate

4.  **配置联合身份验证信任以使用某证书作为下一个证书**
    
    本示例将配置联合身份验证信任 Azure AD 身份验证，以将具有所提供指纹的证书用作下一个证书。将证书部署到组织中所有 Exchange 服务器上之后，可以使用 *PublishCertificate* 开关配置联合身份验证信任，以将此证书用作当前证书。
    
        Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17

5.  **配置联合身份验证信任，以将下一个证书用作当前证书**
    
    此示例将联合身份验证信任 Azure AD 身份验证配置为将下一个证书用作当前证书，并将其发布到 Azure AD 身份验证系统。
    
        Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    
    > [!CAUTION]  
    > 在将联合身份验证信任配置为将下一个证书用作当前联合身份验证证书之前，请确保已在组织中的所有 Exchange 服务器上部署了该证书。使用 <a href="https://technet.microsoft.com/zh-cn/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</a> cmdlet 可检查此证书的部署状态。


6.  **刷新 Azure AD 身份验证系统中的联合元数据和证书**
    
    此示例将刷新 Azure AD 身份验证系统的联合元数据和证书，以进行联合身份验证信任 Azure AD 身份验证。
    
        Set-FederationTrust "Azure AD authentication" -RefreshMetadata

有关语法和参数的详细信息，请参阅下列主题：

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/zh-cn/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/zh-cn/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd298034\(v=exchg.150\))

## 您如何知道这有效？

成功完成“启用共享的域”向导初步表示，按预期配置了联合身份验证信任。

若要进一步验证是否成功，请执行下列操作：

1.  运行以下命令行管理程序命令以验证联合身份验证信任信息。
    
        Get-FederationTrust | format-list

2.  运行以下命令行管理程序命令以验证是否可以从组织检索联合身份验证信息。例如，验证是否在 *DomainNames* 参数中返回了 sales.contoso.com 和 marketing.contoso.com 域。
    
        Get-FederationInformation -DomainName <your primary sharing domain>

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

