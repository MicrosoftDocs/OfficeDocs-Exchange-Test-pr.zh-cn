---
title: '接收连接器: Exchange 2013 Help'
TOCTitle: 接收连接器
ms:assetid: 17751a60-39fe-433f-84d2-bfc14ff4ba51
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996395(v=EXCHG.150)
ms:contentKeyID: 50490095
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 接收连接器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-07_

接收连接器控制发送到 Exchange 组织的入站邮件流。会在具有传输服务的运行 Microsoft Exchange Server 2013 的计算机上，或是在客户端访问服务器上的前端服务中配置这些控制器。可以在 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序中创建它们。

默认情况下，安装客户端访问服务器或邮箱服务器时，将自动创建内部邮件流所需的接收连接器。

运行传输服务的 Exchange 2013 服务器需要接收连接器从 Internet、电子邮件客户端和其他电子邮件服务器接收邮件。接收连接器控制与 Exchange 组织的入站连接。

每个接收连接器都会侦听与接收连接器的设置相匹配的入站连接。接收连接器会侦听通过特定的本地 IP 地址和端口接收的、来自指定 IP 地址范围的连接。当要控制哪些服务器接收来自特定 IP 地址或 IP 地址范围的邮件时，以及当要针对从特定 IP 地址接收的邮件来配置特殊的连接器属性（如允许更大邮件或每个邮件更多收件人）时，可以创建接收连接器。还可以使用 **Set-ReceiveConnector** cmdlet 的 *TlsCertificateName* 参数限定接收连接器作用域，这使您可以指定要用于连接器的证书。

接收连接器的作用域限于单台服务器，可确定该特定服务器如何侦听连接。在运行传输服务的邮箱服务器上创建接收连接器时，该接收连接器会作为其所在服务器的子对象存储在 Active Directory 中。

如果特定方案需要使用其他的接收连接器，可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序创建所需的接收连接器。每个接收连接器必须使用绑定的 IP 地址、分配的端口号和远程 IP 地址范围（接受来自这些 IP 地址的邮件）的唯一组合。

有关如何创建接收连接器的详细信息，请参阅[接收连接器步骤](receive-connector-procedures-exchange-2013-help.md)。

**目录**

安装过程中创建的默认接收连接器

在运行传输服务的邮箱服务器上创建的默认接收连接器

前端传输服务器上创建的默认接收连接器

接收连接器类型

接收连接器权限组

接收连接器类型规范

接收连接器权限

接收连接器身份验证设置

Exchange 2013 中的新接收连接器功能

## 安装过程中创建的默认接收连接器

安装邮箱服务器角色时，默认情况下将创建某些接收连接器。

## 在运行传输服务的邮箱服务器上创建的默认接收连接器

安装运行传输服务的邮箱服务器时，将创建两个接收连接器。典型操作中无需其他的接收连接器，且大多数情况下不必对默认的接收连接器进行配置更改。这些连接器如下：

  - **默认 \<服务器名称\>**   接受来自运行传输服务的邮箱服务器和来自边缘服务器的连接。

  - **客户端代理 \<服务器名称\>**   接受来自前端服务器的连接。通常，邮件会通过 SMTP 发送到前端服务器。

会向每个连接器分配一个 *TransportRole* 值。可以使用该值确定连接器运行时所属的角色。如果在单个服务器上运行多个角色，则这可能会十分有用。对于前面提到的每个接收连接器，其 *TransportRole* 值为 **HubTransport**。

若要查看默认接收连接器及其参数值，可以使用 [Get-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/aa998618\(v=exchg.150\)) cmdlet。

## 前端传输服务器上创建的默认接收连接器

在安装期间，将在前端传输或客户端访问服务器上创建三个接收连接器。默认前端接收连接器会配置为接受来自所有 IP 地址范围的 SMTP 通信。此外，还有一个接收连接器可以充当从邮箱服务器发送到前端服务器的邮件的出站代理。最后，有一个安全接收连接器，配置为接受使用传输层安全性 (TLS) 加密的邮件。这些连接器如下：

  - **默认前端 \<服务器名称\>**   通过端口 25 接受来自 SMTP 发件人的连接。这是进入组织的常用邮件入口点。

  - **出站代理前端 \<服务器名称\>**   接受来自后端服务器（启用了前端代理）上的发送连接器的邮件。

  - **客户端前端 \<服务器名称\>**   接受应用了传输层安全性 (TLS) 的安全连接。

