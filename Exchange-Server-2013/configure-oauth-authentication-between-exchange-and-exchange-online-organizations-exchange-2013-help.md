---
title: '配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证: Exchange 2013 Help'
TOCTitle: 配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170809
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

使用混合配置向导时，仅 Exchange 2013 混合部署将配置 OAuth 身份验证。对于 Exchange 2013/2010 与 Exchange 2013/2007 混合部署，Office 365 和内部部署组织之间基于新混合部署 OAuth 的身份验证连接不由混合配置向导配置。默认情况下，这些部署继续使用联合身份验证信任过程。但是，某些 Exchange 2013 功能仅在使用新的 Exchange OAuth 身份验证协议时，才在整个组织内完全可用。

新的 Exchange OAuth 身份验证过程当前支持以下 Exchange 功能：

  - 邮件权限管理 (MRM)

  - Exchange 就地电子数据展示

  - Exchange 就地存档

我们建议所有实现 Exchange 2013 和 Exchange Online 混合部署的混合 Exchange 组织在使用混合部署向导配置混合部署之后都要配置 Exchange OAuth 身份验证。

> [!IMPORTANT]  
> 如果您的内部部署组织仅运行安装有累积更新 5 或更高版本的 Exchange 2013 服务器，请运行混合部署向导而不是执行本主题中的步骤。
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“联合身份验证和证书”权限条目。

  - 使用混合部署向导完成混合部署的配置。有关详细信息，请参阅 [Exchange Server 混合部署](https://technet.microsoft.com/zh-cn/library/jj200581\(v=exchg.150\))。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 如何在本地 Exchange 和 Exchange Online 组织之间配置 OAuth 身份验证？

## 步骤 1：为 Exchange Online 组织创建授权服务器对象

对于此步骤，您必须为 Exchange Online 组织指定验证域。此域应与用于基于云的电子邮件帐户的主 SMTP 域一样。在后面的步骤中，此域称为 *\<您的验证域\>*。

在本地 Exchange 组织的 Exchange 命令行管理程序 (Exchange PowerShell) 中运行以下命令。

    New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1

## 步骤 2：为 Exchange Online 组织启用合作伙伴申请

在本地 Exchange 组织的 Exchange PowerShell 中运行以下命令。

    Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true

## 步骤 3：导出本地授权证书

在此步骤中，您必须运行可导出本地授权证书的 PowerShell 脚本，此证书可在下一步骤中导入您的 Exchange Online 组织。

1.  将以下文本保存到名为 **ExportAuthCert.ps1**（示例名称）的 PowerShell 脚本文件中。
    
        $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
         
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)

2.  在本地 Exchange 组织的 Exchange PowerShell 中，运行您在上一步骤中创建的 PowerShell 脚本。例如：
    
        .\ExportAuthCert.ps1

## 步骤 4：将本地授权证书上载到 Azure Active Directory ACS

接下来，您必须使用 Windows PowerShell 将您在上一步骤中导出的本地授权证书上载到 Azure Active Directory 访问控制服务 (ACS)。为了完成此操作，必须安装 用于 Windows PowerShell 的 Azure Active Directory 模块 cmdlet。如果尚未安装，请转到 <https://aka.ms/aadposh> 安装 用于 Windows PowerShell 的 Azure Active Directory 模块。安装 用于 Windows PowerShell 的 Azure Active Directory 模块 后，完成以下步骤。

1.  单击“用于 Windows PowerShell 的 Azure Active Directory 模块”快捷方式，打开已安装 Azure AD cmdlet 的 Windows PowerShell 工作区。使用 Azure Active Directory 控制台的 Windows PowerShell 运行此步骤中的所有命令。

2.  将以下文本保存到名为 **UploadAuthCert.ps1**（示例名称）的 PowerShell 脚本文件中。
    
        Connect-MsolService;
        Import-Module msonlineextended;
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        $objFSO = New-Object -ComObject Scripting.FileSystemObject;
        $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
        $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
        $cer.Import($CertFile);
        $binCert = $cer.GetRawCertData();
        $credValue = [System.Convert]::ToBase64String($binCert);
        
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
        New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue

3.  运行您在上一步骤中创建的 PowerShell 脚本。例如：
    
        .\UploadAuthCert.ps1

