---
title: '统一消息中的 IPv6 支持: Exchange 2013 Help'
TOCTitle: 统一消息中的 IPv6 支持
ms:assetid: 91242c85-ce4e-422a-954e-ab623d3d6939
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150536(v=EXCHG.150)
ms:contentKeyID: 50491027
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 统一消息中的 IPv6 支持

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-04-07_

Internet 协议版本 6 (IPv6) 是 Internet 协议 (IP) 的最新版本。IPv6 旨在修正上一版本 IP 协议 IPv4 中的许多不足之处。在 Microsoft Exchange Server 2010 中，仅在也使用 IPv4 时才支持 IPv6。不支持纯 IPv6 Exchange 环境。仅在运行 Exchange 2010 的计算机上同时启用 IPv6 和 IPv4 且网络同时支持这两种 IP 地址版本时，才支持使用 IPv6 地址和 IP 地址范围。但是，由于 IPv4 和 IPv6 是完全不同的协议，所以 IPv4 网络无法直接与 IPv6 网络进行通信，反之亦然。为克服这一缺点，网络管理员需要部署路由器等设备，以便可以在 IPv4 网络与 IPv6 网络之间路由信息。如果同时使用 IPv4 和 IPv6 来部署 Exchange 2010，则除了统一消息 (UM) 以外的所有服务器角色均可从使用 IPv6 地址的设备、服务器和客户端收发数据。在 Exchange 2013 中，统一消息不再是 Exchange 2007 和 Exchange 2010 中的传输服务器角色、客户端访问服务器角色和邮箱服务器角色那样的独立服务器角色。与 UM 相关的组件和语音服务只在客户端访问服务器和邮箱服务器上运行。

在 Exchange 2013 中，由于 UM 体系结构已发生变化，并且现在要借助 Unified Communications Managed API (UCMA) v4.0 来同时支持 IPv4 和 IPv6 以及其他 Exchange 功能，所以具备统一消息组件和服务的客户端访问服务器和邮箱服务器将完全支持 IPv6 网络。

## IPv6 支持

在 Exchange 2010 Service Pack 1 (SP1) 及更高版本中，统一消息服务器角色一直依赖 UCMA 2.0 进行基础的会话初始协议 (SIP) 信号和语音处理。UCMA 2.0 是 UM 中的语音功能的主要组件。UCMA 2.0 包含 SIP 栈、媒体堆栈以及用于自动语音识别 (ASR) 和由文本到语音转换 (TTS) 生成的语音合成的语音引擎。

在 Exchange 2010 中，除 UM 以外的所有服务器角色都需要运行双协议栈（IPv4 和 IPv6），这是因为 UM 需要使用 UCMA 2.0，但仅支持 IPv4，而不支持 IPv6。对于 Exchange 2013，UCMA 4.0 不仅用于统一消息，并且对于在客户端访问服务器和邮箱服务器上安装 Exchange 2013 也是必需的。要支持新的功能和 IPv6，也需要使用 UMA 4.0。

UM 目前之所以使用 UCMA 4.0 来支持 Exchange 2013 中的新功能（包括 IPv6），是因为：

  - 一些政府部门需要为所使用的产品提供 IPv6 支持。

  - UM 目前需要与运行双协议栈（IPv4 和 IPv6）或仅运行 IPv6 的路由器、IP 网关、IP PBX 和会话边界控制器 (SBC) 等硬件设备兼容。

  - 在 Exchange 2013 中，Microsoft Exchange 统一消息服务在邮箱服务器上运行，而 Microsoft Exchange 统一消息呼叫路由器服务在客户端访问服务器上运行。Exchange 2013 中的邮箱服务器角色和客户端访问服务器角色既同时需要 IPv4 和 IPv6。

  - 联机服务允许客户端使用 IPv4 或 IPv6 连接到它们的服务。

  - 公用 IPv4 地址空间会不足。对于 Exchange Server 2013 Enterprise，这实际上不是 UM 的问题，因为 UM 始终与可以使用专用 IPv4 地址空间部署的内部 SIP 对等项通信。但是，如果是托管的 Exchange UM，客户的设备必须支持使用 IPv4 和 IPv6 连接托管的 UM。

