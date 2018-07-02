---
title: '混合部署故障排除: Exchange 2013 Help'
TOCTitle: 混合部署故障排除
ms:assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ659053(v=EXCHG.150)
ms:contentKeyID: 50492082
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合部署故障排除

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-04-29_

在 Exchange 中使用混合配置向导配置混合部署将极大减少混合部署出现问题的可能性。然而，这里有一些混合配置向导范围之外的典型区域，如果配置不当的话，可能导致混合部署出现问题。本主题将讨论可能出现问题的以下常见区域，并介绍验证或修正问题的基本步骤：

  - 本地 Exchange 服务器

  - 证书

  - 混合配置向导的具体错误

> [!NOTE]
> 在本主题中，“Exchange 服务器”指的是下列服务器：
> <ul>
> <li><p><strong>客户端访问服务器</strong> Exchange 2013 及之前版本</p></li>
> <li><p><strong>邮箱服务器</strong> Exchange 2016 及更高版本</p></li></ul>

有关其他信息，请参阅 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

关于混合部署的更多管理任务，参阅 [Hybrid Deployment procedures](hybrid-deployment-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：因混合部署问题的类型而异

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](https://technet.microsoft.com/zh-cn/library/dd638114\(v=exchg.150\))主题中的“混合部署”条目。

  - 本主题中的指导适用于使用混合配置向导配置的混合部署。不支持手动配置的混合部署。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](https://technet.microsoft.com/zh-cn/library/jj150484\(v=exchg.150\))。

> [!TIP]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 要执行什么操作？

## 内部部署 Exchange 服务器故障排除

内部部署 Exchange 服务器的配置通常是混合配置最有可能出现问题的区域。通常，需要检查的区域包括：

  - **可用性**   正确发布内部部署 Exchange 服务器到 Internet 对于在混合部署中正常运行的功能来说至关重要。为了使混合功能正常运行，您必须配置内部部署防火墙或其他安全设备，以允许从 Internet 到内部部署 Exchange 服务器上的自动发现和 Exchange Web Services (EWS) 终结点的入站访问。此外，还必须配置 Exchange 服务器以接受入站 SMTP 邮件。如果 Office 365 租户组织中包含的 Microsoft Exchange Online Protection (EOP) 服务无法到达内部部署 Exchange 服务器，从 Exchange Online 组织到内部部署组织的安全邮件可能无法正常运行。

  - **证书**   用于内部部署和 Exchange Online 组织之间的安全邮件传输的数字证书必须安装在将与 Exchange Online 通信的面向 Internet 的所有内部部署 Exchange 服务器上、必须由第三方证书颁发机构 (CA) 颁发、不得到期，同时必须分配有 IIS 和 SMTP 服务。如果未满足这些证书要求，将无法正常运行从 Exchange Online 组织到内部部署组织的安全邮件传输。本主题后面的“解决证书问题”提供了有关证书要求的详细信息。

## 如何知道您的 Exchange 服务器配置是否正确？

要验证您已成功发布内部部署 Exchange 服务器，使用 Microsoft Remote Connectivity Analyzer 验证内部部署 Exchange 服务器的入站 Internet 连接。请执行以下操作：

1.  转到[远程连接分析器](https://www.testexchangeconnectivity.com/)工具。

2.  该步骤用于 EWS 任务的常规测试，以确认它们是否正常运行，同时已配置 EWS 终结点。
    
    运行“Microsoft Exchange Web 服务连接性测试”部分的“同步、通知、可用性和自动回复 (OOF)”部分，并验证没有任何错误。如果发生错误，更正测试确定的项目。

3.  该步骤用于自动发现服务的常规测试，以确认它们是否正常运行，同时已配置自动服务终结点。
    
    运行“Microsoft Office Outlook 连接性测试”部分的“Outlook 自动发现”测试，并验证没有任何错误。如果发生错误，更正测试确定的项目。

4.  该步骤用于 SMTP 连接性的一般测试，并确认 Exchange 服务器可以接收入站 Internet 邮件。
    
    运行“Internet 电子邮件测试”部分的“入站 SMTP 电子邮件”测试，并验证没有任何错误。如果发生错误，更正测试确定的项目。

## 证书问题故障排除

在内部部署 Exchange 服务器上安装的证书配置可能导致混合部署发生问题。在大多数情况下，以下证书相关问题将影响混合功能：

  - **证书类型**   用于安全混合传输并在混合配置向导中定义的数字证书必须由第三方 CA 颁发。自签名证书必须不得用于混合传输身份验证。如果无意中选择或分配自签名证书，Exchange Online 和内部部署组织之间的安全邮件传输将无法正常运行。

  - **分配的服务**   Internet 信息服务 (IIS) 和简单邮件传输协议 (SMTP) 服务必须被分配给用于混合传输的数字证书。如果未分配这些服务，Exchange Online 组织和内部部署组织之间的安全邮件传输将无法正常运行。

  - **安装**   必须在所有内部部署 Exchange 服务器上安装用于在内部部署和 Exchange Online 组织之间进行安全邮件传输的数字证书。如果您正为内部部署边缘传输服务器部署混合部署，数字证书还必须安装在您的边缘传输服务器上。如果未在内部部署服务器上安装证书，Exchange Online 和内部部署组织之间的安全邮件传输将无法正常运行。

  - **到期**   用于内部部署和 Exchange Online 组织之间的安全邮件传输的数字证书必须不得到期。如果证书到期，Exchange Online 组织和内部部署组织之间的安全邮件传输将无法正常运行。

## 如何知道您的证书是否正确配置？

要验证用于内部部署 Exchange 服务器的混合邮件传输证书正确配置，请执行以下操作：

1.  在本地 Exchangex 服务器，打开Exchange 命令行管理程序

2.  在Exchange 命令行管理程序中，运行以下命令。
    
        Get-ExchangeCertificate| format-list

3.  查找您在用于安全邮件传输的混合配置向导中定义证书的信息。

4.  验证已分配以下参数值给证书：
    
      - “IsSelfSigned 参数”   此参数值应为 *False*。
    
      - “RootCAType 参数”   此参数值应为 *Third Party*。
    
      - “服务参数”   此参数值应为 *IIS, SMTP*。
    
      - “NotAfter 参数”   此参数值是证书到期日期。这里列出的日期不应到期。

## 混合配置向导的具体错误疑难解答

如果您在运行混合配置向导时收到错误，通常可以通过执行若干简单的检查或操作来解决问题。关于解决在运行混合配置向导时可能遇到的具体消息或问题，请参阅以下建议。

  - **消息：“在服务器 \<服务器名称\> 上找不到默认接收连接器”**   当下列属性中所列的任一 Exchange 服务器上的接收连接器未在 TCP 端口 25 上侦听 IPv4 和 IPv6 协议时，会出现此消息：`(Get-HybridConfiguration).ReceivingTransportServers.`
    
      -  
        若要在运行 `(Get-HybridConfiguration).ReceivingTransportServers.` 时验证所列 Exchange 服务器上的接收连接器是否绑定正确，可以在Exchange 命令行管理程序中运行以下命令。
        
            Get-ReceiveConnector -Server <Server Name> | FT Identity, Bindings
        
        您应当查看针对 Exchange 服务器所列的下列条目：`{[::]:25, 0.0.0.0:25}`
        
        如果绑定未列出，您需要使用 **Set-ReceiveConnector** cmdlet 的 *Bindings* 参数将其添加至接收连接器。有关详细信息，请参阅 [Set-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125140\(v=exchg.150\))。

