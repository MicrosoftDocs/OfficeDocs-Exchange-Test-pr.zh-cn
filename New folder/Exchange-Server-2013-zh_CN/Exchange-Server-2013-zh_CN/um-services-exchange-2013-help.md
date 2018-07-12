---
title: 'UM 服务: Exchange 2013 Help'
TOCTitle: UM 服务
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50556685
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 服务

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-18_

通过运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器和运行 Microsoft Exchange 统一消息服务的邮箱服务器，可以为组织中的用户部署统一消息 (UM) 和语音邮件功能。

寻找与 UM 服务有关的管理任务？请参阅[UM 服务过程](um-services-procedures-exchange-2013-help.md)。

**目录**

Client Access and Mailbox servers

Server configuration settings

Server operation

## 客户端访问和邮箱服务器

在 Exchange 2013 中，Exchange 2007 和 Exchange 2010 中的服务器角色合并为两种服务器类型，来自这些服务器角色的所有组件或服务都在相同物理服务器上或在两个称为\&quot;客户端访问\&quot;和\&quot;邮箱\&quot;的单独服务器上运行。

在新模型中，客户端访问服务器负责自动发现、 安全套接字层 (SSL)、 身份验证、 重定向和代理。客户端访问服务器是任何入站调用的入口点或会话启动协议 (SIP) 统一消息的请求。作为自动包含在客户端访问服务器的服务实现的路由逻辑和 SIP 重定向。此项服务被称为 Microsoft Exchange 统一消息呼叫路由器服务。它在您的组织中的每个客户端访问服务器上运行。

当客户端访问服务器接收 SIP 邀请来电时，Microsoft Exchange 统一消息呼叫路由器服务将重定向到邮箱服务器传入的呼叫。然后 VoIP 网关，IP PBX 或会话边框控制器 (SBC) 和承载用户的邮箱的邮箱服务器之间建立一个媒体信道 （RTP 或 SRTP）。尽管客户端访问服务器作为 SIP 重定向器，它只处理 VoIP 网关，IP Pbx 或 SBCs 中的 SIP 请求。该组件不接收任何介质流量。邮箱服务器和 SIP 对等端如 VoIP 网关，IP Pbx 或 SBCs 之间传递使用 RTP 或 srtp 结合媒体通信。Exchange 2013和 UM 部署时，您必须配置您的 VoIP 网关，IP Pbx 或 SBCs 指向您已安装，以便将 um 正确路由传入呼叫的客户端访问服务器。

在Exchange 2013，邮箱服务器处理相同的流程与处理Exchange 2007和Exchange 2010中的统一消息服务器角色。邮箱服务器运行的 Microsoft Exchange 统一消息服务和 UM 工作进程。

当您安装客户端访问和邮箱服务器，并且部署统一消息时，您不必将相关联或添加客户端访问或邮箱服务器与 UM 拨号计划。客户端访问和邮箱服务器应答所有传入呼叫，然后使用 UM 拨号计划来查找用户。

但是，如果正在使用 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync Server 集成统一消息，SIP 和 RTP 或 SRTP 传媒渠道，以拨入呼叫处理通过 Lync 服务器和邮箱服务器。在 Lync 集成环境中，您没有 VoIP 网关，IP Pbx 或 SBCs。Lync，到邮箱服务器运行 Microsoft Exchange 统一消息服务看起来就像一个Exchange 2010 UM 服务器。邮箱服务器和客户端访问服务器被认为是受信任的同事，因为两个服务器必须添加到 SIP 拨号计划。Lync 将路由使用入站路由组件，使用 SIP 来与客户端访问服务器通信，然后路由到邮箱服务器呼叫的传入呼叫。

返回顶部

## 服务器配置设置