除了 UM 和一小部分传输服务器角色之外，Exchange 2013 可以连接到组织中的 Exchange 2010 服务器，但前提是客户端访问服务器或邮箱服务器要运行在启用了 IPv4 和 IPv6 的双协议栈模式下。这意味着，客户可以在同时配置有 IPv4 和 IPv6 栈地址的计算机上安装 Exchange 2013。这样，IPv6 客户端和其他 Exchange 服务器，包括 Exchange Server 2010，将可以直接连接到 Exchange 2013。

UM 可在运行双协议栈模式的 Windows 服务器上正常工作。这是因为诸如 HTTP 的协议会忽略传输类型，并且 UM 使用不互相依赖的 Voice over IP (VoIP) 协议（包括 SIP/RTP/STUN/TURN/ICE）。这其中包括媒体放音协商 (RTP/SRTP)。在协商过程中，UM 会播发 IP 地址列表并将列表传递给 SIP 对等项，如 IP 网关、IP PBX 或 SBC。

## UM 支持 IPv6 意味着什么？

要使 Exchange 2013 UM 可以支持 IPv6，企业和联机 UM 管理员必须能够在将 UM 连接到支持 IPv6 的设备（包括路由器、IP 网关、IP PBX 以及 Office Communications Server 2007 R2 和 Microsoft Lync 服务器等设备）时利用 IPv6。但是，如果没有 IPv6 可用于实现与以前版本 Exchange 的互操作和向后兼容，管理员无需进行额外的配置更改，可以改用 IPv4。

对于 Exchange 2013 Enterprise，UM 必须直接与 SIP 对等项（IP 网关、IP PBX 和 SBC）通信，但这些对等项的软件或固件可能不支持 IPv6。因此，UM 必须能够直接与支持 IPv4 和（更重要的）IPv6 的 SIP 对等项通信。对于托管的 Exchange 2013，UM 通过 SBC 或 Lync Server 2010 或 Lync Server 15 与客户设备通信。在托管的 Exchange 2013 环境中，可能会部署可感知 SIP 的 IPv6 客户端（如 SBC 和 Lync 服务器），并将其用于处理\&quot;从 IPv6 到 IPv4\&quot;的转换过程。

## 针对 IPv6 的 UM 设备支持

因为运行 UM 组件和服务的 Exchange 2013 邮箱服务器和客户端访问服务器支持 IPv6，所以 IP 网关、IP PBX 和 SBC 供应商也必须能够支持 IPv6。有几个问题会影响设备对 IPv6 的支持：

  - 有些 IP 网关、IP PBX 和 SBC 可能能够支持 IPv6，但是尚未使用 IPv6 和 UM 进行测试。未来可能会添加这种支持，但这具体取决于硬件供应商。

  - 某些 IP 网关当前不支持 IPv6。

  - 某些 SBC 具备 IPv4-IPv6 功能，但是当前对 UM 无效，因为它们不支持 SRTP（安全实时传输协议）/SDES（会话描述协议安全性）。

  - 有些 IP PBX 不支持双协议栈和纯 IPv6，但是，尚未测试这些设备能否能与 Exchange 2013 配合使用。

目前，UCMA 4.0 支持 IPv6，意味着它可以接受 IPv6 连接，也可以在运行双协议栈模式时或进行出站连接时接受 IPv4。运行双协议栈模式，允许在需要使用 IPv4 连接到以前版本的 Exchange UM 时建立 IPv4 连接。对于 Lync 安装，将由 Lync Server 来完成。Lync Server 会从 Active Directory 获取最新版 Exchange Server 的版本信息。要使传统电话服务设备（包括 IP 网关、IP PBX 和 SBC）支持 IPv6 连接以及 IPv4，它们必须同时侦听这两种类型的连接。这是因为每个 SIP 对等项都必须能够接受这两种类型的连接，才能与以前版本的 Exchange UM 向后兼容。这对于同时支持这两类连接的外拨同样也是必要的。

## 用于支持 IPv6 的 UM 配置