在典型安装中，不需要其他接收连接器。

## 接收连接器类型

此类型可确定每个接收连接器的默认安全设置。

接收连接器的安全设置可指定向连接到接收连接器的会话授予的权限以及支持的身份验证机制。

使用 EAC 配置接收连接器时，新建接收连接器页面会提示您选择连接器的类型。根据您进行的选择，可以对参数进行设置，以符合所选配置。特定过程包含有关接收连接器类型设置的详细信息。这些过程的示例有[通过互联网创建接收连接器接收电子邮件](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)和[创建安全接收连接器以从合作伙伴接收电子邮件](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)。

## 接收连接器权限组

权限组是预定义的权限集，将其授予常用的安全主体并分配给接收连接器。安全主体包括用户、计算机和安全组。使用权限组可以简化接收连接器的权限配置操作。**PermissionGroups** 属性定义可将邮件提交给接收连接器的组或角色以及分配给这些组的权限。

权限组包括 *Anonymous*、*ExchangeUsers*、*ExchangeServers*、*ExchangeLegacyServers* 和 *Partner*。

## 接收连接器类型规范

此类型可确定分配给接收连接器的默认权限组，以及可用于会话身份验证的默认身份验证机制。下面的列表描述了可用类型：

1.  **客户端**   通常用于连接到不使用 Microsoft Office Outlook 的客户端。它可以使用 TLS 身份验证。

2.  **自定义**   通常用于跨林方案，或是组织从 SMTP 邮件传输代理接收邮件的方案。

3.  **内部**   用于运行传输服务的服务器之间或是运行传输服务的邮箱服务器与第三方传输代理之间的通信。

4.  **Internet**   用于从 Internet 接收 SMTP 邮件。

5.  **合作伙伴**   在要配置与某个合作伙伴进行安全通信时可使用此类型。

每种类型都适用于特定的连接方案。请选择默认设置最适合所需配置的类型。可以使用 **Add-ADPermission** cmdlet 和 **Remove-ADPermission** cmdlet 修改权限。有关详细信息，请参阅下列主题：

  - [Add-ADPermission](https://technet.microsoft.com/zh-cn/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-cn/library/aa996048\(v=exchg.150\))

## 接收连接器权限

为接收连接器指定权限组时，会将接收连接器权限分配给安全主体。某个安全主体与接收连接器建立会话时，接收连接器权限将决定是否接受该会话以及如何处理收到的邮件。您可使用 EAC 或在命令行管理程序中结合使用 *PermissionGroups* 参数与 **Set-ReceiveConnector** cmdlet 来设置接收连接器的权限。若要修改接收连接器的默认权限，还可以使用 **Add-ADPermission** cmdlet。

[接收连接器权限](receive-connector-permissions-exchange-2013-help.md)包含一个表，其中详细列出了安全主体和权限类型。

## 接收连接器身份验证设置

在 EAC 中，可以对接收连接器使用身份验证设置，以指定 Exchange 2013 传输服务器所支持的身份验证机制。在命令行管理程序中，可以使用 *AuthMechanisms* 参数来指定所支持的身份验证机制。可以为一个接收连接器配置多种身份验证机制。有关详细信息，请参阅[接收连接器身份验证机制](receive-connector-authentication-mechanisms-exchange-2013-help.md)。

## Exchange 2013 中的新接收连接器功能

Exchange 2013 中添加了以下功能：

  - 通过 *TlsCertificateName* 参数，可以指定要用于安全邮件的本地证书颁发机构 (CA) 颁发的证书。这有助于将欺诈证书的风险降到最低。

  - *TransportRole* 参数指定与此连接器关联服务器角色。它通常用于在单台计算机上承载多个服务器角色时指定服务器角色。

有关接收连接器的这些参数及其他参数的详细信息，请参阅 [New-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125139\(v=exchg.150\))。