4.  启动脚本后，您会看到凭据对话框。输入 Microsoft Online Azure AD 组织中的租户管理员帐户的凭据。运行脚本后，让 Azure AD 会话的 Windows PowerShell 处于打开状态。您将在下一步骤中使用此程序运行 PowerShell 脚本。

## 步骤 5：使用 Azure Active Directory 为外部本地 Exchange HTTP 端点注册所有主机名颁发机构

在此步骤中，您必须为可公开访问的本地 Exchange 组织中的每个端点运行该脚本。我们建议您使用通配符（如果可以的话）。例如，假设可通过 **https://mail.contoso.com/ews/exchange.asmx** 从外部访问 Exchange。在这种情况下，可以使用单个通配符：** \*.contoso.com**。这样就可以涵盖 autodiscover.contoso.com 和 mail.contoso.com 端点。不过，不会涵盖顶级域 **contoso.com**。如果 Exchange 2013 客户端访问服务器可通过顶级主机名颁发机构从外部访问，则您必须也将该主机名颁发机构注册为 **contoso.com**。注册其他外部主机名颁发机构并无限制。

如果您不确定本地 Exchange 组织中的外部 Exchange 端点，则可以通过在本地 Exchange 组织的 Exchange PowerShell 中运行以下命令来获取外部配置的 Web 服务端点的列表。

    Get-WebServicesVirtualDirectory | FL ExternalUrl

> [!NOTE]  
> 若要成功运行以下脚本，必须将 Azure Active Directory 的 Windows PowerShell 连接到 Microsoft Online Azure AD 租户，如上述部分中的步骤 4 所述。


1.  将以下文本保存到名为 **RegisterEndpoints.ps1**（示例名称）的 PowerShell 脚本文件中。本示例使用通配符将所有的端点注册为 contoso.com。用本地 Exchange 组织的主机名颁发机构替换 **contoso.com**。
    
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;

2.  在 Azure Active Directory 的 Windows PowerShell 中，运行您在上一步骤中创建的 Windows PowerShell 脚本。例如：
    
        .\RegisterEndpoints.ps1

## 步骤 6：创建从您的本地组织到 Office 365 的 IntraOrganizationConnector

必须为在 Exchange Online 中托管的邮箱定义目标地址。该目标地址会在 Office 365 租户创建后自动创建。例如，如果您的组织在 Office 365 租户中托管的域是“contoso.com”，则目标服务地址是“contoso.mail.onmicrosoft.com”。

使用 Exchange PowerShell 在本地组织中运行以下 cmdlet：

    New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>

## 步骤 7：创建从 Office 365 租户到您的本地 Exchange 组织的 IntraOrganizationConnector

必须为在本地组织中托管的邮箱定义目标地址。如果您组织的主 SMTP 地址是“contoso.com”，则该目标地址是“contoso.com”。

此外，您还必须为本地组织定义外部自动发现端点。如果您的公司是“contoso.com”，则此端点通常是以下两个地址中的一个：

  - https://autodiscover.\<主 SMTP 域\>/autodiscover/autodiscover.svc

  - https://\<主 SMTP 域\>/autodiscover/autodiscover.svc

> [!NOTE]  
> 您可以在本地和 Office 365 租户中使用 <a href="https://technet.microsoft.com/zh-cn/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</a> cmdlet，以确定 <a href="https://technet.microsoft.com/zh-cn/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</a> cmdlet 所需的端点值。


使用 Windows PowerShell 运行以下 cmdlet：

    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>

## 步骤 8：为任何 Exchange 2013 SP1 之前的服务器配置 AvailabilityAddressSpace。

在 Exchange 2013 之前的组织中配置了混合部署后，您需要在现有的 Exchange 组织中至少安装一个具有客户端访问服务器角色和邮箱服务器角色的 Exchange 2013 SP1 或更高版本服务器。Exchange 2013 客户端访问服务器和邮箱服务器充当前端服务器，负责协调现有 Exchange 内部部署组织和 Exchange Online 组织之间的通信。此通信包括内部部署组织与 Exchange Online 组织之间的邮件传输和消息功能。我们强烈建议在内部部署组织中安装多个 Exchange 2013 服务器，以帮助提高混合部署功能的可靠性和可用性。

