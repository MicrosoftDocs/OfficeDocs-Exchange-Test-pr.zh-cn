---
title: 'UM IP 网关: Exchange 2013 Help'
TOCTitle: UM IP 网关
ms:assetid: 991d77e0-3995-44ab-bedf-52ff7a0301ab
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123890(v=EXCHG.150)
ms:contentKeyID: 50491214
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM IP 网关

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2014-06-24_

统一消息 (UM) IP 网关表示物理 IP 语音 (VoIP) 网关、IP 专用交换机 (PBX) 或会话边界控制器 (SBC) 硬件设备。必须先在目录服务中创建 UM IP 网关，才能使用 VoIP 网关、IP PBX 或 SBC 应答语音邮件用户的传入呼叫和发送其传出呼叫。

**目录**

UM IP 网关概述

UM IP 网关

UM IP 网关的 IPv6 支持

启用和禁用 UM IP 网关

## UM IP 网关概述

通常，*网关*一词用于表示连接两个不兼容网络的物理设备。通过 Exchange 统一消息和其他统一消息解决方案，可以使用 VoIP 网关在基于公用电话交换网 (PSTN)/时分多路复用 (TDM) 或基于电路交换的电话网络与 IP 或分组交换的数据网络之间进行转换。IP PBX 也可以在 PSTN 网络和分组交换的网络之间进行转换，因此使用 IP PBX 时，不需要 VoIP 网关。只有将旧有 PBX 硬件设备连接到 UM 部署时才需要 VoIP 网关。

> [!NOTE]
> 分组交换网络中的数据包（邮件或邮件片段）分别在路由器、交换机、VoIP 网关、IP PBX 和 SBC 等设备之间路由。与电路交换网相比，后者在两个节点之间建立专用连接，在通信期间独占使用。


Exchange 统一消息依靠 VoIP 网关的以下能力：将 PBX 中基于 TDM 或电话电路交换的协议（例如综合业务数字网络 (ISDN) 或 QSIG）转换为基于 VoIP 或 IP 的协议（例如会话初始协议 (SIP)、实时传输协议 (RTP) 或用于实时传真传输的 T.38）。

IP PBX 也可用于将电路交换的电话网络连接到数据网络或分组交换的网络。它们还可用于将电路交换协议转换为基于 VoIP 或 IP 的协议，如 SIP、RTP 和安全 RTPC (SRTP)。

会话边界控制器 (SBC) 与 VoIP 网关和 IP PBX 存在些微差别。它们用于连接公用网络（如 Internet）或私有 WAN 连接的两个数据网络，而不是将电路交换的网络连接到分组交换的网络。在统一消息中，SBC 可用于 UM 混合部署，其中 UM 使用某些内部部署组件以及其他位于云环境中的组件，如邮箱。

## VoIP 设备配置

尽管 PBX、VoIP 网关、IP PBX 和 SBC 有许多类型和制造商，但 VoIP 设备配置基本上有三种类型：

  - **IP PBX**   一个在 PSTN/TDM 或基于电路交换的电话网络与 IP 或分组交换的数据网络之间进行转换的设备

  - **PBX（旧版）和 VoIP 网关**   两个一起在 PSTN/TDM 或基于电路交换的电话网络与 IP 或分组交换的数据网络之间进行转换的单独组件

  - **SBC**   连接两种基于 IP 的网络（如局域网和数据中心）的一个或多个设备。

为了支持统一消息，将电话网络基础结构连接到数据网络基础结构或连接内部部署与云环境中的 UM 部署时，会使用一种或两种 IP/ VoIP 设备配置。

## UM IP 网关

UM IP 网关包含一个或多个 UM 智能寻线和配置设置。UM 智能寻线用于将 UM IP 网关链接到 UM 拨号计划。结合使用 UM IP 网关与 UM 智能寻线功能，可以在 VoIP 网关、IP PBX 或 SBC 与 UM 拨号计划之间建立链接。通过创建多个 UM 智能寻线，可以将一个 UM IP 网关与多个 UM 拨号计划关联。

创建 UM IP 网关后，链接到 UM IP 网关的 Exchange 服务器会向 VoIP 网关、IP PBX 或 SBC 发送 SIP OPTIONS 请求，以确保设备具有响应能力。如果 VoIP 网关、IP PBX 或 SBC 未响应该请求，Exchange 服务器将记录一个 ID 为 1400 的事件，表明请求失败。如果发生这种情况，请确保 VoIP 网关、IP PBX 或 SBC 可用并且联机，以及统一消息配置正确。

邮箱服务器只与作为受信任 SIP 对等项列出的 VoIP 网关、IP PBX 或 SBC 通信。在某些情况下，如果将两个 VoIP 网关、IP PBX 或 SBC 配置为使用相同的 IP 地址，将记录一个 ID 为 1175 的事件。统一消息通过检索统一消息 Web 服务虚拟目录的内部 URL 防止未经授权的请求，然后使用 URL 生成受信任 SIP 对等项的 FQDN 列表。当两个 FQDN 解析为同一个 IP 地址时，将记录此事件。