在Exchange 2013，所有 UM 组件和配置设置应用到一台运行在Exchange 2010中的统一消息服务器角色都都仍然可用。但是，这些组件和配置设置的一些发现客户端访问服务器上和其他人的邮箱服务器上可用。在某些情况下上两者都, 提供了相同的设置。下面的列表显示的参数和设置的客户端访问服务器和邮箱服务器上可用。

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \<Int32\>\]

  - \[-SipTcpListeningPort \<Int32\>\]

  - \[-SipTlsListeningPort \<Int32\>\]

  - \[-Status \<Enabled | Disabled | NoNewCalls\>\]

  - \[-UMStartupMode \<TCP | TLS | Dual\>\]

邮箱服务器，您将使用的**Set-UMService**、 **Get-UMService**、 **Enable-UMService**和**Disable-UMService** cmdlet 以查看或配置 Microsoft Exchange 统一消息服务的 UM 属性。一组不同的 cmdlet、 **Set-UMCallRouterSettings**和**Get-UMCallRouterSettings**，用于查看或配置客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务的属性。这将确保现有的**Get-UMServer**、 **Set-UMServer**、 **Enable-UMServer**和**Disable-UMServer**从Exchange 2007和Exchange 2010的 cmdlet 将共存与Exchange 2013邮箱服务器部署中正常工作。这还可以确保这些 cmdlet 起时在相同或不同的计算机上安装了邮箱服务器和客户端访问服务器。

返回顶部

## 服务器操作

在安装客户端访问服务器和邮箱服务器时，会自动将它们启用，因此它们可以应答传入和传出语音呼叫，以及将语音邮件消息路由给 Exchange 组织中的预期收件人。

您可以允许在邮箱服务器上的 Microsoft Exchange 统一消息服务或回答新的呼叫的客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务或阻止它这样做。默认情况下，邮箱或客户端访问服务器处于启用状态安装后。在设置邮箱或客户端访问服务器接受传入的语音、 传真、 自动助理和 Outlook Voice Access 调用时，您可以使用**Set-ServerComponentState** cmdlet。

Exchange 2013邮箱或客户端访问服务器配置维护模式，可以使服务器停止服务。邮箱服务器，出服务意味着服务器不承载任何活动的数据库，所有传输队列都是空的并且服务器将不接受任何来电从客户端访问服务器、 VoIP 网关，IP Pbx、 SIP 启用 Pbx 或 SBCs。对于客户端访问服务器，出服务意味着服务器不接受 VoIP 网关，IP Pbx、 SIP 启用 Pbx 或 SBCs 从任何拨入呼叫。

在Exchange 2007和Exchange 2010中，没有一个状态参数，可用于控制统一消息服务器的运行状态。在Exchange 2013，无状态参数是可为此目的在**Set-UMService** cmdlet 邮箱服务器或客户端访问服务器上的**Set-UMCallRouterSettings** cmdlet。

虽然客户端访问服务器和邮箱服务器在其安装时就设置为启用，但在 UM 拨号计划至少与一个 UM IP 网关关联之前，两种服务器都无法正确地对至启用 UM 的用户的传入呼叫进行处理和路由。

拨号计划与 UM IP 网关后，在客户端访问、 邮箱服务器定位与 UM 拨号计划和 VoIP 网关，IP Pbx 和 SBCs 相关联的所有 UM IP 网关。检测和识别在 UM 拨号计划或 UM IP 网关的任何配置更改，客户端访问或邮箱服务器，请检查配置每隔 10 分钟。

如果 UM IP 网关标识对配置进行任何更改，该客户端访问或邮箱服务器进行相应，并开始使用或停止使用相应的 VoIP 网关，IP PBX 或 SBC。在客户端访问、 邮箱服务器应答传入后求助用户链接与 UM 拨号计划，它们正确的通信与 VoIP 网关，IP Pbx 和 SBCs，您可以运行一组诊断操作，以验证正在正常运行，并且 Exchange 服务器和 VoIP 网关，IP Pbx 或 SBCs 之间的连接正常工作。

返回顶部

