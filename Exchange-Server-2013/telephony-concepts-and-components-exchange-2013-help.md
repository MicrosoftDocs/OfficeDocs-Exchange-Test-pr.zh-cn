---
title: '电话概念和组件: Exchange 2013 Help'
TOCTitle: 电话概念和组件
ms:assetid: ce70bf6a-db85-411b-8b93-2987703963a9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124606(v=EXCHG.150)
ms:contentKeyID: 54652299
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 电话概念和组件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-25_

如果要在网络上规划和部署 MicrosoftExchange 2013 统一消息 (UM)，则必须了解统一消息和电话网络。本主题概述电话基础结构的概念和组件，将帮助您规划和部署运行 Exchange 2013 统一消息的服务器。

**目录**

概述

概念和组件

电路交换网络

数据包交换网络

PBX

IP PBX

启用 SIP 的 PBX

VoIP

IP 网关

## 概述

在 Exchange Server 2007 之前的 Microsoft Exchange 版本中，Exchange 管理员的主要职责是管理电子邮件，有时也管理网络基础结构。早期版本的 Exchange 没有统一消息功能。Exchange Server 版本 5.5、Exchange 2000 Server 和 Exchange Server 2003 管理员重点关注 Exchange 环境和网络基础结构，并且很大程度上依靠电话顾问来管理电话环境和基础结构。

## 概念和组件

若要成功在 Exchange 2013 中部署统一消息 (UM)，您必须对基本的电话概念和电话组件有很好的了解。在详细了解电话的基础知识之后，可以成功地将 Exchange 2013 统一消息集成到 Exchange 2013 组织中。基本概念和组件包括下列项目：

  - 电路交换和数据包交换网络

  - 专用交换机 (Private Branch eXchange, PBX)

  - IP PBX

  - Voice over Internet 协议 (VoIP)

  - VoIP 网关

## 电路交换网络

在电路交换网络（例如公用电话交换网 (PSTN)）中，通过相同的传输介质传输多个呼叫。PSTN 中常用的介质是铜线。但是，也可能会使用光缆。

电路交换网络中存在专用的连接。专用连接是在两个节点之间建立的电路或信道，以便可以进行通信。在两个节点之间建立呼叫之后，只有这两个节点可以使用该连接。其中一个节点结束呼叫时，将取消连接。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PSTN 是全球公用电路交换电话网络的组合。此组合类似于 Internet 是全球公用 IP 数据包交换网络的组合。</td>
</tr>
</tbody>
</table>


电路交换网络有两种基本类型：模拟和数字。模拟网络用于语音传输。许多年来，PSTN 只是模拟网络，但是现在，基于电路的网络（例如 PSTN）已从模拟网络转换为数字网络。为了支持通过数字网络传输模拟语音传输信号，必须将模拟传输信号编码或转换为数字格式，然后再传入电话 WAN。在连接的接收端，必须将数字信号解码或转换回模拟信号格式。

电路交换网络有优点也有缺点。电路交换网络有多个缺点。电路交换网络效率可能相对较低，因为可能会浪费带宽。在数据包交换网络上使用 VoIP 时，则不是这种情况。VoIP 与所有其他网络应用共享可用带宽，这样可以更加有效地使用可用带宽。电路交换网络的另一个缺点是，必须为高峰使用时间需要的最大电话呼叫数提供资源，并为占用支持最大呼叫数的电路付费。

与数据包交换网络相比，电路交换有一个很大的优点。在电路交换网络中使用电路时，您在使用该电路的时间内将拥有整个电路，不会与其他用户争用。数据包交换网络则不是这种情况。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>同步数字层次结构 (SDH) 已成为大多数 PSTN 网络的主要传输协议。SDH 通过光纤网络携带。</td>
</tr>
</tbody>
</table>


返回页首

## 数据包交换网络

数据包交换是一种将数据邮件拆分成更小的单元（称为数据包）的技术。数据包通过可用的最佳路由发送到目标地址，然后在接收端重新组合。