## UM IP 网关的 IPv6 支持

Internet 协议版本 6 (IPv6) 是 Internet 协议 (IP) 的最新版本。IPv6 旨在修正上一版本 IP 协议 IPv4 中的许多不足之处。在 Microsoft Exchange Server 2010 内部部署和混合部署中，仅在也使用 IPv4 时才支持 IPv6。

在 Exchange 2013 内部部署和混合部署中，UM 相关组件和语音服务仅在客户端访问和邮箱服务器上运行。由于 UM 体系结构已发生更改，现在需要统一通信托管 API (UCMA) v4.0 来支持 IPv4 和 IPv6 以及其他 Exchange 功能，因此包含统一消息组件和服务的客户端访问和邮箱服务器完全支持 IPv6 网络，且不需要 IPv4。

在内部部署、混合部署和 Exchange Online 部署中，企业和 Exchange Online UM 管理员可以使用 IPv6 将 UM 连接到支持 IPv6 的设备，包括路由器、IP 网关、IP PBX 以及 Microsoft Office Communications Server 2007 R2 和 Microsoft Lync Server。但是，如果 UM IP 网关上的 *IPAddressFamily* 参数设置为 `Any`，则可以改用 IPv4，而无需进行其他配置更改，以便实现互操作和向后兼容。

Exchange UM 必须仍然直接与在其软件或固件中不能支持 IPv6 的 SIP 对等项（VoIP 网关、IP PBX 和 SBC）通信。如果它们不支持 IPv6，则 UM 必须能够直接与使用 IPv4 的 SIP 对等项通信。对于托管语音邮件，UM 通过 SBC、Lync Server 2010 或 Lync Server 2013 与客户设备通信。在托管环境中，可以部署 IPv6 SIP 感知客户端（如 SBC 和 Lync Server）以处理 IPv6 到 IPv4 的转换过程。

对于安装客户端访问服务器和邮箱服务器后的内部部署和云部署，以及对于 Exchange Online UM 部署，需要创建 UM IP 网关。如果需要 UM IP 网关支持 IPv6，还必须执行下列操作：

1.  为网络上的每个 IP 网关、IP PBX 或 SBC 创建新的 UM IP 网关或配置现有的具有 IPv6 地址的 UM IP 网关。在创建和配置所需 UM IP 网关时，必须为 UM IP 网关添加 IPv6 地址或完全限定域名 (FQDN)。如果将 FQDN 添加到 UM IP 网关，则必须创建正确的 DNS 记录才能将 UM IP 网关 FQDN 解析为 IPv6 地址。如果存在现有 UM IP 网关，则可以使用 **Set-UMIPgateway** cmdlet 配置 IPv6 地址或 FQDN。

2.  在每个 UM IP 网关上配置 *IPAddressFamily* 参数。要启用 VoIP 网关以接受 IPv6 数据包，必须使用 **Set-UMIPgateway** cmdlet 将 UM IP 网关设置为同时接受 IPv4 和 IPv6 连接，或仅接受 IPv6 连接。

3.  在配置了 UM IP 网关之后，还必须在网络上将 VoIP 网络、IP PBX 和 SBC 配置为支持 IPv6。有关详细信息，请联系硬件供应商以了解支持 IPv6 的设备列表以及如何正确配置它们。

> [!NOTE]
> 每个拨号计划的 UM IP 网关的最大值为 200,。如果您创建了多于 200 个网关，则 UM 服务将不会启动。


## 启用和禁用 UM IP 网关

默认情况下，UM IP 网关在创建后处于启用状态。但是，可以启用或禁用 UM IP 网关。如果禁用 UM IP 网关，您可以将其设置为强制所有 Exchange 服务器删除现有呼叫。您可以将其设置为强制与 UM IP 关联的 Exchange 服务器停止处理 VoIP 网关、IP PBX 或 SBC 提供的任何新呼叫。

如果正在集成统一消息和 Office Communications Server R2 或 Microsoft Lync Server，则只能允许一个 UM IP 网关发出用户的传出呼叫，并禁用所有其他与 SIP URI 拨号计划关联的 UM IP 网关上的出站呼叫。使用命令行管理程序或 EAC 禁用出站呼叫。

为内部部署和混合部署选择允许出站呼叫通过的 UM IP 网关时，选择可能会处理大部分通信的网关。不允许传出的流量通过连接到 Lync Server Director 池的 UM IP 网关。必须确保运行 Microsoft Exchange 统一消息服务的邮箱服务器（例如，在“在电话上播放”方案中）向外部用户发出的出站呼叫能够可靠地遍历企业防火墙。

