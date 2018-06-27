---
title: '部署语音邮件和 UM: Exchange 2013 Help'
TOCTitle: 部署语音邮件和 UM
ms:assetid: 3df61b62-a1e4-41fb-969c-319189ae4e42
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673519(v=EXCHG.150)
ms:contentKeyID: 50490358
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 部署语音邮件和 UM

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

Exchange 统一消息 (UM) 使您能够为贵组织中的用户提供语音邮件服务。部署统一消息时，必须将 Exchange 服务器部署与贵组织中现有的电话服务系统或 Microsoft Lync Server 集成在一起。要成功进行部署，您需要仔细分析现有电话服务基础结构，并执行正确的计划步骤来部署和管理统一消息中的语音邮件。如果要将 Exchange 与 Lync Server 整合，还必须熟悉此产品。

部署统一消息时，您具有多个选项，具体取决于贵组织中的电话硬件。如果将 UM 连接到电话服务网络，则贵组织可以采取以下电话配置之一：

  - 一个或多个 VoIP 网关（使用一个或多个 PBX）

  - 一个或多个 IP PBX

  - 一个或多个启用了 SIP 的 PBX

  - Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 2010 或 2013

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在托管或混合环境中部署 Exchange UM 时，必须部署会话边界控制器 (SBC)。SBC 不支持将 UM 连接到电话服务网络，亦不支持为组织提供拨号音。但是，它们却可以使用通过公用或专用 WAN 的 IP 协议将您的内部 UM 部署连接到数据中心。</td>
</tr>
</tbody>
</table>


**电话硬件**   选择正确的 VoIP 网关、IP PBX 或 SBC，只是将电话服务网络与 UM 集成的第一步。您必须配置这些设备并使它们能与 UM 配合使用，部署必需的客户端访问服务器和邮箱服务器，以及创建和配置需要的所有 UM 组件。借助这些组件，您可以将基于电路的协议网络连接到 IP 数据网络，并为组织内的用户启用语音邮件功能。有关详细信息，请参阅[Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)。

**Microsoft Lync Server**   统一消息服务可以使用 Microsoft Lync Server 将语音邮件、即时消息、增强状态、音频/视频会议和电子邮件结合在一起，提供熟悉、整合的通信体验。将 UM 和 Lync Server 集成具有以下优点：

  - 跨多种应用程序的增强用户在线状态通知让用户始终了解联系人的可用情况。

  - 整合即时消息、语音邮件、会议、电子邮件及其他通信方法，允许用户为任务选择最适合的方法。用户还可以在需要时从一种方法切换为另一种方法。

  - 在具备 Internet 连接的任何位置的备用通信设备的可用情况。

  - 用于电话服务、即时消息和会议的智能客户端 (Microsoft Lync)。

  - 跨多个设备的用户体验连续性。

有关 Lync Server 的详细信息，请参阅 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

## 部署步骤

对统一消息可用的多个部署选项。每个选项都包含几个通用步骤，创建可伸缩的高可用性系统以支持大量用户时必须执行这些步骤。这些步骤如下：

1.  使用统一消息部署并配置电话服务组件或 Microsoft Lync Server。

2.  验证是否已经正确安装了统一消息所需的客户端访问和邮箱服务器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在配置 VoIP 网关或 IP PBX 以将 UM SIP 和 RTP 通信发送到 Exchange 2013 客户端访问服务器之前，您应在您的组织内部署至少一个 Exchange 2013 邮箱服务器。</td>
    </tr>
    </tbody>
    </table>


3.  创建和配置必需的统一消息组件，包括 UM 拨号计划、UM IP 网关、UM 智能寻线和 UM 邮箱策略。

4.  执行部署后任务，包括为相互 TLS 部署证书、创建 UM 自动助理和客户端功能。

有关部署统一消息的详细信息，请参阅[部署 Exchange 2013 UM](deploy-exchange-2013-um-exchange-2013-help.md)。

如果要将统一消息环境与 Microsoft Lync Server 集成，则应考虑其他规划因素。有关详细信息，请参阅[部署 Exchange 2013 UM 和 Lync Server 概述](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)。

