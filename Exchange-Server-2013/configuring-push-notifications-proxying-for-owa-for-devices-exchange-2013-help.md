---
title: '为 OWA for Devices 配置推送通知代理: Exchange 2013 Help'
TOCTitle: 为 OWA for Devices 配置推送通知代理
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59954253
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为 OWA for Devices 配置推送通知代理

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

为 Microsoft Exchange 2013 本地部署的 适用于设备的 OWA（OWA for iPhone 和 OWA for iPad）启用推送通知，使用户能够接收其 OWA for iPhone 和 OWA for iPad 的 Outlook Web App 图标上的更新，这些更新将指明用户邮箱中未查看的邮件数量。如果未配置和启用推送通知，那么在不启动应用的情况下，具有 适用于设备的 OWA 的用户将无从知晓收件箱中存在未查看的邮件。当收到新邮件时，用户设备上的 适用于设备的 OWA 徽章将会更新，看上去和以下徽章一样。

![OWA for Devices 标志](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "OWA for Devices 标志")

## 如何启用推送通知？

若要启用推送通知，本地 Exchange 2013 服务器必须要连接到 Office 365 推送通知服务，以便将推送通知发送到 iPhone 和 iPad。Exchange 2013 本地服务器通过 Office 365 通知服务路由其更新通知，从而无需为开发者帐户注册第三方推送通知服务。下图显示了 iPhone 和 iPad 用户如何获取有关未查看邮件的徽章更新的流程。

![推送通知的流程](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "推送通知的流程")

若要启用推送通知，管理员必须执行以下操作：

1.  在适用于企业的 Office 365 中注册您的组织。

2.  将所有本地服务器更新到 Exchange Server 2013 累积更新 3 (CU3) 或更高版本。

3.  将本地 Exchange 2013 设置为使用 Office 365 身份验证

4.  启用从本地 Exchange Server 2013 到 Office 365 的推送通知，并验证这些推送通知是否正常工作。

## 在适用于企业的 Office 365 中注册您的组织

Office 365 是一款基于云的服务，旨在帮助您满足组织对强大安全性、可靠性和用户工作效率的需求。Office 365 是指一系列订阅计划，其中包括对以下内容的访问：Office 应用程序以及通过 Internet（云服务）实现的其他生产效率服务（例如 Lync Web 会议和适用于企业的 Exchange Online 托管电子邮件）。

