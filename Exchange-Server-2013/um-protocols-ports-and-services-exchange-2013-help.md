---
title: 'UM 协议、端口和服务: Exchange 2013 Help'
TOCTitle: UM 协议、端口和服务
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54652283
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 协议、端口和服务

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

MicrosoftExchange 2013 统一消息 (UM) 要求使用多个 TCP 和用户数据报协议 (UDP) 端口在运行 Exchange 2013 的服务器与其他设备之间建立通信。通过使用这些 IP 端口进行访问，可以使统一消息正常运行。本主题讨论 Exchange 2013 统一消息中使用的 TCP 和 UDP 端口。

## 统一消息协议和服务

Exchange 2013 统一消息功能和服务依靠静态和动态 TCP 和 UDP 端口，确保运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器和运行 Microsoft Exchange 统一消息服务的邮箱服务器正常工作。安装 Exchange 2013 后，将为 Exchange 添加静态入站 Windows 防火墙规则。如果更改客户端访问和邮箱服务器所使用的 TCP 端口，则可能还需要重新配置 Windows 防火墙规则才能使统一消息正常工作。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在运行 UM 组件和服务的 Exchange 2013 客户端访问和邮箱服务器上，Exchange 安装程序将创建入站防火墙规则，这些规则允许入站通信，而且没有任何 TCP 端口限制。添加 UM 服务的以下入站规则：</td>
</tr>
</tbody>
</table>


1.  **SESWorker (GFW) (TCP-In)**

2.  **UMCallRouter (GFW) (TCP-In)**

3.  **UMCallRouter (TCP-In)**

4.  **UMService (GFW) (TCP-In)**

5.  **UMService (TCP-In)**

6.  **UMWorkerProcess – RPC (TCP-In)**

7.  **UMWorkerProcess (GFW) (TCP-In)**

8.  **UMWorkerProcess (TCP-In)**

## 会话初始协议

会话初始协议 (SIP) 是一个用于启动、修改和结束涉及多媒体元素（例如，视频、语音、即时消息、联机游戏和虚拟现实）的交互式用户会话的协议。该协议以及 H.323 标准都是用于语音 IP (VoIP) 的领先信号传输协议。大多数基于 VoIP 标准的解决方案都是使用的 H.323 或 SIP。但也有其他的专有设计和协议。VoIP 协议通常支持呼叫等待、电话会议和呼叫转移等功能。

VoIP 网关和 IP 专用交换机 (PBX) 等 SIP 客户端可以使用 TCP 和 UDP 端口 5060 连接到 SIP 服务器，包括运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器。SIP 只能用于建立和挂断语音或视频呼叫。所有语音和视频通信都是通过实时传输协议 (RTP) 进行。

## 实时传输协议

RTP 定义了通过特定网络（例如 Internet）传输音频和视频时使用的标准数据包格式。RTP 只能通过网络传输语音/视频数据。呼叫建立和挂断通常是由 SIP 执行的。

RTP 不需要与标准或静态 TCP 或 UDP 端口进行通信。RTP 通信使用的是一个偶数 UDP 端口，相邻的较大奇数端口则用于 TCP 通信。虽然没有端口范围分配标准，但通常将 RTP 配置为使用端口号在 1024 到 65535 之间的端口，且运行 Microsoft Exchange 统一消息服务的邮箱服务器遵循此约定。由于 RTP 使用的是一个动态端口范围，因此通过防火墙会很难。

## 统一消息 Web 服务

邮箱服务器上安装的统一消息 Web 服务使用 IP 在客户端、邮箱服务器和运行其他 Exchange 2013 服务器角色的计算机之间进行网络通信。一些 Exchange 2013Outlook Web App 和 Outlook 2013 客户端功能依靠统一消息 Web 服务才能正常运行。

以下统一消息客户端功能依赖于统一消息 Web 服务：

  - Exchange 2013 Outlook Web App 提供的语音邮件选项，包括在电话上播放功能和重置 PIN 的功能。

  - Outlook 客户端中有“在电话上播放”功能。

## UM 端口

