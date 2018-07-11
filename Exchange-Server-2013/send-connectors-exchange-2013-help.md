---
title: '发送连接器: Exchange 2013 Help'
TOCTitle: 发送连接器
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 50490761
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 发送连接器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-15_

在 Microsoft Exchange Server 2013 中，发送连接器控制发送到接收服务器的出站邮件流。它们在运行传输服务的邮箱服务器上进行配置。最常见的是，配置发送连接器以将出站电子邮件发送到智能主机或直接发送到其收件人（使用 DNS）。

运行传输服务的 Exchange 2013 邮箱服务器需要发送连接器将邮件传递给到达其目标的途径中的下一个跃点。在邮箱服务器上创建的发送连接器存储在 Active Directory 中，可供组织中运行传输服务的所有邮箱服务器使用。

> [!IMPORTANT]  
> 当部署 Exchange 2013 时，在配置发送连接器以将出站邮件路由到 Internet 之前，无法形成出站邮件流。有关详细信息，请参阅<a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">为发送到 Internet 的电子邮件创建发送连接器</a>。


## 选择发送连接器的类型

通常会在 Exchange 管理中心 (EAC) 的“邮件流”部分中创建发送连接器。在创建新发送连接器时，选择适用于您的连接方案的可用“类型”。类型可确定连接器上分配的默认权限集，并将这些权限授予受信任的安全主体。安全主体包括用户、计算机和安全组。

说明特定“类型”选择的过程包括[创建发送连接器以通过智能主机路由出站电子邮件](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)和[创建“发送连接器”以发送电子邮件给合作伙伴，应用传输层安全性 (TLS)](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md)。

在更喜欢使用 Exchange 命令行管理程序而不是 EAC 时，可以使用 [New-SendConnector](https://technet.microsoft.com/zh-cn/library/aa998936\(v=exchg.150\)) cmdlet 创建发送连接器并指定类型。

## Exchange 2013 中的新发送连接器功能

通过客户端访问服务器上的前端传输服务与邮箱服务器上的传输服务之间的关系，Exchange 2013 提供了用于发送连接器的新行为。首先，可以通过 [Set-SendConnector](https://technet.microsoft.com/zh-cn/library/aa998294\(v=exchg.150\)) cmdlet 的 *FrontEndProxyEnabled* 参数，在邮箱服务器的传输服务中设置发送连接器以通过本地 Active Directory 站点中的前端传输服务器路由出站邮件，从而合并从传输服务路由电子邮件的方式。[邮件路由](mail-routing-exchange-2013-help.md)提供了有关 Exchange 2013 中的传输服务、路由行为和目标的详细信息。[邮件流](mail-flow-exchange-2013-help.md)提供了传输管道的概述和每个传输服务的说明。

*IsCoexistenceConnector* 参数已弃用。在大多数情况下，当要配置混合环境（其中一部分邮箱托管于内部部署上，而另一部分托管于云中）时，建议使用混合配置向导。

*LinkedReceiveConnector* 已弃用。例如，此参数曾用于创建可以将邮件路由到第三方反垃圾邮件服务的连接器。目前，在大多数情况下，会通过 MX 记录将邮件路由到反垃圾邮件服务，而不需要链接连接器行为。

通过 *MaxMessageSize* 参数指定的默认最大邮件大小已从 10MB 增加到 25MB。[Set-SendConnector](https://technet.microsoft.com/zh-cn/library/aa998294\(v=exchg.150\)) 提供了有关如何对发送连接器设置参数的详细信息。

添加了 *TlsCertificateName*。它用于对要用于出站连接的本地证书进行身份验证并在最大程度上减少欺诈性证书的风险。

