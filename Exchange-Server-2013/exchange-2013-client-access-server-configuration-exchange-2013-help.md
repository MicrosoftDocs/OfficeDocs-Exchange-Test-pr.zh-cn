---
title: 'Exchange 2013 客户端访问服务器配置: Exchange 2013 Help'
TOCTitle: Exchange 2013 客户端访问服务器配置
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 50489826
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 客户端访问服务器配置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-07-25_

在安装了 Exchange 2013 客户端访问服务器之后，可以执行各种配置任务。虽然 Exchange 2013 中的客户端访问服务器不针对客户端协议进行处理，但是需要将几个设置应用于客户端访问服务器，包括虚拟目录设置和证书设置。

## 配置服务器证书

在 Exchange 2013 中，可以使用证书向导从证书颁发机构请求数字证书。在请求了数字证书之后，需要将其安装在客户端访问服务器上。

无需在组织中的邮箱服务器上安装数字证书。默认情况下会将一个自签名证书安装在邮箱服务器上，无需替换它。组织中的客户端访问服务器会隐式信任邮箱服务器上的自签名证书。有关详细信息，请参阅 [Exchange 2013 证书管理 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)。

## 配置虚拟目录

可以在虚拟目录上为脱机通讯簿 (OAB)、Exchange Web 服务、Exchange ActiveSync、Outlook Web App 和 Exchange 管理中心配置几个设置。有关虚拟目录管理的其他信息，请参阅[虚拟目录管理](virtual-directory-management-exchange-2013-help.md)。可以使用以下命令配置虚拟目录。

  - Exchange 2013 提供了 Outlook Anywhere 配置的两组 HTTP 连接设置，以便管理员配置内部或外部终结点。
    
    要使用单个连接用 URL 配置 Outlook Anywhere，必须提供主机名称，指明是否要求 SSL，还必须在 Exchange 命令行管理程序中使用以下命令指定一个 Authpackage：
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    也可以在 Exchange 命令行管理程序中通过使用以下命令来指定外部可访问终结点：
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    > [!TIP]  
    > 虽然 Exchange 2013 支持 Outlook Anywhere HTTP“协商”身份验证，但仅当环境中的所有服务器运行 Exchange 2013 时才能使用。


  - 若要配置 Exchange ActiveSync，请运行以下命令。
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"

  - 若要配置 Exchange Web 服务虚拟目录，请运行以下命令。
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx

  - 若要配置脱机通讯簿，请运行以下命令。
    
        Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"

  - 若要配置服务连接点，请运行以下命令。
    
        Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml

## 从 Exchange 2007 和 2010 客户端访问升级

使用该部分可帮助您配置对 Exchange 2013 客户端访问服务器上协议的外部访问。运行上面配置虚拟目录部分的 Exchange 命令行管理程序命令及下面的命令。

还需运行以下命令来为 Exchange 2013 配置虚拟目录。

1.  若要配置 Outlook Web App 的外部 URL，请在 Exchange 命令行管理程序中运行以下命令。
    
        Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    
    设置 Outlook Web App 虚拟目录后，在命令提示符中运行以下命令。
    
        Net stop IISAdmin /y
    
        Net start W3SVC

2.  若要配置外部 EAC 访问，请在 Exchange 命令行管理程序中运行以下命令。
    
        Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 

3.  若要配置可用性服务，请在 Exchange 命令行管理程序中运行以下命令。
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx

若要验证是否已为 Exchange ActiveSync 或 Outlook Web App 正确配置外部 URL，可以使用远程连接分析器（一种由 Microsoft 免费提供的基于 Web 的工具）。可以在[此处](http://go.microsoft.com/fwlink/?linkid=154308)找到远程连接分析器。

也可以使用 ExRCA 验证是否已为 Exchange ActiveSync 或 Outlook Web App 正确配置了身份验证。

若要验证是否已为 Outlook Web App 正确配置了直接文件访问，请使用公用计算机选项以用户身份登录到 Outlook Web App，然后尝试访问和保存附加到电子邮件的文件。

## 在 Exchange 2007 客户端访问服务器上配置协议

需要运行以下命令来为 Exchange 2007 配置虚拟目录。

  - 若要在 Exchange ActiveSync 虚拟目录上配置外部 URL，请在 Exchange 命令行管理程序中运行以下命令。
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync

  - 若要在 Outlook Web App 虚拟目录上配置外部 URL，请在 Exchange 命令行管理程序中运行以下命令。
    
        Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa

