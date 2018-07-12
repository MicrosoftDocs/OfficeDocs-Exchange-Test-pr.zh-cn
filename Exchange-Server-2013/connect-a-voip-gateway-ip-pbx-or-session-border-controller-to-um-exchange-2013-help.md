---
title: '将 VoIP 网关、IP PBX 或会话边界控制器与 UM 连接: Exchange 2013 Help'
TOCTitle: 将 VoIP 网关、IP PBX 或会话边界控制器与 UM 连接
ms:assetid: a7cecf59-b93a-413b-bb88-29f2669ef2cf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124084(v=EXCHG.150)
ms:contentKeyID: 50556633
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将 VoIP 网关、IP PBX 或会话边界控制器与 UM 连接

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

在为组织部署统一消息 (UM) 时，必须正确配置 IP 语音 (VoIP) 网关和 IP 专用交换机 (PBX)。如果正在混合环境中部署 UM，也将需要正确部署会话边界控制器 (SBC)。为此，需要配置接口或 VoIP 网关、IP PBX 和 SBC 的接口，以便与运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器和运行 Microsoft Exchange 统一消息服务的邮箱服务器进行通信。

> [!IMPORTANT]  
> 如果使用 Web 浏览器对 VoIP 网关、IP PBX 或 SBC 执行管理任务，则通过网络发送的 HTTP 请求不会被加密。若要提高网络上 VoIP 网关、IP PBX 或 SBC 的安全级别，请使用 Internet 协议安全 (IPsec) 或安全套接字层 (SSL) 帮助保护通过网络传输的管理凭据和数据。我们还建议使用强大的身份验证机制和复杂的管理密码来保护设备的管理凭据。


## 电话 IP 设备接口

必须配置几种类型的端口或接口以支持 PBX、VoIP 网关、IP PBX 或 SBC 与网络上的客户端访问服务器和邮箱服务器之间的通信。配置 VoIP 网关、IP PBX 或 SBC 时，必须考虑设备是模拟、数字的还是模拟和数字都有。

如果连接 PBX 的 VoIP 网关接口是模拟接口，则必须正确地配置相应的设置，以便 VoIP 网关可以与客户端访问和邮箱服务器进行通信。对于 IP PBX 和 SBC，还必须正确地配置 IP 接口以支持这些设备与客户端访问服务器和邮箱服务器通信。所有这些设备都有不同类型的连接或端口，它们的可用情况取决于设备型号和供应商。

若要支持与网络上的客户端访问服务器和邮箱服务器通信，请执行以下操作：

  - 对于 VoIP 网关，必须配置电话接口才能与 PBX 通信，并且必须配置设置的 IP 接口。

  - 对于 IP PBX，必须配置基于线路的网络连接或基于 IP 的连接。

  - 对于 SBC，必须同时配置两个 IP 接口，一个接口用于网络，另一个接口用于通过 Internet 或专用 WAN 连接进行连接。

下面列出了 Exchange TechCenter 上的一些资源，提供的信息可以帮助您正确地配置 VoIP 网关、IP PBX 和 SBC：

  - **支持的 IP 网关、IP PBX 和 PBX 文档** [Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)中包含在配置 VoIP 网关、IP PBX、PBX 和 SBC 时可以使用的配置文件和设置信息。

  - **配置和技术说明** [支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)中包含在配置 VoIP 网关、IP PBX 和 PBX 时可以使用的配置文件和设置信息。

  - **Exchange UM 在线配置说明** [受支持的会话边界控制器的配置说明](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)中包含在配置 SBC 时可以使用的配置文件和设置信息。

统一消息专家可以协助配置电话和基于 IP 的网络设备。统一消息专家帮助确保从旧版或第三方语音邮件系统平稳过渡到统一消息，或者帮助使用 Exchange 统一消息规划和部署新的语音邮件系统。部署新的语音邮件系统或者升级旧版语音邮件系统需要大量有关 VoIP 网关、IP PBX、PBX 和统一消息的知识。有关如何联系统一消息专家的详细信息，请参阅 [Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists（Microsoft Exchange Server 2013 统一消息 (UM) 专家）](http://go.microsoft.com/fwlink/p/?linkid=262708)，或者咨询经过认证的 UM 合作伙伴（[Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)）。

在配置了 VoIP 网关、IP PBX 或 SBC IP 接口后，必须创建并配置 UM IP 网关以代表部署的每个设备。有关如何创建 UM IP 网关的详细信息，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

创建 UM IP 网关后，与 UM IP 网关相关的客户端访问和邮箱服务器会向 VoIP 网关、IP PBX 或 SBC 发送 SIP OPTIONS 请求，以确保设备具有响应能力。如果 VoIP 网关、IP PBX 或 SBC 未响应，邮箱服务器将记录一个 ID 为 1088 的事件，表明请求失败。为解决此问题，请确保 VoIP 网关、IP PBX 或 SBC 可用并且联机，且统一消息配置正确。

客户端访问服务器和邮箱服务器将仅与列为受信任会话初始协议 (SIP) 对等项的 VoIP 网关、IP PBX 或 SBC 通信。当多个 DNS 主机共享同一 IP 地址时，将记录一个 ID 为 1175 的事件。如果已使用网络上 VoIP 网关的 (FQDN) 配置 DNS 区域，则可能会发生此事件。统一消息通过检索邮箱服务器上统一消息 Web 服务虚拟目录的内部 URL，然后使用此 URL 生成受信任 SIP 对等项的 FQDN 列表来防止未经授权的请求。两个 FQDN 解析为同一个 IP 地址后，将记录该事件。

> [!NOTE]  
> 如果将 VoIP 网关、IP PBX 或 SBC 配置为具备 FQDN，并且 VoIP 网关、IP PBX 或 SBC 的 DNS 记录在启动统一消息服务后已更改，则必须重新启动 MicrosoftExchange 统一消息服务。如果不重新启动该服务，邮箱服务器将无法定位 VoIP 网关、IP PBX 或 SBC。这是因为邮箱服务器在内存中为所有 VoIP 网关、IP PBX 或 SBC 维护了一个缓存，且仅当该服务重启或者当 VoIP 网关、IP PBX 或 SBC 的配置更改时，才会执行 DNS 解析。