安装客户端访问服务器和邮箱服务器之后，您需要创建统一消息拨号计划、自动助理、IP 网关和智能寻线。要使 UM 可以支持 IPv6，您必须：

  - 为网络上的每个 IP 网关、IP PBX 或 SBC 创建新的 UM IP 网关或配置现有的具有 IPv6 地址的 UM IP 网关。创建和配置所需的 UM IP 网关时，必须为 UM IP 网关添加 IPv6 地址或完全限定域名 (FQDN)。如果要将 FQDN 添加到 UM IP 网关，必须已创建了正确的 DNS 记录，以便将 UM IP 网关 的 FQDN 解析为 IPv6 地址。如果存在现有 UM IP 网关，则可以使用 **Set-UMIPgateway** cmdlet 配置 IPv6 地址或 FQDN。创建或配置 UM IP 网关之后，可以使用 **Get-UMIPgateway** cmdlet 查看 UM IP 网关的属性，以确保 IPv6 设置正确。

  - 在每个 UM IP 网关上配置 *IPAddressFamily* 参数。要使 IP 网关可以接受 IPv6 数据包，必须使用 **Set-UMIPgateway** cmdlet 并将 *IPAddressFamily* 参数设置为下列值之一，以设置 UM IP 网关同时接受 IPv4 和 IPv6 连接或仅接受 IPv6 连接：
    
      - *IPv4* – 此为默认值，在未配置任何其他值时使用。
    
      - *IPv6* - 设置为此值时，将可以使用 IPv6，但不能使用 IPv4。
    
      - *Any* – 此值支持使用 IPv6，但如果设备不支持 IPv6，将改用 IPv4。

  - 配置了 UM IP 网关之后，您还必须配置网络上的 IP 网关、IP PBX 和 SBC，使它们支持 IPv6。有关详细信息，请联系硬件供应商以了解支持 IPv6 的设备列表以及如何正确配置它们。

  - 另外，如果客户端访问服务器和邮箱服务器中有任何一类仅设置为接收 IPv4 流量，您可能需要将这两类服务器设置为接受 IPv6 流量。但是，默认设置是运行 Microsoft Exchange 统一消息呼叫路由服务的客户端访问服务器和运行 Microsoft Exchange 统一消息服务的邮箱服务器都接受 IPv4 和 IPv6 流量。有关在客户端访问服务器和邮箱服务器上配置 IPv6 设置的详细信息，请参阅 [Set-UMCallRouterSettings](https://technet.microsoft.com/zh-cn/library/jj215758\(v=exchg.150\)) 和 [Set-UMService](https://technet.microsoft.com/zh-cn/library/jj552412\(v=exchg.150\))。
    
    要支持 IPv6，可能需要在客户端访问服务器和邮箱服务器上配置以下两个参数：*IPAddressFamily* 和 *IPAddressFamilyConfigurable*。要使客户端访问服务器和邮箱服务器能够接受 IPv6 数据包，必须将客户端访问服务器和邮箱服务器设置为同时接受 IPv4 和 IPv6 连接，或者仅接受 IPv6 连接。要配置 *IPAddressFamily* 参数，必须将 *IPAddressFamilyConfigurable* 参数设置为 `$true`。

## UM IP 寻址逻辑

Exchange 2013 中 UM 的 IPv6 支持背后的逻辑如下所示：

  - 当启用了双协议栈，并且客户端访问服务器和邮箱服务器设置为 *IPv6* 或 *Any* 时，客户端访问服务器和邮箱服务器同时在 IPv4 和 IPv6 接口上侦听。否则，将仅使用 IPv4。

  - 对于传出呼叫，如果 UM IP 网关、客户端访问服务器和邮箱服务器的 *IPAddressFamily* 参数设置为 *IPv6* 或 *Any*，UM 将使用双协议栈模式。否则，将仅使用 IPv4。

在双协议栈模式下进行传出呼叫时，如果 *IPAddressFamily* 参数设置为 *IPv6* 或 *Any*：

  - UCMA 会获取它尝试到达的 SIP 对等项的 FQDN 中的地址列表。

  - UCMA 会尝试所有 IPv6 地址（如果有）。

  - 如果 UCMA 确定某个地址不可用，则它会将该地址包含在一个列表中，并且不会基于配置的间隔再次尝试该地址。这样可以防止不必要地重试已知的错误地址。

  - 如果没有任何 IPv6 地址可用，UCMA 会回退到 SIP 对等项地址列表中的 IPv4 地址。