在具有 Exchange 2013/2010 或 Exchange 2013/2007 的混合部署中，建议用于内部部署组织的面向 Internet 的所有前端服务器均为运行 Exchange 2013 SP1 或更高版本的客户端访问服务器。来自 Office 365 和 Exchange Online 的所有 Exchange Web 服务 (EWS) 请求均连接到内部部署中的 Exchange 2013 客户端访问服务器。此外，来自内部部署 Exchange 组织的适用于 Exchange Online 的所有 EWS 请求都必须通过运行 Exchange 2013 SP1 或更高版本的客户端访问服务器进行代理。由于这些 Exchange 2013 客户端访问服务器必须处理这些额外的传入和传出 EWS 请求，必须具有足够的 Exchange 2013 客户端访问服务器来处理负载并提供连接冗余。所需的客户端访问服务器数量取决于 EWS 请求的平均数量，且因组织而异。

完成下面的步骤之前，请确保：

  - 前端混合服务器为 Exchange 2013 SP1 或更高版本

  - 您对 Exchange 2013 服务器具有唯一的外部 EWS URL。Office 365 租户必须连接到这些服务器，使基于云的混合功能请求正常运行。

  - 服务器具有邮箱服务器和客户端访问服务器角色

  - 任何现有的 Exchange 2010/2007 邮箱服务器和客户端访问服务器都应用了最新的累积更新 (CU) 或 Service Pack (SP)。
    
    > [!NOTE]  
    > 现有的 Exchange 2010/2007 邮箱服务器可以继续使用 Exchange 2010/2007 客户端访问服务器，作为非混合功能连接的前端服务器。只有 Office 365 租户的混合部署功能请求需要连接到 Exchange 2013 服务器。


在指向内部部署 Exchange 2013 SP1 客户端访问服务器的 Exchange Web 服务终结点的 Exchange 2013 之前的客户端访问服务器上，必须配置 *AvailabilityAddressSpace*。此终结点是步骤 5 之前介绍的同一个终结点，您也可以通过在本地 Exchange 2013 SP1 客户端访问服务器上运行以下 cmdlet 来确定此终结点：

    Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl

> [!NOTE]  
> 如果从多个服务器返回虚拟目录信息，请确保使用为 Exchange 2013 SP1 客户端访问服务器返回的终结点。它将显示 <em>AdminDisplayVersion</em> 参数的 15.0（内部版本 847.32）或更高版本。


要配置 *AvailabilityAddressSpace*，请使用 Exchange PowerShell 并在内部部署组织中运行以下 cmdlet：

    Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True

## 您如何知道这有效？

您可以使用 [Test-OAuthConnectivity](https://technet.microsoft.com/zh-cn/library/jj218623\(v=exchg.150\)) cmdlet 验证 OAuth 配置是否正确。此 cmdlet 可验证本地 Exchange 和 Exchange Online 终结点能否成功对对方的请求进行身份验证。

> [!IMPORTANT]  
> 通过远程 PowerShell 连接到您的 Exchange Online 组织时，您可能需要结合使用 <em>AllowClobber</em> 参数和 <strong>Import-PSSession</strong> cmdlet，以将最新的命令导入本地 PowerShell 会话。


若要验证您的本地 Exchange 组织能否成功连接到 Exchange Online，请在本地组织的 Exchange PowerShell 中运行以下命令：

    Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl

若要验证您的 Exchange Online 组织能否成功连接到本地 Exchange 组织，请使用[远程 PowerShell](https://technet.microsoft.com/zh-cn/library/jj984289\(v=exchg.150\)) 连接到您的 Exchange Online 组织，并运行以下命令：

    Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl

例如 Test-OAuthConnectivity -Service EWS -TargetUri https://lync.contoso.com/metadata/json/1 -Mailbox ExchangeOnlineBox1 -Verbose | fl

> [!IMPORTANT]  
> 可以忽略“SMTP 地址没有与其关联的邮箱。”错误。只需关注 <em>ResultTask</em> 参数是否返回值“成功”即可。例如，测试输出的最后一部分应显示：
> <code>ResultType: Success</code><br />
> <code>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</code><br />
> <code>IsValid: True</code><br />
> <code>ObjectState: New</code>


> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

