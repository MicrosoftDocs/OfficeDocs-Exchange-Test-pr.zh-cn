---
title: '与 UM 电话系统集成: Exchange Online Help'
TOCTitle: 与 UM 电话系统集成
ms:assetid: b8790117-b040-4c84-9d34-005c75088e76
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673558(v=EXCHG.150)
ms:contentKeyID: 50556648
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 与 UM 电话系统集成

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

若要成功部署统一消息 (UM)，必须更好地理解基本的电话概念和电话服务组件。在了解电话服务基础知识后，您可以将 UM 集成到 Exchange 组织。基本概念和组件如下所示︰

  - 电路交换和数据包交换网络

  - 专用交换机 (Private Branch eXchange, PBX)

  - IP PBX

  - Voice over Internet 协议 (VoIP)

  - VoIP 网关

在内部，混合或Office 365的环境中，连接和配置所需的电话组件是成功部署 UM，带有或不带 Lync 服务器企业语音的最复杂和最重要一步。您需要连接和配置先进的 VoIP 网关、 Pbx、 IP Pbx 和会话边框控制器 (SBCs) 的传统电话网络的 VoIP 网关连接到电话网络中，如果您将使用 Microsoft Lync Server 和 UM。

规划和部署新的 UM 部署或升级旧的语音邮件系统可能会带来挑战的组织。它要求有关 VoIP 网关、 Pbx、 IP Pbx、 Microsoft Lync 服务器和统一消息的重要知识。根据交换和语音邮件系统与您的技术经验，您可能想要获得统一消息专家的协助。Exchange 统一消息专家将帮助确保从旧式或第三方语音邮件系统平滑过渡到 Exchange 统一消息。有关如何联系统一消息专家的详细信息，请参阅[Microsoft Exchange Server 2013年统一消息 (UM) 专家](http://go.microsoft.com/fwlink/p/?linkid=262708)。

## 集成电话网络

统一的消息要求您使用现有的电话网络集成您的 Exchange Server 部署或为您的组织使用 Microsoft Lync Server 集成 UM。若要成功部署和管理 UM 语音邮件，您需要进行仔细分析您的现有电话基础架构或 Microsoft Lync 服务器企业语音部署并完成必要的规划步骤。

## VoIP 网关

如果要在 Exchange 组织中部署 UM，必须安装、部署并配置单个或多个 VoIP 网关以连接到电话网络中的 PBX，或者安装、部署并配置支持会话初始协议 (SIP) 的 PBX 或 IP PBX。

VoIP 网关是将传统的 PBX 连接到 LAN 的第三方硬件设备。VoIP 网关允许 PBX 系统与您组织中的 Exchange 服务器进行通信。

UM 依赖 VoIP 网关的翻译或转换时分多路复用技术 (TDM) 或电路交换基于的协议，如 ISDN 和 QSIG 从 PBX 如 SIP、 实时传输协议 (RTP) 或 T.38 的基于 IP 的或基于 VoIP 协议的实时传真传输的能力。VoIP 网关是不可或缺的功能和操作的 UM 的一部分。VoIP 网关还可以连接到 PBX 系统，而不是公用交换的电话网络 (PSTN) 电路交换协议使用 VoIP。

选择正确的 VoIP 网关，IP PBX、 SIP 启用 PBX、 或 SBC 是只有第一部分与 UM 集成电话网络。您必须配置这些设备与 UM 工作。在内部和混合部署中，您将需要部署所需的客户端访问和邮箱服务器，并创建和配置所有必需的 UM 组件。对于承载的语音邮件， Office 365 ，不是要求您安装和配置的任何服务器。组件允许您要从您的电话连接，电路交换网与 IP 数据网络并使您的组织中的用户的语音邮件。有关详细信息和支持电话服务设备，请参阅以下资源︰

  - [Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

  - [支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [受支持的会话边界控制器的配置说明](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

## Microsoft Lync Server

统一的消息可以使用 Microsoft Lync Server 将语音邮件、 即时消息、 增强的状态显示、 音频/视频会议和电子邮件组合到一个熟悉的、 集成的通信体验。将 UM 和 Microsoft Lync Server 集成企业语音功能向您组织中的用户具有以下优点︰

  - 跨多种应用程序的增强用户在线状态通知让用户始终了解联系人的可用情况。

  - 集成的即时消息、 语音邮件、 会议、 电子邮件和其他通信模式，使用户可以选择为任务最合适的模式。用户可以还从一个模式切换到另一个根据需要。

  - 在具备 Internet 连接的任何位置的备用通信设备的可用情况。

  - 用于电话服务、即时消息和会议的智能客户端 (Microsoft Lync)。

  - 跨多个设备的用户体验连续性。

嗯 Exchange 路由组件处理语音邮件路由之间 Lync 服务器和 Exchange 服务器将 Lync Server 集成与统一消息功能。Lync 服务器中找到该 UM Exchange 路由组件还可以处理通过 PSTN 重排的语音邮件，如果 Exchange 服务器不可用。如果您有企业语音部署在分支机构站点，并且这些网站不具有弹性的 WAN 链接到中心站点，分支地点部署高存活力分支装置提供语音邮件分支用户如果 WAN 链接发生故障。WAN 链接不可用时，高存活力的分支装置执行以下任务︰

  - 将未应答的呼叫通过 PSTN 重新路由到中心站点中的 Exchange 服务器。

  - 支持用户通过 PSTN 检索语音邮件。

  - 将未接来电通知排队，然后在 WAN 链接恢复时将它们上传到 Exchange 服务器。

有关 Microsoft Lync 服务器的详细信息，请参阅[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当您正在集成统一消息和 Lync 服务器在内部部署中，或位于 Exchange 2007 或 Exchange 2010 邮箱服务器混合部署，未接来电通知没有可供拥有邮箱的用户。在用户断开呼叫发送到邮箱服务器之前，会生成未接的来电通知。</td>
</tr>
</tbody>
</table>