许多 Office 365 计划还包括最新 Office 应用程序的桌面版本，可供用户在多台计算机和设备上安装。所有 Office 365 计划均在订阅的基础上按月或按年付费。要查看更多信息或在适用于您组织的 Office 365 中注册，请参阅[什么是适用于企业的 Office 365？](http://go.microsoft.com/fwlink/?linkid=335705)。有关通过 Office 365 提供的各项服务的详细信息，请参阅 [Office 365 服务订阅](http://go.microsoft.com/fwlink/?linkid=335704)。

## 升级到 CU3 或更高版本

Exchange Server 2013 的累积更新 3 (CU3) 解决了自 RTM 后发布的 Exchange Server 2013 软件中存在的问题。其中包含 CU1 和 CU2 中的所有问题和修复以及自 CU2 发布后的其他修复和更新。强烈建议所有 Exchange Server 2013 本地客户安装此更新，而且这也是接收推送通知所必需的。若要了解有关累积更新（包括 CU3）的信息，请参阅 [Exchange 2013 更新](updates-for-exchange-2013-exchange-2013-help.md)。

## 将本地 Exchange 2013 设置为使用 Office 365 身份验证

Exchange Server 2013 采用的方法是对服务器到服务器身份验证使用单个标准化方法。[Exchange Server 2013](http://go.microsoft.com/fwlink/?linkid=290946)（以及 [Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=273796) 和 [SharePoint 2013](http://go.microsoft.com/fwlink/?linkid=335701)）和 [Office 2013](http://go.microsoft.com/fwlink/?linkid=335696) 支持对服务器到服务器身份验证和授权使用 OAuth（开放授权）协议。OAuth 是许多重要网站使用的标准授权协议，借助于该协议，用户凭据和密码不会从一台计算机传递到另一台计算机。相反，身份验证和授权在 OAuth 安全令牌的基础上进行；这些令牌会授予在特定时间段内对一组特定资源的访问权限。

OAuth 身份验证通常涉及到三个组件：一台授权服务器和两个需要互相进行通信的领域。授权服务器（也称为安全令牌服务器）向需要通信的两个领域颁发安全令牌；这些令牌会确认来自一个领域的通信是否应受另一个领域信任。例如，授权服务器可能会颁发令牌来验证某个特定 Lync Server 2013 领域的用户是否能够访问指定的 Exchange 2013 领域；反之亦然。

> [!TIP]  
> 领域是一个安全容器。


但是，对于本地服务器到服务器身份验证，无需使用第三方令牌服务器。服务器产品（例如 Lync Server 2013 和 Exchange 2013）都具有内置的令牌服务器，可用于其他支持服务器到服务器身份验证的 Microsoft 服务器（例如 SharePoint Server）进行身份验证。例如，Lync Server 2013 本身可以颁发和签署安全令牌，然后使用该令牌与 Exchange 2013 进行通信。在此类情况下，不需要第三方令牌服务器。

为了配置 Exchange Server 2013 的本地实现到 Office 365 的服务器到服务器身份验证，您必须要完成两个步骤：

  - **步骤 1 – 向本地 Exchange 服务器的内置令牌颁发者分配证书。** 首先，本地 Exchange 管理员必须使用以下 Exchange 命令行管理程序脚本创建证书（如果以前没有创建），并将其分配给本地 Exchange 服务器的内置令牌颁发者。此为一次性流程；创建证书后，该证书将重复用于其他身份验证方案，且不会被替代。请务必将 *$tenantDomain* 的值更新为您的域名。为此，请复制并粘贴以下代码。
    
    > [!WARNING]  
    > 通过将代码复制并粘贴到文本编辑器（如 Notepad）中，并使用 .ps1 扩展名将其保存，运行命令行管理程序脚本将变得更加容易。
    

    ```C Sharp
    # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
    
    $tenantDomain = "Fabrikam.com"
    
    # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
    
    $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
    If ($c.Count -eq 0)
    {
        Write-Host "Creating certificate for oAuth..."
        $ski = [System.Guid]::NewGuid().ToString("N")
        $friendlyName = "Exchange S2S OAuth"
        New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
        $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
    }
    ElseIf ($c.Count -gt 1)
    {
        $c = $c[0]
    }
    
    $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
    If ($a.Count -eq 0)
    {
        Set-AuthConfig -CertificateThumbprint $c.Thumbprint
    }
    Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
    
    # Export the certificate
    
    Write-Host "Exporting certificate..."
    if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
    {
        md $env:SYSTEMDRIVE\OAuthConfig
    }
    cd $env:SYSTEMDRIVE\OAuthConfig
    
    $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
    $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
    $certBytes = $oAuthCert.Export($certType)
    $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
    [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
    
    # Set AuthServer
    $authServer = Get-AuthServer MicrosoftSts;
    if ($authServer.Length -eq 0)
    {
        Write-Host "Creating AuthServer Config..."
        New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
    }
    elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
    {
        Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
        Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
    }
    else
    {
        Write-Host "AuthServer Config already exists."
    }
    Write-Host "Complete."
    ```    

    预期的结果应类似于以下输出结果。
    
    ```powershell
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
    ```

    > [!WARNING]  
    > 在继续之前，必须执行 用于 Windows PowerShell 的 Azure Active Directory 模块 cmdlet。如果尚未安装 用于 Windows PowerShell 的 Azure Active Directory 模块 cmdlet（以前称为用于 Windows PowerShell 的 Microsoft Online Services 模块），您可以从<a href="http://aka.ms/aadposh">使用 Windows PowerShell 管理 Azure AD</a> 进行安装。


  - **步骤 2 – 将 Office 365 配置为与 Exchange 2013 本地服务器进行通信。** 将 Exchange Server 2013 要与之通信的 Office 365 服务器配置为合作伙伴应用程序。例如，如果 Exchange Server 2013 本地服务器需要与 Office 365 进行通信，则需要将 Exchange 本地服务器配置为合作伙伴应用程序。合作伙伴应用程序是可以与 Exchange 2013 直接交换安全令牌的任何应用程序，而无需通过第三方安全令牌服务器。本地 Exchange 2013 管理员必须使用以下 Exchange 命令行管理程序脚本将 Exchange 2013 要与之通信的 Office 365 租户配置为合作伙伴应用程序。在执行期间，系统将提示输入 Office 365 租户域的管理员用户名和密码（例如，administrator@fabrikam.com）。请务必将 *$CertFile* 的值更新到证书的位置（如果未从以前的脚本创建）。为此，请复制并粘贴以下代码。
    
    ```C Sharp
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        } 
    ```

    预期的结果应如下所示。
    
    ```powershell
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.
    ```

## 启用推送通知代理

根据上述步骤成功设置 OAuth 身份验证后，本地管理员必须通过以下脚本启用推送通知代理。请务必将 *$tenantDomain* 的值更新为您的域名。为此，请复制并粘贴以下代码。

```powershell
    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain
```

预期的结果应类似于以下输出结果。

```powershell
    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged
```

## 验证推送通知是否正常工作

完成上述步骤后，可以通过以下方式之一测试推送通知：

  - **向用户的邮箱发送测试电子邮件：** 
    
    1.  在移动设备上的 OWA for Devices 中设置帐户，以订阅通知。
    
    2.  返回设备主屏幕，这将使 OWA for Devices 在后台工作。
    
    3.  从另一台设备（如电脑）将一封电子邮件发送到在移动设备上设置的帐户的收件箱。
    
    4.  这应该会在几分钟内生成未查看邮件的计数（将在应用图标上指明）。

  - **启用监控。** 测试推送通知或调查通知失败原因的另一种方法是，在您的组织中对邮箱服务器启用监控。本地 Exchange 2013 服务器管理员必须通过以下脚本调用推送通知代理监控。为此，请复制并粘贴以下代码。
    
    ```powershell
        # Send a push notification to verify connectivity.
        
        $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
        If ($s.Count -gt 1)
        {
            $s = $s[0]
        }
        If ($s.Count -ne 0)
        {
            # Restart the monitoring service to clear the cache from when push was previously disabled.
            Restart-Service MSExchangeHM
        
            # Give the monitoring service enough time to load.
            Start-Sleep -Seconds:120
        
            Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
        }
        Else
        {
            Write-Error "Cannot find a Mailbox server in the current site."
        }
    ```

    预期的结果应类似于以下输出结果。
    
    ```powershell
        ResultType : Succeeded
        Error      :
        Exception  :
    ```
