---
title: '统一消息规划: Exchange 2013 Help'
TOCTitle: 统一消息规划
ms:assetid: 942788b1-b19d-40b3-a52e-2e1fef8df3f9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674306(v=EXCHG.150)
ms:contentKeyID: 50491050
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 统一消息规划

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

规划统一消息 (UM) 部署时，必须要考虑许多因素才能成功部署 UM。必须了解统一消息的不同要素以及各个组件和功能，以便合理规划统一消息的基础结构和部署。在组织中部署统一消息时，分配一些时间来进行规划和处理这些问题将有助于防止出现各种状况。

可以在一个新的 Exchange 组织中部署统一消息，也可以对旧有或第三方语音邮件解决方案进行升级。如果要进行升级，需要确定是否要将接受电话服务线路协议的设备转换为使用 IP 的数据网络，或者是否要部署 Microsoft Lync Server 一类的企业语音解决方案。在准备了解 UM 并为组织部署 UM 的过程中，这些仅仅是第一步。

## 规划语音邮件系统

UM 在一个存储中提供语音邮件、传真和电子邮件传送服务，该存储可以从电话、用户计算机或移动设备进行访问。用户可以从电子邮件客户端（如 Outlook 和 Outlook Web App）访问位于 Exchange 邮箱中的语音邮件、电子邮件、日历信息和个人联系人信息。

有两种服务器可为组织中的用户提供语音邮件功能：一种是运行 Microsoft Exchange 统一消息呼叫路由服务的客户端访问服务器，另一种是运行 Microsoft Exchange 统一消息服务的邮箱服务器。

邮箱服务器依赖客户端访问服务器转发来自传入呼叫的 SIP 流量，然后与 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 建立连接，接受 RTP/SRTP 媒体流量。所有语音邮件和传真邮件通过邮箱服务器上的 Microsoft Exchange 统一消息服务提交，以传递到用户的邮箱。如果用户要将语音邮箱功能与统一消息配合使用，必须具备一个 Exchange 邮箱。

## 规划 UM 部署

一般而言，统一消息的拓扑越简单，UM 的部署和维护越容易。从满足业务和组织目标的实际需要出发，安装尽可能少的客户端访问服务器和邮箱服务器，创建尽可能少的统一消息组件（如 UM 拨号计划、自动助理和 UM 邮箱策略）。与在统一消息方面需求相对简单的小型组织相比，拥有复杂网络和电话环境、多个业务单位或其他复杂情况的大型企业需要进行更细致的规划。

在组织中规划统一消息时，应考虑到下列几个方面：

  - **组织要求**   评估业务需求、部署语音邮件系统的用处、物理网络和业务拓扑结构，以及组织的安全性要求。

  - **电话服务系统要求**   检查现有的电路服务、线路交换网络和语音邮件系统。

  - **网络要求**   分析网络拓扑结构、当前的分组交换 IP 网络设计（包括 LAN 和 WAN 连接点）和相关设备。

  - **Active Directory（目录服务）**   检查当前的实施情况和设计，考虑如何整合 UM。

  - **部署模式**   决定是要采用混合式、仅在线式还是内建式 UM 部署。

  - **Exchange 要求**   确定下列事项：
    
      - 将有多少用户使用语音邮件。
    
      - 要部署哪些 UM 功能和服务，如并发呼叫、用户内部和外部访问、传入传真、语音邮件预览等。
    
      - 需要部署的客户端访问服务器和邮箱服务器的数量。
    
      - 语音邮件用户的存储要求和配额。
    
      - 实现高可用性和站点恢复能力的最佳设计。这包括 UM 的系统要求（提供具有高可用性和高伸缩性的 UM 部署）以及系统硬件要求，以确保良好的性能。

  - **与电话服务组件和设备的集成**   决定是使用传统电话服务设备还是 Microsoft Lync Server。考虑在何处放置 VoIP 网关、电话服务设备以及客户端访问服务器和邮箱服务器，并考虑是否要在组织中启用企业语音功能。

## 连接电话服务网络

统一消息要求将 Exchange 服务器部署与现有的电话服务系统或 Microsoft Lync Server 集成在一起。需要仔细分析现有的电话服务基础结构和 Microsoft Lync Server，然后按正确的规划步骤操作，才能成功部署和管理 UM 语音邮件。

**VoIP 网关** 选择正确的 VoIP 网关、IP PBX、启用了 SIP 的 PBX 或 SBC，只是将电话服务网络与 UM 集成的第一步。必须配置这些设备并使它们能与 UM 配合使用，部署必需的客户端访问服务器和邮箱服务器，以及创建和配置所有必要的 UM 组件。借助这些组件，可以建立从线路协议网络到 IP 数据网络的连接，并为用户启用语音邮件功能。

**Microsoft Lync Server**   统一消息服务可以使用 Microsoft Lync Server 将语音邮件、即时消息、增强状态、音频/视频会议和电子邮件结合在一起，提供熟悉、整合的通信体验。将 UM 和 Microsoft Lync Server 集成具有以下优点：

  - 跨多种应用程序的增强用户在线状态通知让用户始终了解联系人的可用情况。

  - 整合即时消息、语音邮件、会议、电子邮件及其他通信方法，让用户能够选择最适合任务的方法。用户还可以在需要时从一种方法切换为另一种方法。

  - 在具备 Internet 连接的任何位置的备用通信设备的可用情况。

  - 用于电话服务、即时消息和会议的智能客户端 (Microsoft Lync)。

  - 跨多个设备的用户体验连续性。

有关 Microsoft Lync Server 的详细信息，请参阅 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>规划和部署统一消息可能会带来一定的挑战。根据在 Exchange 和语音邮件系统方面的技术经验，可能需要从统一消息专家那里获取帮助。Exchange 统一消息专家将帮助确保从旧有或第三方语音邮件系统顺利过渡到 Exchange 统一消息。执行新部署或升级旧有语音邮件系统需要大量 VoIP 网关、PBX 和统一消息方面的知识。有关如何联系统一消息专家的详细信息，请参阅 <a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists（Microsoft Exchange Server 2013 统一消息 (UM) 专家）</a>。</td>
</tr>
</tbody>
</table>


## 部署步骤

统一消息有多个可用的部署选项。每个选项都包含几个通用步骤，创建可伸缩的高可用性系统以支持大量用户时必须执行这些步骤。这些步骤如下：

1.  使用统一消息部署并配置电话服务组件或 Microsoft Lync Server。

2.  验证是否已经正确安装了统一消息所需的客户端访问和邮箱服务器。

3.  创建和配置必需的统一消息组件，包括 UM 拨号计划、UM IP 网关、UM 智能寻线和 UM 邮箱策略。

4.  执行部署后任务，包括获取相互 TLS 证书、创建 UM 自动助理和配置传真。

有关部署统一消息的详细信息，请参阅[部署 Exchange 2013 UM](deploy-exchange-2013-um-exchange-2013-help.md)。

如果要将统一消息环境与 Microsoft Lync Server 集成，则应考虑其他规划因素。有关详细信息，请参阅[部署 Exchange 2013 UM 和 Lync Server 概述](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)。