客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务使用 SIP 通过传输控制协议 (TCP) 或相互传输层安全性（相互 TLS）与运行 Microsoft Exchange 统一消息服务的邮箱服务器通信。为了避免 TCP/用户数据报协议 (UDP) 端口冲突，Microsoft Exchange 统一消息呼叫路由器服务和 Microsoft Exchange 统一消息服务默认为不同 TCP 端口并在这些端口上进行侦听。它们可以接受不安全和安全的连接，具体取决于是否将相互 TLS 用于 SIP 和 RTP 通信。默认情况下，在使用相互 TLS 时，客户端访问服务器会同时在 TCP 端口 5060（在非安全模式下）和 TCP 端口 5061（在 SIP 安全模式下）侦听 SIP 请求。这些端口可使用 **Set-UMCallRouterSettings** cmdlet 进行配置。客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务不处理媒体（RTP 或 SRTP）通信，因此仅使用 TCP 端口，而不使用 UDP 端口。默认情况下，在使用相互 TLS 时，邮箱服务器会同时在 TCP 端口 5062（在非安全模式下）和 TCP 端口 5063（在 SIP 安全模式下）侦听 SIP 请求。不能使用 Exchange 命令行管理程序 cmdlet 配置这些端口。邮箱服务器上的 Microsoft Exchange 统一消息服务会在 SIP 端口 5062 和 5063 上接受来自客户端访问服务器的连接。在客户端访问服务器将 SIP 请求重定向到邮箱服务器之后，会使用 VoIP 网关、IP PBX 或 SBC 和邮箱服务器上的 Microsoft Exchange 统一消息工作进程创建 RTP 或 SRTP 媒体通道。

下表汇总了 Exchange 2013 端口和协议以及这些端口是否可以更改。

### UM 侦听端口

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>协议</th>
<th>TCP 端口</th>
<th>UDP 端口</th>
<th>这些端口是否可以更改？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP（客户端访问服务器 – Microsoft 统一消息呼叫路由器服务）</p></td>
<td><p>5060（不安全）、5061（安全）。该服务同时侦听这两个端口。</p></td>
<td><p>不适用</p></td>
<td><p>可以，使用 <strong>Set-UMCallRouterSettings</strong> cmdlet。</p></td>
</tr>
<tr class="even">
<td><p>SIP（邮箱服务器 – Microsoft Exchange 统一消息服务）</p></td>
<td><p>5062（不安全）、5063（安全）。该服务同时侦听这两个端口。</p></td>
<td><p>不适用</p></td>
<td><p>不能更改端口。</p></td>
</tr>
<tr class="odd">
<td><p>SIP（邮箱服务器 - UM 工作进程）</p></td>
<td><p>5065 和 5067 用于 TCP（不安全）。5065 和 5067 用于相互 MTLS（安全）。如果您已将其设置为双协议模式，也可以使用 5066 和 5068。</p></td>
<td><p>不适用</p></td>
<td><p>不能更改端口。</p></td>
</tr>
<tr class="even">
<td><p>RTP（邮箱服务器 - UM 工作进程）</p></td>
<td><p>不适用</p></td>
<td><p>1024 到 65535 之间的端口。</p></td>
<td><p>可以在 msexchangeum.config 配置文件中更改端口。msexchangeum.config 文件位于 Exchange 2013 统一消息服务器的 \Program Files\Microsoft\Exchange\V15\bin 文件夹中。</p></td>
</tr>
</tbody>
</table>


## Lync Server 和 UM 端口

Exchange 2013 统一消息支持网络地址转换 (NAT) 遍历，并允许邮箱服务器的 RTP 媒体从隧道通过 NAT 防火墙。但是，若要这样做，必须还要在环境中部署 Microsoft Office Communications Server 2007 R2 和 Microsoft Lync Server 2010 或 Microsoft Lync 2013。如果在网络上部署了 Exchange 2013 和 Communications Server 2007 R2 或 Microsoft Lync Server 2010 或 Lync 2013，此部署将使运行 Microsoft Exchange 统一消息服务的邮箱服务器可以与 NAT 防火墙外部的终结点进行通信。邮箱服务器与 Communications Server 2007 R2、Microsoft Lync Server 2010 或 Lync 2013 池关联，并在服务于该特定 Communications Server 2007 或 Lync Server 池的计算机上，通过 A/V 身份验证服务获取相应的身份验证令牌。

A/V 身份验证服务用于使 RTP 语音媒体可以通过 NAT 设备和防火墙。由于媒体网关只处理信号，不能使语音安全地通过 NAT 设备或防火墙，所以，该服务是必不可少的。在 Communications Server 2007 R2、Lync Server 2010 或 Lync 2013 中配置中介服务器时，应指定运行 A/V 身份验证服务的 A/V 边缘服务器，以便于中介服务器了解传入媒体数据包转发的目标位置。

有关如何部署 Communications Server 2007 R2 或 Lync Server 2010 或 2013 和 Exchange 2013 统一消息的详细信息，请参阅以下主题：

  - [部署 Exchange 2013 UM 和 Lync Server 概述](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [检查表：将 Exchange 2013 UM 与 Lync Server 集成](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