在数据包交换网络（例如 Internet）中，数据包通过最佳路由传输到目标地址，但是并非在两个主机间传输的所有数据包都通过相同的路由，即使是来自一封邮件的数据包也是如此。这几乎可以确定数据包将在不同时间无顺序地到达。在数据包交换网络中，数据包（邮件或邮件片断）通过可能由其他节点共享的数据链路在两个节点之间分别路由。数据包交换与电路交换不同，与网络节点的多个连接将共享可用带宽。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对于电路交换，所有数据包沿着一条路径按顺序到达接收端。</td>
</tr>
</tbody>
</table>


使用数据包交换网络，可通过 Internet 在全球范围内进行数据通信。公用数据网络或数据包交换网络与 PSTN 在数据通信方面互为补充。

在 LAN 和 WAN 网络等网络环境中也可以找到数据包交换网络。WAN 数据包交换环境依赖于电话线路，但是线路的布置要保持与终结点的永久连接。在 LAN 数据包交换环境（例如以太网网络）中，数据包的传输依赖于数据包交换机、路由器和 LAN 电缆。在 LAN 中，交换仅在两个其间距足以发送当前数据包的网段之间建立连接。传入数据包保存到临时内存区或内存缓冲区中。在基于以太网的 LAN 中，以太网帧包含数据包的有效负载（或数据）部分以及包含数据包的来源和目标的介质访问控制 (MAC) 地址信息的特殊头。数据包到达目标地址后，将通过数据包组合程序按顺序放回。因为数据包可能采用不同的路由，所以需要数据包组合程序。

数据包交换网络使 Internet 的存在成为可能，同时，可以提高数据网络（尤其是基于 LAN 的 IP 网络）的可用性并增大覆盖范围。

返回页首

## PBX

旧式 PBX 是充当交换机的电话设备，用于在电话或电路交换网络中切换呼叫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>旧式 PBX 是无法传递 IP 数据包的 PBX。在很多公司，旧式 PBX 已更换为 IP PBX。</td>
</tr>
</tbody>
</table>


PBX 是大部分大中型公司都在使用的电话设备。PBX 使 PBX 的用户或订阅者可以共享一定数量的外线，从而拨打被视为 PBX 外部的电话。与为公司中每个用户提供专用的外线电话相比，PBX 解决方案成本要低得多。PBX 可以连接电话、传真机、调制解调器以及许多其他的通信设备。

PBX 设备通常安装在企业的办公场所，可以在位于并在企业场所中安装的电话机之间建立呼叫连接。通常提供有限数量的外线（也称为中继线）供拨打和接听来自外部源（例如 PSTN）的公司外部呼叫。

在某些系统中，要在公司内部使用 PBX 拨打外部电话号码，可以拨打 9 或 0，然后拨打外部号码。系统会自动选择外线来完成呼叫。反之，在公司内部用户之间的呼叫通常不要求拨打特殊号码或使用外线。这是因为内部呼叫由 PBX 在物理连接到 PBX 的电话之间进行路由或交换。

在大中型公司中。可以使用下列 PBX 配置：

  - 支持整个公司的单个 PBX。

  - 未联网或未互相连接的两个或更多 PBX 的组合。

  - 连接在一起或联网的两个或更多 PBX 的组合。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 UM 拨号计划可以跨越多个 PBX 或 IP PBX。</td>
</tr>
</tbody>
</table>


返回页首

## IP PBX

IP PBX 是一种 PBX，它支持 IP 协议使用以太网或数据包交换 LAN 连接电话，并在 IP 数据包中发送语音通话。混合 IP PBX 既支持 IP 协议在数据包中发送语音通话，也支持连接传统的模拟和数字电路交换时分多路复用 (TDM) 电话。IP PBX 是私人公司中的电话交换设备，而不是电话公司中的电话交换设备。

