---
title: '配置联合身份验证信任: Exchange 2013 Help'
TOCTitle: 配置联合身份验证信任
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 50491053
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置联合身份验证信任

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-07-26_

联合身份验证信任在 Microsoft Exchange 2013 组织和 Azure Active Directory 身份验证系统之间建立信任关系。通过配置联合信任，可以配置与其他联合 Exchange 组织的联合共享以便在收件人之间共享日历忙/闲信息。可以在两个联合 Exchange 2013 组织之间或在联合 Exchange 2013 组织与联合 Exchange 2010 组织之间配置联合共享。您还可以设置与 Office 365 组织的共享。

> [!NOTE]
> 创建联合身份验证信任是在 Exchange 组织中设置联合共享的若干步骤之一。若要查看所有步骤，请参阅<a href="configure-federated-sharing-exchange-2013-help.md">配置联合共享</a>。


有关与联合身份验证相关的更多管理任务，请参阅[联合程序](federation-procedures-exchange-2013-help.md)。

> [!important]
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


## 在开始之前，您需要知道什么？

  - 估计完成时间：30 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅"联合身份验证和证书"中的[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题的权限条目。

  - 应当从 Internet 解析用于建立联合身份验证信任的域。这就要求通过域注册商注册该域，而且该域的域名系统 (DNS) 区域必须驻留在可从 Internet 访问的 DNS 服务器上。如果组织接收域的 Internet 电子邮件，则表明已符合这些要求。

  - 您需要将 TXT 记录添加到公用 DNS 中。查看向托管公用 DNS 记录的组织添加 TXT 记录的要求。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 具有联合共享关系的两个 Exchange 组织必须对其联合身份验证信任使用相同的 Azure AD 身份验证系统。此要求适用于在两个本地 Exchange 组织之间或在本地 Exchange 组织与由 [Office 365](https://go.microsoft.com/fwlink/?linkid=392576) 托管的 Exchange 组织之间配置联合共享的情况。

  - 在为您的 Exchange 2013 组织创建与 Azure AD 身份验证系统的联合身份验证信任时，该联合身份验证信任将使用 Azure AD 身份验证系统的业务实例。但是，其他具有早期 Exchange 版本和现有联合身份验证信任的联合 Exchange 组织可能会使用 Azure AD 身份验证系统的业务实例或消费者实例。
    
    默认情况下，以下 Exchange 组织会使用 Azure AD 身份验证系统的业务实例：
    
      - 对联合身份验证信任使用\&quot;启用联合身份验证信任\&quot;向导和自签名证书的 Exchange 2013 组织。
    
      - Exchange 2010 SP1 或更高版本组织，通过使用\&quot;新建联盟信任\&quot;向导和联盟信任的自签名证书。
    
      - 由 Office 365 托管的 Exchange 组织，例如 Exchange Online。
    
    默认情况下，以下 Exchange 组织会使用 Azure AD 身份验证系统的消费者实例：
    
      - 交付厂商版 (RTM) 的 Exchange 2010 组织，通过使用第三方证书颁发机构颁发的证书。
    
    我们建议所有 Exchange 组织都对联合身份验证信任使用 Azure AD 身份验证系统的业务实例。在两个 Exchange 组织之间配置联合共享之前，需要验证每个 Exchange 组织用于任何现有联合身份验证信任的 Azure AD 身份验证系统实例。若要确定 Exchange 组织对现有联合身份验证信任使用哪种 Azure AD 身份验证系统实例，请运行以下命令行管理程序命令。
    
        Get-FederationInformation -DomainName <hosted Exchange domain namespace>
    
    业务实例的 *TokenIssuerURIs* 参数将返回值 `<uri:federation:MicrosoftOnline>`。
    
    消费者实例的 *TokenIssuerURIs* 参数将返回值 `<uri:WindowsLiveID>`。
    
    若要配置与有现有的联合身份验证信任使用Azure AD身份验证系统的业务实例的Exchange组织联盟共享，请按照本主题中的步骤。这些步骤是所有您需要执行以创建可用于启用联盟共享或Exchange 2013公司和Exchange 2010公司正在使用Exchange 2013的两个组织之间的联合身份验证信任Azure AD身份验证系统的业务实例。
    
    要在您的 Exchange 2013 组织和一个具有使用 Azure AD 身份验证系统消费者实例的现有联合身份验证信任的 Exchange 组织之间配置联合共享，使用消费者实例的 Exchange 组织应安装 Exchange 2010 SP2 或更高版本或升级到 Exchange 2013。如果您决定安装 Exchange 2010 SP2 或更高版本，请使用\&quot;新建联合身份验证信任\&quot;向导删除并重新创建现有的联合域和联合身份验证信任。重新创建联合身份验证信任时，将使用 Azure AD 身份验证系统的业务实例。

## 使用 EAC 创建和配置联合身份验证信任

1.  在内部部署组织中的 Exchange 2013 服务器上，导航到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  单击\&quot;启用\&quot;以启动\&quot;启用联合身份验证信任\&quot;向导。

3.  在向导完成后，单击\&quot;关闭\&quot;。

4.  在\&quot;共享\&quot;选项卡的\&quot;联合身份验证信任\&quot;部分，单击\&quot;修改\&quot;。

5.  在\&quot;启用共享的域\&quot;中的\&quot;步骤 1\&quot;旁边，单击\&quot;浏览\&quot;。

6.  在\&quot;选择接受的域\&quot;中，从列表中选择主共享域，然后单击\&quot;确定\&quot;。
    
    > [!NOTE]
    > 您选择的域将用于配置联合身份验证信任的 OrgID。有关 OrgID 的详细信息，请参阅<a href="federation-exchange-2013-help.md">联盟</a>。


7.  记下生成的主共享域联盟的域证明。您将使用此字符串以公用 DNS 服务器上创建一个 TXT 记录。
    
    > [!important]
    > 联盟的域证明是字母数字字符的字符串。若要避免输入的错误，我们建议您从 EAC，复制字符串并将其粘贴到文本编辑器 （如记事本）。可以然后将其从文本编辑器中复制到剪贴板，并将它粘贴到<strong>文本</strong>字段中创建 TXT 记录时。如果使用创建 TXT 记录不正确的联盟域验证字符串、 Azure AD身份验证系统将无法验证域所有权证明和您不能将其添加到联盟的组织标识符。


8.  在**第 2 步**中，单击**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")将其他域添加到组织中需要联合共享功能的用户将使用的电子邮件地址的联盟信任。例如，如果您有使用其电子邮件地址，例如 sales.contoso.com 在一个子域中的用户，您将 sales.contoso.com 域添加到联合身份验证信任。
    
    > [!NOTE]
    > 将为选择的每个额外域创建一个联合域证明字符串。必须为每个额外域在公用 DNS 上创建单独的 TXT 记录。


9.  使用为每个域创建的联合域证明字符串，在公用 DNS 服务器上为每个域创建 TXT 记录。根据公用 DNS 主机的更新计划，DNS 更改的复制可能需要 15 分钟或更久。

10. 在创建并复制 TXT 记录之后，单击\&quot;更新\&quot;。

## 使用命令行管理程序创建和配置联合身份验证信任

1.  运行以下命令来创建联合身份验证信任证书的唯一主题密钥标识符：
    
        $ski = [System.Guid]::NewGuid().ToString("N")

2.  使用此语法来创建联合身份验证信任的自签名的证书：
    
        New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    
    本示例创建自行签署式证书对联合身份验证信任与Azure AD身份验证系统。证书使用友好名称值联合共享交换，以及域值从**USERDNSDOMAIN**环境变量。
    
        New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski

3.  要创建联合身份验证信任和自动部署到Exchange服务器前面步骤中创建您的组织中的自签名的证书，请使用以下语法：
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    
    本示例创建名为 Azure AD 身份验证联合身份验证信任并部署名为联合共享交换自签名的证书。
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"

4.  使用此语法要返回的域所有权具有所需的任何域，您将配置联合身份验证信任的 TXT 记录证明。
    
        Get-FederatedDomainProof -DomainName <domain>
    
    本示例返回域所有权具有所需的共享的主域 contoso.com 的 TXT 记录的证明。
    
        Get-FederatedDomainProof -DomainName contoso.com
    
    **注意：** 
    
      - 每个域或子域配置联合身份验证信任需要域所有权 TXT 记录的证明，因此您可能需要运行此命令多次使用不同的*DomainName*值。
    
      - 我们建议您将域验证字符串复制中右击外壳、 选择**标记**，选择**证明**值，然后按 enter 键，以便您可以使用它创建 TXT 记录时。如果使用不正确的联盟的域验证字符串创建 TXT 记录， Azure AD身份验证系统无法验证您的域中，所有权，您不能将其添加到联盟的组织标识符。

5.  使用上一步的信息，将会包括在联合身份验证信任每个域中公用 DNS 服务器上创建 TXT 记录。这取决于您的公用 DNS 主机的更新计划，复制 DNS 更改可能需要 15 分钟或更长时间。验证了新 TXT 记录都可用后继续。

6.  运行以下命令来从Azure AD中检索元数据和证书：
    
        Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"

7.  使用此语法来配置主要共享您在步骤 3 中创建的联合身份验证信任域。将使用您指定的域配置联合身份验证信任的组织标识符 (OrgID)。有关 OrgID 的详细信息，请参阅[联合组织标识符](federation-exchange-2013-help.md)。
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    
    本示例配置接受的域 contoso.com 共享为主的联合身份验证信任域命名 Azure AD 身份验证。
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true

8.  若要将其他域添加到联合身份验证信任，请使用以下语法：
    
        Add-FederatedDomain -DomainName <AdditionalDomain>
    
    此示例向子域 sales.contoso.com 联合信任，因为具有 sales.contoso.com 域中的电子邮件地址的用户需要联合共享功能。
    
        Add-FederatedDomain -DomainName sales.contoso.com
    
    请记住，任何域或子域添加到联合身份验证信任需要域所有权 TXT 记录的证据

有关详细的语法和参数的信息，请参阅[New-ExchangeCertificate](https://technet.microsoft.com/zh-cn/library/aa998327\(v=exchg.150\))、 [New-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd351047\(v=exchg.150\))、 [Get-FederatedDomainProof](https://technet.microsoft.com/zh-cn/library/ff717833\(v=exchg.150\))、 [Set-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd298034\(v=exchg.150\))、 [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/zh-cn/library/dd351037\(v=exchg.150\))和[Add-FederatedDomain](https://technet.microsoft.com/zh-cn/library/dd351208\(v=exchg.150\))。

## 您如何知道这有效？

成功完成\&quot;启用联合身份验证信任\&quot;和\&quot;启用共享的域\&quot;向导初步表示，按预期配置了联合身份验证信任。

为了进一步确认您已经成功创建与配置了联合身份验证信任，请执行以下操作：

1.  运行以下命令行管理程序命令以验证联合身份验证信任信息。
    
        Get-FederationTrust | Format-List

2.  将*\<PrimarySharedDomain\>*替换为主要共享域，并运行以下的 Shell 命令，以验证联盟信息可从您的组织。
    
        Get-FederationInformation -DomainName <PrimarySharedDomain>

有关语法和参数的详细信息，请参阅 [Get-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd351262\(v=exchg.150\)) 和 [Get-FederationInformation](https://technet.microsoft.com/zh-cn/library/dd351221\(v=exchg.150\))。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

