---
title: '不使用 EdgeSync 的情况下通过边缘传输服务器配置 Internet 邮件流: Exchange 2013 Help'
TOCTitle: 不使用 EdgeSync 的情况下通过边缘传输服务器配置 Internet 邮件流
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61183392
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 不使用 EdgeSync 的情况下通过边缘传输服务器配置 Internet 邮件流

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-01-23_

我们建议您使用边缘订阅过程在 Exchange 组织与边缘传输服务器之间建立邮件流。但是，在某些情况下您可能无法使用边缘订阅过程将边缘传输服务器订阅到 Exchange 组织。若要手动在 Exchange 组织和边缘传输服务器之间建立邮件流，必须在 Exchange 组织中的边缘传输服务器和邮箱服务器上创建和配置发送连接器和接收连接器。

## 开始之前

  - 估计完成该任务的时间：30 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“发送连接器”条目、“发送连接器 - 边缘传输”条目和“接收连接器 - 边缘传输”条目。

  - 此步骤使用基于传输层安全性 (TLS) 的基本身份验证提供加密和身份验证。使用基于 TLS 的基本身份验证时，接收服务器必须安装了 X.509 安全套接字层 (SSL) 服务器证书。在接收连接器上配置的完全限定的域名 (FQDN) 值必须与 SSL 服务器证书中的 FQDN 相匹配。默认情况下，接收连接器上的 FQDN 值就是包含该接收连接器的服务器的 FQDN。

  - 您还可以使用外部保护身份验证方法。但是，如果使用此方法，边缘传输服务器和邮箱服务器之间的通信将不经过 Exchange 的身份验证或加密。我们建议您仅在同时使用其他加密方法的情况下使用外部保护身份验证方法。该加密方法可能是 Internet 协议安全性 (IPsec) 关联或虚拟专用网络 (VPN)。

  - 边缘传输服务器通常为“多宿主”。这意味着边缘传输服务器具有若干个连接到不同网段的网络适配器。其中的每个网络适配器都具有唯一的 IP 配置。连接到外部或公用网段的网络适配器应配置为使用公用域名系统 (DNS) 服务器进行名称解析。这使服务器能够将 SMTP 域名解析为 MX 资源记录并将邮件路由到 Internet。连接到内部或专用网段的网络适配器应配置为使用外围网络中的 DNS 服务器或者应具有可用的 Hosts 文件。

  - 您需要在 Active Directory 中创建用户帐户，并将此帐户添加到 Exchange Server 计算机上的通用安全组。边缘传输服务器上的发送连接器使用此帐户对 Exchange 组织中的目标邮箱服务器进行身份验证。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>该帐户被授予与运行 Exchange Server 的计算机关联的权限。确保保护帐户凭据以避免误用该帐户。可以将该帐户配置为仅允许登录特定的计算机。</td>
    </tr>
    </tbody>
    </table>


## 边缘传输服务器步骤

边缘传输服务器需要以下连接器：

  - 配置为向 Internet 发送邮件的发送连接器

  - 配置为向 Exchange 组织中的邮箱服务器发送邮件的发送连接器

  - 配置为仅从 Exchange 组织中的邮箱服务器接收邮件的接收连接器

  - 配置为仅从 Internet 接收邮件的接收连接器

默认情况下，在安装边缘传输服务器角色的过程中会创建单个接收连接器。此连接器可用于传入的 Internet 邮件和从邮箱服务器传入的邮件。通常，边缘订阅过程在默认的接收连接器上自动配置正确的权限和身份验证。如果您不使用边缘订阅过程，我们建议您将边缘传输服务器上的默认接收连接器修改为仅接受来自 Internet 的邮件。然后，您应在已配置为仅接受来自内部邮箱服务器的邮件的边缘传输服务器上创建一个接收连接器。

以下各节将引导您完成准备边缘传输服务器与 Exchange 组织进行通信所需的所有配置步骤。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只能使用命令行管理程序在边缘传输服务器上执行这些步骤。</td>
</tr>
</tbody>
</table>


## 步骤 1：创建一个配置为向 Internet 发送邮件的发送连接器

此发送连接器要求进行以下配置：

  - **名称**   To Internet（或任何描述性名称）

  - **使用类型**   Internet

  - **地址空间**   “\*”（所有域）

  - **网络设置**   使用 DNS MX 记录自动路由邮件。根据您的网络配置，还可以通过智能主机路由邮件。智能主机将邮件路由到 Internet。

若要创建配置为将邮件发送到 Internet 的发送连接器，请运行以下命令。

    New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true