IP PBX 通常要比旧版的 PBX 更易于管理，因为管理员可以轻松地使用 Internet 浏览器或其他基于 IP 的实用工具来配置其 IP PBX 服务。此外，您还无需安装其他任何线路、电缆或配线盘。使用 IP PBX 移动基于 IP 的电话机就像拔掉电话线将其插在新位置一样简单，而无需高额的电话服务费用来移动旧版的 PBX 供应商提供的电话机。此外，拥有 IP PBX 的企业不必增加额外的基础结构成本来维护和管理两个独立的电路交换网络和数据包交换网络。

## 启用 SIP 的 PBX

启用 SIP 的 PBX 是充当网络交换机的电话设备，用于在电话或电路交换网络中切换呼叫。但是，启用 SIP 的 PBX 与传统 PBX 的区别在于，前者可以连接到 Internet 并使用 SIP 协议在 Internet 上进行呼叫。

启用 SIP 的 PBX 使用的呼叫格式包括一个 SIP URI，其中包含全局 E.164 号码和\&quot;user=phone\&quot;参数。例如：sip:+14255551234@contoso.com;user=phone

E164 号码以置前的\&quot;+\&quot;打头，不包含手机上下文参数或任何分隔符。启用 SIP 的 PBX 支持 TCP 和 UDP。UDP 仍广泛用于旧版系统。启用 SIP 的 PBX 也支持相互传输层安全性（相互 TLS）和 DNS 查找。

## VoIP

IP 电话 (VoIP) 技术包含的硬件和软件使用户可以使用基于 IP 的网络作为电话呼叫的传输介质。在 VoIP 中，使用 IP 在数据包中发送语音数据，而不是通过传统的电路传输或 PSTN 的电路交换电话线路。连接到 IP 网络上的 VoIP 网关使用 VoIP 协议在 Exchange 2013 客户端访问和邮箱服务器以及 PBX 系统之间发送语音数据包。

## VoIP 网关

VoIP 网关是将旧式 PBX 连接到 LAN 的第三方硬件设备或产品。VoIP 网关允许 PBX 系统与运行 Microsoft Exchange 统一消息和统一消息呼叫路由器服务的 Exchange 2013 邮箱和客户端访问服务器进行通信。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>VoIP 网关还可以连接到使用 VoIP（而不是 PSTN 电路交换协议）的 PBX 系统。</td>
</tr>
</tbody>
</table>


Exchange 2013 统一消息依靠 VoIP 网关的以下能力：将 PBX 中基于 TDM 或电话电路交换的协议（例如 ISDN 和 QSIG）转换为基于 IP 或 VoIP 的协议（例如会话初始协议 (SIP)、实时传输协议 (RTP) 或用于实时传真传输的 T.38）。VoIP 网关对统一消息的功能和运行是不可或缺的。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>安装了 VoIP 网关、IP PBX 或启用了 SIP 的 PBX 之后，必须创建用于代表物理设备的 UM IP 网关。在创建了 UM IP 网关后，使用 UM IP 网关链接的客户端访问服务器和邮箱服务器将向 VoIP 网关、IP PBX 或启用了 SIP 的 PBX 发送 SIP OPTIONS 请求，以确保设备有响应。如果 VoIP 网关对邮箱服务器的 SIP OPTIONS 请求没有响应，邮箱服务器将记录一个 ID 为 1088 的事件，表明请求失败。若要解决此问题，请确保 VoIP 网关、IP PBX 或启用了 SIP 的 PBX 可用并且联机，并且客户端访问服务器和邮箱服务器上的统一消息配置均正确。</td>
</tr>
</tbody>
</table>


有关 IP PBX 和 PBX 配置的详细信息，请参阅[PBX 和 IP PBX 配置](pbx-and-ip-pbx-configurations-exchange-2013-help.md)。

返回页首

## 详细信息

[UM 协议、端口和服务](um-protocols-ports-and-services-exchange-2013-help.md)

[Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

