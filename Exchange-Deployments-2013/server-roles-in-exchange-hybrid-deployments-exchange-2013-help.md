---
title: 'Exchange 混合部署中的服务器角色: Exchange 2013 Help'
TOCTitle: Exchange 混合部署中的服务器角色
ms:assetid: 7a7eaf17-d2b0-4d62-90a2-45a0d2faca54
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ659051(v=EXCHG.150)
ms:contentKeyID: 50492079
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 混合部署中的服务器角色

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

您可以配置基于 Exchange 2013 和 Exchange 2016 的混合部署。支持混合部署需要配置的角色取决于您使用的 Exchange 版本。

## Exchange 2016 混合部署

在 Exchange 2016 组织中配置混合部署时，无需在现有 Exchange 组织中安装任何额外的 Exchange 服务器。您的邮箱服务器将协调现有 Exchange 2016 组织和 Exchange Online 组织之间的通信。此通信包括本地组织与 Exchange Online 组织之间的邮件传输和消息功能。我们强烈建议在本地组织中安装多个 Exchange 服务器，以帮助提高混合部署功能的可靠性和可用性。

Exchange 2016 只有一个必需的服务器角色 - 邮箱角色。除了托管本地收件人邮箱，邮箱角色还执行所有使用 Exchange Online 支持混合部署所必需的功能。这包括处理本地组织和 Exchange Online 组织之间的安全邮件以及处理传输规则、日志记录策略和向用户的混合部署邮箱中执行的邮件传递操作。所有客户端连接和组织的关系功能（如忙/闲共享）也由邮箱服务器处理。

了解有关 [Exchange 2016 部署的大小调整](http://go.microsoft.com/fwlink/p/?linkid=301990)的 Exchange 2016 容量规划的详细信息。

## Exchange 2013 混合部署

在 Exchange 2013 组织中配置混合部署时，无需在现有 Exchange 组织中安装任何额外的 Exchange 服务器。您的客户端访问和邮箱服务器将协调现有 Exchange 2013 组织和 Exchange Online 组织之间的通信。此通信包括内部部署组织与 Exchange Online 组织之间的邮件传输和消息功能。我们强烈建议在内部部署组织中安装多个 Exchange 服务器，以帮助提高混合部署功能的可靠性和可用性。

下面是混合部署中的 Exchange 2013 服务器角色的快速概述：

  - **客户端访问服务器角色**   客户端访问服务器角色继续提供实际上是 Exchange 2013 组织中的客户端访问服务器提供的相同功能，外加支持混合部署所需的少量其他功能。客户端访问服务器还处理在内部部署和 Exchange Online 组织之间发送的所有安全邮件消息，以及处理混合部署中的传输规则、日记策略和到用户邮箱的邮件传递。默认情况下，在客户端访问服务器上配置有专门的接收连接器以支持安全混合邮件传输。所有客户端连接（包括 Outlook 客户端访问、Outlook Web App 和 Outlook Anywhere）都通过客户端访问服务器角色进行。内部部署组织与 Exchange Online 组织之间的组织关系功能（如忙/闲共享）也由客户端访问服务器角色处理。
    
    有关详细信息，请参阅 [客户端访问服务器](https://technet.microsoft.com/zh-cn/library/dd298114\(v=exchg.150\))。

  - “邮箱服务器角色”   邮箱服务器角色托管内部部署收件人邮箱，并通过内部部署客户端访问服务器的代理与 Exchange Online 组织通信。默认情况下，在邮箱服务器角色上配置有专门的发送连接器以支持安全混合邮件传输。
    
    有关详细信息，请参阅 [邮箱服务器](https://technet.microsoft.com/zh-cn/library/jj150491\(v=exchg.150\))。

根据所需的混合部署配置，Exchange 2013 服务器需要安装一个或两个服务器角色：

  - **单个 Exchange 服务器**   如果选择在您的内部部署组织中安装单个 Exchange 服务器，则需要在该单个服务器上同时安装客户端访问和邮箱服务器角色。

  - **多个 Exchange 服务器**   如果选择在您的内部部署组织中安装多个 Exchange 服务器，则可在内部部署组织中的单独服务器上安装服务器角色。例如，可以安装一个安装了邮箱和客户端访问服务器角色的 Exchange 服务器，同时也再安装一个仅安装了客户端访问服务器角色的 Exchange 服务器。但是，最佳实践及推荐的服务器配置是在内部部署组织中部署的*每个*服务器上同时安装客户端访问和邮箱服务器。

有关 Exchange 2013 容量规则的详细信息，请参阅[了解容量规划中的多个服务器角色配置](http://go.microsoft.com/fwlink/?linkid=266576)。

## 混合部署中的 Exchange 服务器功能

Exchange 服务器为混合部署中的内部部署组织提供了几个重要功能：

  - **联合身份验证**   使用 Exchange 服务器，可以通过 Microsoft 联合网关为本地组织创建联合身份验证信任。Microsoft 联合网关是 Microsoft 提供的一项基于云的免费服务，该服务可充当本地组织与 Office 365 组织之间的信任代理。联合身份验证是关于在本地组织与 Exchange Online 组织之间创建组织关系的要求。
    
    有关详细信息，请参阅 [联盟](https://technet.microsoft.com/zh-cn/library/dd335047\(v=exchg.150\))。

  - **组织关系**   具有客户端访问角色的 Exchange 2013 服务器和具有邮箱角色的 Exchange 2016 服务器支持创建本地组织与 Exchange Online 组织之间的组织关系。混合部署中的许多其他服务（包括日历忙/闲信息共享、邮件跟踪以及本地组织与 Exchange Online 组织之间的邮箱移动）需要组织关系。
    
    有关详细信息，请参阅 [共享](https://technet.microsoft.com/zh-cn/library/dd638083\(v=exchg.150\))。

  - “邮件传输”   具有客户端访问和邮箱服务器角色的 Exchange 服务器负责混合部署中的邮件传输。通过使用发送和接收连接器，这些服务器可用作传入外部邮件的连接终结点，并提供到 Internet 和 Exchange Online 组织的出站邮件传递。
    
    有关详细信息，请参阅 [Exchange 混合部署的传输选项](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)。

  - **邮件传输安全**   具有客户端访问和邮箱服务器角色的 Exchange 服务器可使用 Exchange 中的域安全功能，帮助保护内部部署组织与 Exchange Online 组织之间的邮件通信安全。可以通过将相互传输层安全性身份验证和加密用于邮件通信，来增强安全。
    
    有关更多信息，请参阅[了解域安全性](http://go.microsoft.com/fwlink/p/?linkid=266581)。

  - **Web 上的 Outlook（也称作 Exchange 2013 中的 Outlook Web App）**   具有客户端访问角色的 Exchange 2013 服务器和具有邮箱角色的 Exchange 2016 服务器支持为与本地邮箱和 Exchange Online 邮箱之间存在的外部连接配置单个 URL 终结点。对于本地邮箱，Exchange 服务器被配置为 Web 上的 Outlook 请求。对于 Exchange Online 组织邮箱，Exchange 服务器被配置为自动显示到 Exchange Online 组织上的 Web 上的 Outlook 终结点的链接。
    
    有关详细信息，请参阅 [Outlook Web App](https://technet.microsoft.com/zh-cn/library/jj657718\(v=exchg.150\))。