有关语法和参数的详细信息，请参阅 [New-SendConnector](https://technet.microsoft.com/zh-cn/library/aa998936\(v=exchg.150\))。

## 步骤 2：创建一个配置为向 Exchange 组织发送邮件的发送连接器

使用 **New-SendConnector** cmdlet 创建发送连接器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在创建发送连接器之前，首先需要运行 <strong>Get-Credential</strong> 命令，以保存将在临时变量中使用的用户名和密码。需要执行此操作是因为 <strong>New-SendConnector</strong> cmdlet 不接受纯文本格式的用户凭据。</td>
</tr>
</tbody>
</table>


此发送连接器要求进行以下配置：

  - **名称**   To Internet Org（或任何描述性名称）

  - **使用类型**   内部

  - **地址空间**   Exchange 组织的所有接受域。例如，\*.contoso.com。

  - DNS 路由已禁用（智能主机路由已启用）

  - **智能主机**   一个或多个作为智能主机的邮箱服务器的 FQDN。例如，mbxserver01.contoso.com 和 mbxserver02.contoso.com。

  - **智能主机身份验证方法**   基于 TLS 的基本身份验证

  - **智能主机身份验证凭据**   内部域中用户帐户的凭据。首先需要将用户名和密码保存在临时变量中，因为 **New-SendConnector** cmdlet 不接受纯文本格式的用户凭据。

若要创建配置为将邮件发送到 Exchange 组织的发送连接器，请运行以下命令。

    $MailboxCredentials = Get-Credential
    New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials

有关语法和参数的详细信息，请参阅 [New-SendConnector](https://technet.microsoft.com/zh-cn/library/aa998936\(v=exchg.150\))。

## 步骤 3：将默认接收连接器修改为仅接受来自 Internet 的邮件

应对默认接收连接器进行以下配置更改：

  - 修改名称，以反映该连接器将单独用于接收来自 Internet 的电子邮件。默认接收连接器的名称为“默认内部接收连接器 \<边缘传输服务器名称\>”。

  - 将网络绑定更改为仅接受来自可通过 Internet 访问的网络适配器的邮件。例如，10.1.1.1 和标准 SMTP TCP 端口值 25。

若要将默认接收连接器修改为仅接受来自 Internet 的邮件，请运行以下命令。

    Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25

有关语法和参数的详细信息，请参阅 [Set-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125140\(v=exchg.150\))。

## 步骤 4：创建一个配置为仅接受来自 Exchange 组织的邮件的接收连接器

此接收连接器要求进行以下配置：

  - **名称**   From Internet Org（或任何描述性名称）

  - **使用类型**   内部

  - **本地网络绑定**   面向内部网络的网络适配器。例如，10.1.1.2 和标准 SMTP TCP 端口值 25。

  - **远程网络设置**   Exchange 组织中的一个或多个邮箱服务器的 IP 地址。例如，192.168.5.10 和 192.168.5.20。

  - **身份验证方法**   TLS、基本身份验证、基于 TLS 的基本身份验证和 Exchange Server 身份验证。

若要创建配置为仅接受来自 Exchange 组织的邮件的接收服务器，请运行以下命令。

    New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20

有关语法和参数的详细信息，请参阅 [New-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125139\(v=exchg.150\))。

## 您如何知道这些步骤有效？

若要验证是否已成功配置所需的发送连接器和接收连接器，请在边缘传输服务器上运行以下命令，并验证显示的值是否为您配置的值。

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
    Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges

## 邮箱服务器步骤

组织中的邮箱服务器需要一个配置为将邮件发送到边缘传输服务器以中继到 Internet 的发送连接器。

默认情况下，在安装邮箱服务器角色的过程中会创建两个接收连接器。名为“客户端*服务器名称*”的连接器配置为接受来自所有 POP3 和 IMAP 邮件客户端的邮件。另一个名为“默认*服务器名称*”的连接器配置为接受来自边缘传输服务器的邮件。不需要对这些连接器进行修改。

## 步骤 5：创建配置为向边缘传输服务器发送传出邮件的发送连接器

此发送连接器要求进行以下配置：

  - **名称**   To Edge（或任何描述性名称）

  - **使用类型**   内部

  - **地址空间**   “\*”（所有域）

  - DNS 路由已禁用（智能主机路由已启用）

  - **智能主机**   边缘传输服务器的 IP 地址或 FQDN。例如，edge01.contoso.net。

  - **源邮箱服务器**   一个或多个邮箱服务器的 FQDN。例如，mbxserver01.contoso.com 和 mbxserver02.contoso.com。

  - **智能主机身份验证方法**   基于 TLS 的基本身份验证。

  - **智能主机身份验证凭据**   边缘传输服务器中用户帐户的凭据。首先需要将用户名和密码保存在临时变量中，因为 **New-SendConnector** cmdlet 不接受纯文本格式的用户凭据。

若要创建配置为将传出邮件发送到边缘传输服务器的发送连接器，请运行以下命令。

    $EdgeCredentials = Get-Credential
    New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials

有关语法和参数的详细信息，请参阅 [New-SendConnector](https://technet.microsoft.com/zh-cn/library/aa998936\(v=exchg.150\))。

## 您如何知道此步骤有效？

若要验证是否已成功创建配置为将传出邮件发送到边缘传输服务器的发送连接器，请在邮箱服务器上运行以下命令，并验证显示的值是否为您配置的值。

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism

