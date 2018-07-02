---
title: 'Exchange 2013/Exchange 2010 混合部署中的传输选项: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 混合部署中的传输选项
ms:assetid: 57f93b81-d153-4f0d-81f6-085130319803
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn393960(v=EXCHG.150)
ms:contentKeyID: 59636468
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 混合部署中的传输选项

本主题正在进行。  

_<strong>适用于：</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>上一次修改主题：</strong>2016-12-09_

在混合部署中，可以具有既驻留在内部部署 Exchange 组织中也驻留在 Exchange Online 组织中的邮箱。为了使这两个单独组织对用户及在他们之间交换的邮件表现为一个合并的组织，关键组件是混合传输。通过混合传输，在任一组织中的收件人之间发送的邮件会经过身份验证、加密并使用传输层安全性 (TLS) 传输，并且向 Exchange 组件（如传输规则、日记和反垃圾邮件策略）显示为“内部”。混合传输由 Exchange 2013 中的混合配置向导自动配置

为了在混合配置向导中使用混合传输配置，接受来自 Microsoft Exchange Online Protection (EOP)（用于处理 Exchange Online 组织的传输）的连接的本地 SMTP 终结点必须是 Exchange 2013 客户端访问服务器、Exchange 2013 边缘传输服务器或 Exchange Server 2010 SP3 边缘传输服务器。

> [!IMPORTANT]
> 本地 Exchange 2013 客户端访问服务器或 Exchange 2013/Exchange 2010 SP3 边缘传输服务器与 EOP 之间可以没有任何其他 SMTP 主机或服务。当邮件经过非 Exchange 2013 服务器、预 Exchange 2010 SP3 服务器或 SMTP 主机时，会删除添加到邮件中用于启用混合传输功能的信息。如果在组织中部署了 Exchange 2010 SP2 边缘传输服务器，并且要将这些服务器用于混合传输，则它们必须升级到 Exchange 2010 SP3。


从外部 Internet 发件人发送到两个组织中的收件人的入站邮件会采用通用入站路由。从组织发送到外部 Internet 收件人的出站邮件可以采用通用出站路由，也可以通过独立的路由发送。

在计划和配置混合部署时需要选择如何路由入站和出站邮件。发送到和发送自内部部署和 Exchange Online 组织中收件人的入站和出站邮件采用的路由取决于以下因素：

  - 您是否希望通过 Microsoft Office 365 和 EOP 或内部部署组织路由内部部署和 Exchange Online 邮箱的入站 Internet 邮件？
    
    可以选择通过内部部署组织或通过 EOP 和 Exchange Online 组织为两个组织路由入站 Internet 邮件。两个组织入站邮件的路由取决于是否在混合部署中启用了集中邮件传输。

  - 是要通过内部部署组织（集中邮件传输）路由来自 Exchange Online 组织的出站邮件到外部收件人，还是要将其直接路由到 Internet？
    
    作为集中邮件传输，可以先通过内部部署组织路由来自 Exchange Online 组织中邮箱的所有邮件，然后再将这些邮件传递到 Internet。此方法用于合规性方案，在这类方案中，发送到和发送自 Internet 的所有邮件都必须由内部部署服务器进行处理。或者，可以配置 Exchange Online 以将外部收件人的邮件直接传递到 Internet。
    
    > [!NOTE]
    > 仅对具有与符合性相关的特定传输需求的组织推荐使用集中式邮件传输。我们建议典型的 Exchange 组织不要启用集中式邮件传输。


  - 是否要在内部部署组织中部署边缘传输服务器？
    
    如果您不想将加入域的内部 Exchange 2013 服务器直接向 Internet 公开，则可在外围网络中部署 Exchange 2013 边缘传输服务器或 Exchange 2010 SP3 边缘传输服务器。有关向混合部署添加边缘传输服务器的详细信息，请参阅 [Exchange 2013/Exchange 2010 混合部署中的边缘传输服务器](edge-transport-servers-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md)。

无论如何路由发送到和发送自 Internet 的邮件，在内部部署与 Exchange Online 组织之间发送的所有邮件都使用安全传输进行发送。有关详细信息，请参阅本主题后面的[受信任通信](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)。

有关这些选项如何影响您的组织中的邮件路由的详细信息，请参阅[Exchange 2013/Exchange 2010 混合部署中的传输路由](transport-routing-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md)。

## 混合部署中的 Exchange Online Protection

EOP 是 Microsoft 提供的联机服务，由许多公司用于保护其内部部署组织免受病毒、垃圾邮件、欺诈邮件和策略违规的危害。在 Office 365 中，EOP 用于保护 Exchange Online 组织免受相同威胁的危害。在注册 Office 365 时，会自动创建与您的 Exchange Online 组织关联的 EOP 公司。

EOP 公司包含一些邮件传输设置，可以为 Exchange Online 组织配置这些设置。可以指定哪些 SMTP 域必须来自特定 IP 地址，需要 TLS 和安全套接字层 (SSL) 证书，可以绕过合规性策略，等等。EOP 是 Exchange Online 组织的前门。所有邮件（无论其来源如何）都必须先经过 EOP，然后才能到达 Exchange Online 组织中的邮箱。而且，从 Exchange Online 组织发送的所有邮件都必须先经过 EOP，然后才能到达 Internet。

在使用混合配置向导配置混合部署时，会在内部部署组织以及为 Exchange Online 组织设置的 EOP 公司中自动配置所有传输设置。混合配置向导会在此 EOP 公司中配置所有入站和出站连接器及其他设置，以保护在内部部署与 Exchange Online 组织之间发送的邮件并将邮件路由到正确目标。如果要为 Exchange Online 组织配置自定义传输设置，则也会在此 EOP 公司中配置这些设置。

## 受信任通信

为了帮助保护内部部署和 Exchange Online 组织中的收件人，并帮助确保不会截获和读取组织之间发送的邮件，内部部署组织与 EOP 之间的传输会配置为使用强制 TLS。TLS 传输使用受信任第三方证书颁发机构 (CA) 提供的安全套接字层 (SSL) 证书。EOP 与 Exchange Online 组织之间的邮件也使用 TLS。

当使用强制 TLS 传输时，发送和接收服务器会检查在其他服务器上配置的证书。对证书配置的使用者名称或使用者替代名称 (SAN) 之一，必须与管理员在其他服务器上显式指定的 FQDN 匹配。例如，如果 EOP 配置为接受并保护从 mail.contoso.com FQDN 发送的邮件，则发送内部部署客户端访问或边缘传输服务器必须具有在主题名称或 SAN 中包含 mail.contoso.com 的 SSL 证书。如果不满足此要求，则 EOP 会拒绝连接。

> [!NOTE]
> 使用的 FQDN 无需与收件人的电子邮件域名匹配。唯一要求在于证书主题名称或 SAN 中的 FQDN 必须与接收或发送服务器配置为接受的 FQDN 匹配。


除了使用 TLS 以外，还可将组织之间的邮件作为“内部”邮件处理。此方法使邮件可以绕过反垃圾邮件设置和其他服务。

有关 SSL 证书和域安全性的详细信息，请参阅 [混合部署的证书要求](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) 和 [了解 TLS 证书](http://go.microsoft.com/fwlink/p/?linkid=187237)。

